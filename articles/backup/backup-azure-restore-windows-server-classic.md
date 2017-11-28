---
title: "aaaRestore 資料 tooa Windows Server 或 Windows 用戶端從 Azure 中，使用 hello 傳統部署模型 |Microsoft 文件"
description: "深入了解如何從 Windows Server 或 Windows 用戶端 toorestore。"
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: 85585dfc-c764-4e8c-8f0e-40b969640ac2
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: saurse;trinadhk;markgal;
ms.openlocfilehash: 4d1458d5233c4f55004ecfa95cbf7b3b18a03dde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="restore-files-tooa-windows-server-or-windows-client-machine-using-hello-classic-deployment-model"></a><span data-ttu-id="fe29d-103">還原檔案 tooa Windows server 或 Windows 用戶端電腦使用 hello 傳統部署模型</span><span class="sxs-lookup"><span data-stu-id="fe29d-103">Restore files tooa Windows server or Windows client machine using hello classic deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fe29d-104">傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="fe29d-104">Classic portal</span></span>](backup-azure-restore-windows-server-classic.md)
> * [<span data-ttu-id="fe29d-105">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="fe29d-105">Azure portal</span></span>](backup-azure-restore-windows-server.md)
>
>

<span data-ttu-id="fe29d-106">本文說明如何 toorecover 資料從備份保存庫，並將它還原 tooa 伺服器或電腦。</span><span class="sxs-lookup"><span data-stu-id="fe29d-106">This article explains how toorecover data from a backup vault and restore it tooa server or computer.</span></span> <span data-ttu-id="fe29d-107">自 2017 年 3 月開始，您可以再建立備份保存庫 hello 傳統入口網站中。</span><span class="sxs-lookup"><span data-stu-id="fe29d-107">Starting in March 2017, you can no longer create backup vaults in hello classic portal.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fe29d-108">您現在可以升級您備份保存庫 tooRecovery 服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="fe29d-108">You can now upgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="fe29d-109">如需詳細資訊，請參閱 hello 文章[升級復原服務保存庫備份保存庫 tooa](backup-azure-upgrade-backup-to-recovery-services.md)。</span><span class="sxs-lookup"><span data-stu-id="fe29d-109">For details, see hello article [Upgrade a Backup vault tooa Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="fe29d-110">Microsoft 會鼓勵 tooupgrade 您備份保存庫 tooRecovery 服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="fe29d-110">Microsoft encourages you tooupgrade your Backup vaults tooRecovery Services vaults.</span></span><br/> <span data-ttu-id="fe29d-111">**2017 年 10 月 15，**，您將不再能夠 toouse PowerShell toocreate 備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="fe29d-111">**October 15, 2017**, you will no longer be able toouse PowerShell toocreate Backup vaults.</span></span> <br/> <span data-ttu-id="fe29d-112">**自 2017 年 11 月 1 日起**：</span><span class="sxs-lookup"><span data-stu-id="fe29d-112">**Starting November 1, 2017**:</span></span>
>- <span data-ttu-id="fe29d-113">任何其餘的備份保存庫會自動升級的 tooRecovery 服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="fe29d-113">Any remaining Backup vaults will be automatically upgraded tooRecovery Services vaults.</span></span>
>- <span data-ttu-id="fe29d-114">您將無法 tooaccess hello 傳統入口網站中無法備份資料。</span><span class="sxs-lookup"><span data-stu-id="fe29d-114">You won't be able tooaccess your backup data in hello classic portal.</span></span> <span data-ttu-id="fe29d-115">相反地，使用 Azure 入口網站 tooaccess hello 備份資料復原服務保存庫中。</span><span class="sxs-lookup"><span data-stu-id="fe29d-115">Instead, use hello Azure portal tooaccess your backup data in Recovery Services vaults.</span></span>
>

<span data-ttu-id="fe29d-116">toorestore 資料，您會使用 hello 復原資料精靈在 hello Microsoft Azure 復原服務 」 (MARS) 代理程式。</span><span class="sxs-lookup"><span data-stu-id="fe29d-116">toorestore data, you use hello Recover Data wizard in hello Microsoft Azure Recovery Services (MARS) agent.</span></span> <span data-ttu-id="fe29d-117">當您還原資料時，您可以︰</span><span class="sxs-lookup"><span data-stu-id="fe29d-117">When you restore data, it is possible to:</span></span>

* <span data-ttu-id="fe29d-118">相同電腦中的 hello 備份還原資料 toohello 拍攝。</span><span class="sxs-lookup"><span data-stu-id="fe29d-118">Restore data toohello same machine from which hello backups were taken.</span></span>
* <span data-ttu-id="fe29d-119">還原資料 tooan 其他機器。</span><span class="sxs-lookup"><span data-stu-id="fe29d-119">Restore data tooan alternate machine.</span></span>

<span data-ttu-id="fe29d-120">年 1 月 2017，Microsoft 發行預覽更新 toohello MARS 代理程式。</span><span class="sxs-lookup"><span data-stu-id="fe29d-120">In January 2017, Microsoft released a Preview update toohello MARS agent.</span></span> <span data-ttu-id="fe29d-121">Bug 修正，以及這項更新啟用立即還原，可讓您 toomount 可寫入的復原點快照集以復原磁碟區。</span><span class="sxs-lookup"><span data-stu-id="fe29d-121">Along with bug fixes, this update enables Instant Restore, which allows you toomount a writeable recovery point snapshot as a recovery volume.</span></span> <span data-ttu-id="fe29d-122">然後，您可以瀏覽 hello 復原磁碟區並將複製檔案 tooa 本機電腦藉此選擇性地還原檔案。</span><span class="sxs-lookup"><span data-stu-id="fe29d-122">You can then explore hello recovery volume and copy files tooa local computer thereby selectively restoring files.</span></span>

> [!NOTE]
> <span data-ttu-id="fe29d-123">hello [2017 年 1 月更新 Azure Backup](https://support.microsoft.com/en-us/help/3216528?preview)如果您想要立即還原 toorestore 資料 toouse，則需要。</span><span class="sxs-lookup"><span data-stu-id="fe29d-123">hello [January 2017 Azure Backup update](https://support.microsoft.com/en-us/help/3216528?preview) is required if you want toouse Instant Restore toorestore data.</span></span> <span data-ttu-id="fe29d-124">也在保存庫在 hello 技術支援文件中所列的地區設定必須加以保護 hello 備份資料。</span><span class="sxs-lookup"><span data-stu-id="fe29d-124">Also hello backup data must be protected in vaults in locales listed in hello support article.</span></span> <span data-ttu-id="fe29d-125">請參閱 hello [2017 年 1 月更新 Azure Backup](https://support.microsoft.com/en-us/help/3216528?preview) hello 支援 立即還原的地區設定的最新的清單。</span><span class="sxs-lookup"><span data-stu-id="fe29d-125">Consult hello [January 2017 Azure Backup update](https://support.microsoft.com/en-us/help/3216528?preview) for hello latest list of locales that support Instant Restore.</span></span> <span data-ttu-id="fe29d-126">「立即還原」目前**無法**在所有地區設定中使用。</span><span class="sxs-lookup"><span data-stu-id="fe29d-126">Instant Restore is **not** currently available in all locales.</span></span>
>

<span data-ttu-id="fe29d-127">立即還原適用於在 hello Azure 入口網站中的 復原服務保存庫中使用與備份保存庫 hello 傳統入口網站中。</span><span class="sxs-lookup"><span data-stu-id="fe29d-127">Instant Restore is available for use in Recovery Services vaults in hello Azure portal and Backup vaults in hello classic portal.</span></span> <span data-ttu-id="fe29d-128">如果您想 toouse 立即還原，下載 hello MARS 更新，並遵循提到立即還原 hello 程序。</span><span class="sxs-lookup"><span data-stu-id="fe29d-128">If you want toouse Instant Restore, download hello MARS update, and follow hello procedures that mention Instant Restore.</span></span>


## <a name="use-instant-restore-toorecover-data-toohello-same-machine"></a><span data-ttu-id="fe29d-129">使用 立即還原 toorecover 資料 toohello 同一部電腦</span><span class="sxs-lookup"><span data-stu-id="fe29d-129">Use Instant Restore toorecover data toohello same machine</span></span>

<span data-ttu-id="fe29d-130">如果您不小心刪除了檔案，並且想 toorestore 它 toohello 同一部電腦 （從哪些 hello 備份），hello 下列步驟將協助您復原 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="fe29d-130">If you accidentally deleted a file and wish toorestore it toohello same machine (from which hello backup is taken), hello following steps will help you recover hello data.</span></span>

1. <span data-ttu-id="fe29d-131">開啟 hello **Microsoft Azure 備份**中對齊。</span><span class="sxs-lookup"><span data-stu-id="fe29d-131">Open hello **Microsoft Azure Backup** snap in.</span></span> <span data-ttu-id="fe29d-132">如果您不知道 hello 嵌入式管理單元安裝所在，搜尋 hello 電腦或伺服器**Microsoft Azure 備份**。</span><span class="sxs-lookup"><span data-stu-id="fe29d-132">If you don't know where hello snap in was installed, search hello computer or server for **Microsoft Azure Backup**.</span></span>

    <span data-ttu-id="fe29d-133">hello 桌面應用程式應該會出現在 hello 搜尋結果中。</span><span class="sxs-lookup"><span data-stu-id="fe29d-133">hello desktop app should appear in hello search results.</span></span>

2. <span data-ttu-id="fe29d-134">按一下**復原資料**toostart hello 精靈。</span><span class="sxs-lookup"><span data-stu-id="fe29d-134">Click **Recover Data** toostart hello wizard.</span></span>

    ![復原資料](./media/backup-azure-restore-windows-server/recover.png)

3. <span data-ttu-id="fe29d-136">Hello 上**入門**窗格中，toorestore hello 資料 toohello 相同伺服器或電腦上，選取**這部伺服器 (`<server name>`)**按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="fe29d-136">On hello **Getting Started** pane, toorestore hello data toohello same server or computer, select **This server (`<server name>`)** and click **Next**.</span></span>

    ![選擇此伺服器選項 toorestore hello 資料 toohello 同一部電腦](./media/backup-azure-restore-windows-server/samemachine_gettingstarted_instantrestore.png)

4. <span data-ttu-id="fe29d-138">在 hello**選取復原模式** 窗格中，選擇**個別檔案及資料夾**，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="fe29d-138">On hello **Select Recovery Mode** pane, choose **Individual files and folders** and then click **Next**.</span></span>

    ![瀏覽檔案](./media/backup-azure-restore-windows-server/samemachine_selectrecoverymode_instantrestore.png)

5. <span data-ttu-id="fe29d-140">在 hello**選取磁碟區和日期**窗格中，選取 hello 磁碟區，其中包含 hello 檔案及/或您想要 toorestore 的資料夾。</span><span class="sxs-lookup"><span data-stu-id="fe29d-140">On hello **Select Volume and Date** pane, select hello volume that contains hello files and/or folders you want toorestore.</span></span>

    <span data-ttu-id="fe29d-141">Hello 日曆上選取的復原點。</span><span class="sxs-lookup"><span data-stu-id="fe29d-141">On hello calendar, select a recovery point.</span></span> <span data-ttu-id="fe29d-142">您可以從任何時間的復原點還原。</span><span class="sxs-lookup"><span data-stu-id="fe29d-142">You can restore from any recovery point in time.</span></span> <span data-ttu-id="fe29d-143">日期**粗體**表示 hello 至少一個復原點的可用性。</span><span class="sxs-lookup"><span data-stu-id="fe29d-143">Dates in **bold** indicate hello availability of at least one recovery point.</span></span> <span data-ttu-id="fe29d-144">一旦您選取日期，如果有多個復原點可用，請選擇 hello 特定的復原點從 hello**時間**下拉式功能表。</span><span class="sxs-lookup"><span data-stu-id="fe29d-144">Once you select a date, if multiple recovery points are available, choose hello specific recovery point from hello **Time** drop-down menu.</span></span>

    ![磁碟區和日期](./media/backup-azure-restore-windows-server/samemachine_selectvolumedate_instantrestore.png)

6. <span data-ttu-id="fe29d-146">一旦您已選擇 hello 復原點 toorestore，按一下 **掛接**。</span><span class="sxs-lookup"><span data-stu-id="fe29d-146">Once you have chosen hello recovery point toorestore, click **Mount**.</span></span>

    <span data-ttu-id="fe29d-147">Azure 備份掛接 hello 本機復原點，並使用它做為復原磁碟區。</span><span class="sxs-lookup"><span data-stu-id="fe29d-147">Azure Backup mounts hello local recovery point, and uses it as a recovery volume.</span></span>

7. <span data-ttu-id="fe29d-148">在 hello**瀏覽和復原檔案** 窗格中，按一下 **瀏覽**想 tooopen Windows 檔案總管 並尋找 hello 檔案及資料夾。</span><span class="sxs-lookup"><span data-stu-id="fe29d-148">On hello **Browse and Recover Files** pane, click **Browse** tooopen Windows Explorer and find hello files and folders you want.</span></span>

    ![修復選項](./media/backup-azure-restore-windows-server/samemachine_browserecover_instantrestore.png)


8. <span data-ttu-id="fe29d-150">在 Windows 檔案總管 中，複製 hello 檔案及/或資料夾想 toorestore，並將它們貼 tooany 位置 toohello 本機伺服器或電腦。</span><span class="sxs-lookup"><span data-stu-id="fe29d-150">In Windows Explorer, copy hello files and/or folders you want toorestore and paste them tooany location local toohello server or computer.</span></span> <span data-ttu-id="fe29d-151">您可以開啟或資料流 hello 檔案直接從 hello 復原磁碟區，並確認 hello 正確版本會復原。</span><span class="sxs-lookup"><span data-stu-id="fe29d-151">You can open or stream hello files directly from hello recovery volume and verify hello correct versions are recovered.</span></span>

    ![複製並貼上檔案和資料夾從掛接的磁碟區 toolocal 位置](./media/backup-azure-restore-windows-server/samemachine_copy_instantrestore.png)

9. <span data-ttu-id="fe29d-153">完成還原 hello 檔案及/或資料夾，在 hello**瀏覽和修復檔案** 窗格中，按一下 **卸載**。</span><span class="sxs-lookup"><span data-stu-id="fe29d-153">When you are finished restoring hello files and/or folders, on hello **Browse and Recovery Files** pane, click **Unmount**.</span></span> <span data-ttu-id="fe29d-154">然後按一下 **是**tooconfirm 想 toounmount hello 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="fe29d-154">Then click **Yes** tooconfirm that you want toounmount hello volume.</span></span>

    ![取消掛接 hello 磁碟區，並確認](./media/backup-azure-restore-windows-server/samemachine_unmount_instantrestore.png)

    > [!Important]
    > <span data-ttu-id="fe29d-156">如果您沒有按一下 取消掛接，hello 復原磁碟區會保持已掛接六個小時，從 hello 裝載時的時間。</span><span class="sxs-lookup"><span data-stu-id="fe29d-156">If you do not click Unmount, hello Recovery Volume will remain mounted for six hours from hello time when it was mounted.</span></span> <span data-ttu-id="fe29d-157">掛上 hello 磁碟區時，將會不執行任何備份作業。</span><span class="sxs-lookup"><span data-stu-id="fe29d-157">No backup operations will run while hello volume is mounted.</span></span> <span data-ttu-id="fe29d-158">Hello 復原磁碟區未裝載任何的排程備份作業 toorun 期間 hello 當 hello 掛上磁碟區，會執行。</span><span class="sxs-lookup"><span data-stu-id="fe29d-158">Any backup operation scheduled toorun during hello time when hello volume is mounted, will run after hello recovery volume is unmounted.</span></span>
    >


## <a name="recover-data-toohello-same-machine"></a><span data-ttu-id="fe29d-159">復原資料 toohello 同一部電腦</span><span class="sxs-lookup"><span data-stu-id="fe29d-159">Recover data toohello same machine</span></span>
<span data-ttu-id="fe29d-160">如果您不小心刪除了檔案，並且想 toorestore 它 toohello 同一部電腦 （從哪些 hello 備份），hello 下列步驟將協助您復原 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="fe29d-160">If you accidentally deleted a file and wish toorestore it toohello same machine (from which hello backup is taken), hello following steps will help you recover hello data.</span></span>

1. <span data-ttu-id="fe29d-161">開啟 hello **Microsoft Azure 備份**中對齊。</span><span class="sxs-lookup"><span data-stu-id="fe29d-161">Open hello **Microsoft Azure Backup** snap in.</span></span>
2. <span data-ttu-id="fe29d-162">按一下**復原資料**tooinitiate hello 工作流程。</span><span class="sxs-lookup"><span data-stu-id="fe29d-162">Click **Recover Data** tooinitiate hello workflow.</span></span>

    ![復原資料](./media/backup-azure-restore-windows-server-classic/recover.png)
3. <span data-ttu-id="fe29d-164">選取 hello **這部伺服器 (*yourmachinename*) * * 選項 toorestore hello 備份上 hello 檔案相同的電腦。</span><span class="sxs-lookup"><span data-stu-id="fe29d-164">Select hello **This server (*yourmachinename*)** option toorestore hello backed up file on hello same machine.</span></span>

    ![相同電腦](./media/backup-azure-restore-windows-server-classic/samemachine.png)
4. <span data-ttu-id="fe29d-166">選擇太**瀏覽檔案**或**搜尋檔案**。</span><span class="sxs-lookup"><span data-stu-id="fe29d-166">Choose too**Browse for files** or **Search for files**.</span></span>

    <span data-ttu-id="fe29d-167">如果，保留單元 hello 預設選項您計劃 toorestore 已知其路徑的一個或多個檔案。</span><span class="sxs-lookup"><span data-stu-id="fe29d-167">Leave hello default option if you plan toorestore one or more files whose path is known.</span></span> <span data-ttu-id="fe29d-168">如果您不確定 hello 資料夾結構，但希望 toosearch 檔案，挑選 hello**搜尋檔案**選項。</span><span class="sxs-lookup"><span data-stu-id="fe29d-168">If you are not sure about hello folder structure but would like toosearch for a file, pick hello **Search for files** option.</span></span> <span data-ttu-id="fe29d-169">為了 hello 這一節，我們將繼續使用 hello 預設選項。</span><span class="sxs-lookup"><span data-stu-id="fe29d-169">For hello purpose of this section, we will proceed with hello default option.</span></span>

    ![瀏覽檔案](./media/backup-azure-restore-windows-server-classic/browseandsearch.png)
5. <span data-ttu-id="fe29d-171">選取您想要從中 toorestore hello 檔案 hello 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="fe29d-171">Select hello volume from which you wish toorestore hello file.</span></span>

    <span data-ttu-id="fe29d-172">您可以從任何時間點還原。</span><span class="sxs-lookup"><span data-stu-id="fe29d-172">You can restore from any point in time.</span></span> <span data-ttu-id="fe29d-173">它會出現在日期**粗體**hello 月曆控制項中指出的還原點的 hello 可用性。</span><span class="sxs-lookup"><span data-stu-id="fe29d-173">Dates which appear in **bold** in hello calendar control indicate hello availability of a restore point.</span></span> <span data-ttu-id="fe29d-174">一旦選取日期之後，根據您的備份排程 （和 hello 成功備份作業的），您可以選取的時間點從 hello**時間**下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="fe29d-174">Once a date is selected, based on your backup schedule (and hello success of a backup operation), you can select a point in time from hello **Time** drop down.</span></span>

    ![磁碟區和日期](./media/backup-azure-restore-windows-server-classic/volanddate.png)
6. <span data-ttu-id="fe29d-176">選取 hello 項目 toorecover。</span><span class="sxs-lookup"><span data-stu-id="fe29d-176">Select hello items toorecover.</span></span> <span data-ttu-id="fe29d-177">您可以將多選資料夾/檔案想 toorestore。</span><span class="sxs-lookup"><span data-stu-id="fe29d-177">You can multi-select folders/files you wish toorestore.</span></span>

    ![選取檔案](./media/backup-azure-restore-windows-server-classic/selectfiles.png)
7. <span data-ttu-id="fe29d-179">指定 hello 復原參數。</span><span class="sxs-lookup"><span data-stu-id="fe29d-179">Specify hello recovery parameters.</span></span>

    ![修復選項](./media/backup-azure-restore-windows-server-classic/recoveroptions.png)

   * <span data-ttu-id="fe29d-181">您可以選擇還原 toohello （中的 hello 檔案/資料夾可能會被覆寫） 的原始位置] 或 [hello tooanother 位置的同一部電腦。</span><span class="sxs-lookup"><span data-stu-id="fe29d-181">You have an option of restoring toohello original location (in which hello file/folder would be overwritten) or tooanother location in hello same machine.</span></span>
   * <span data-ttu-id="fe29d-182">如果 hello 檔案/資料夾，您想 toorestore 存在於 hello 目標位置，您可以建立複本 (hello 的兩個版本相同的檔案)、 覆寫 hello 檔案在 hello 目標位置，或略過的 hello 檔案存在 hello 目標中的 hello 復原。</span><span class="sxs-lookup"><span data-stu-id="fe29d-182">If hello file/folder you wish toorestore exists in hello target location, you can create copies (two versions of hello same file), overwrite hello files in hello target location, or skip hello recovery of hello files which exist in hello target.</span></span>
   * <span data-ttu-id="fe29d-183">強烈建議您保持還原 hello hello 復原的檔案 Acl 的 hello 預設選項。</span><span class="sxs-lookup"><span data-stu-id="fe29d-183">It is highly recommended that you leave hello default option of restoring hello ACLs on hello files which are being recovered.</span></span>
8. <span data-ttu-id="fe29d-184">提供這些輸入之後，按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="fe29d-184">Once these inputs are provided, click **Next**.</span></span> <span data-ttu-id="fe29d-185">hello 復原工作流程，後者還原 hello 檔案 toothis 機器，就會開始。</span><span class="sxs-lookup"><span data-stu-id="fe29d-185">hello recovery workflow, which restores hello files toothis machine, will begin.</span></span>

## <a name="recover-tooan-alternate-machine"></a><span data-ttu-id="fe29d-186">Tooan 替代機器復原</span><span class="sxs-lookup"><span data-stu-id="fe29d-186">Recover tooan alternate machine</span></span>
<span data-ttu-id="fe29d-187">整個伺服器遺失時，您仍然可以從 Azure Backup tooa 不同電腦中復原資料。</span><span class="sxs-lookup"><span data-stu-id="fe29d-187">If your entire server is lost, you can still recover data from Azure Backup tooa different machine.</span></span> <span data-ttu-id="fe29d-188">hello 下列步驟說明 hello 工作流程。</span><span class="sxs-lookup"><span data-stu-id="fe29d-188">hello following steps illustrate hello workflow.</span></span>  

<span data-ttu-id="fe29d-189">包含下列步驟中所使用的 hello 術語：</span><span class="sxs-lookup"><span data-stu-id="fe29d-189">hello terminology used in these steps includes:</span></span>

* <span data-ttu-id="fe29d-190">*來源機器*– 拍攝 hello 從哪個 hello 備份的原始電腦，這是目前無法使用。</span><span class="sxs-lookup"><span data-stu-id="fe29d-190">*Source machine* – hello original machine from which hello backup was taken and which is currently unavailable.</span></span>
* <span data-ttu-id="fe29d-191">*目標電腦*– hello 機器 toowhich hello 資料要復原的目的地。</span><span class="sxs-lookup"><span data-stu-id="fe29d-191">*Target machine* – hello machine toowhich hello data is being recovered.</span></span>
* <span data-ttu-id="fe29d-192">*範例保存庫*– hello 備份保存庫 toowhich hello*來源機器*和*目標機器*註冊。</span><span class="sxs-lookup"><span data-stu-id="fe29d-192">*Sample vault* – hello Backup vault toowhich hello *Source machine* and *Target machine* are registered.</span></span> <br/>

> [!NOTE]
> <span data-ttu-id="fe29d-193">從機器的備份無法還原在執行舊版的 hello 作業系統的電腦上。</span><span class="sxs-lookup"><span data-stu-id="fe29d-193">Backups taken from a machine cannot be restored on a machine which is running an earlier version of hello operating system.</span></span> <span data-ttu-id="fe29d-194">例如，如果從 Windows 7 電腦進行備份，則可以在 Windows 8 或更新版電腦上進行還原。</span><span class="sxs-lookup"><span data-stu-id="fe29d-194">For example, if backups are taken from a Windows 7 machine, it can be restored on a Windows 8 or above machine.</span></span> <span data-ttu-id="fe29d-195">不過，hello 反之亦然並未維持 true。</span><span class="sxs-lookup"><span data-stu-id="fe29d-195">However, hello vice-versa does not hold true.</span></span>
>
>

1. <span data-ttu-id="fe29d-196">開啟 hello **Microsoft Azure 備份**在 hello 上對齊*目標機器*。</span><span class="sxs-lookup"><span data-stu-id="fe29d-196">Open hello **Microsoft Azure Backup** snap in on hello *Target machine*.</span></span>
2. <span data-ttu-id="fe29d-197">請確定該 hello*目標電腦*和 hello*來源機器*是已註冊的 toohello 相同的備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="fe29d-197">Ensure that hello *Target machine* and hello *Source machine* are registered toohello same backup vault.</span></span>
3. <span data-ttu-id="fe29d-198">按一下**復原資料**tooinitiate hello 工作流程。</span><span class="sxs-lookup"><span data-stu-id="fe29d-198">Click **Recover Data** tooinitiate hello workflow.</span></span>

    ![復原資料](./media/backup-azure-restore-windows-server-classic/recover.png)
4. <span data-ttu-id="fe29d-200">選取 [其他伺服器] </span><span class="sxs-lookup"><span data-stu-id="fe29d-200">Select **Another server**</span></span>

    ![其他伺服器](./media/backup-azure-restore-windows-server-classic/anotherserver.png)
5. <span data-ttu-id="fe29d-202">提供對應 toohello hello 保存庫認證檔案*範例保存庫*。</span><span class="sxs-lookup"><span data-stu-id="fe29d-202">Provide hello vault credential file that corresponds toohello *Sample vault*.</span></span> <span data-ttu-id="fe29d-203">如果 hello 保存庫認證檔案無效 （或已過期） 下載新的保存庫認證檔案從 hello*範例保存庫*hello Azure 傳統入口網站中。</span><span class="sxs-lookup"><span data-stu-id="fe29d-203">If hello vault credential file is invalid (or expired) download a new vault credential file from hello *Sample vault* in hello Azure classic portal.</span></span> <span data-ttu-id="fe29d-204">一旦提供 hello 保存庫認證檔案，則會顯示 hello 針對 hello 保存庫認證檔案的備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="fe29d-204">Once hello vault credential file is provided, hello backup vault against hello vault credential file is displayed.</span></span>
6. <span data-ttu-id="fe29d-205">選取 hello*來源機器*從 hello 顯示的電腦清單。</span><span class="sxs-lookup"><span data-stu-id="fe29d-205">Select hello *Source machine* from hello list of displayed machines.</span></span>

    ![電腦清單](./media/backup-azure-restore-windows-server-classic/machinelist.png)
7. <span data-ttu-id="fe29d-207">選取任一 hello**搜尋檔案**或**瀏覽檔案**選項。</span><span class="sxs-lookup"><span data-stu-id="fe29d-207">Select either hello **Search for files** or **Browse for files** option.</span></span> <span data-ttu-id="fe29d-208">本節 hello 目的，我們將使用 hello**搜尋檔案**選項。</span><span class="sxs-lookup"><span data-stu-id="fe29d-208">For hello purpose of this section, we will use hello **Search for files** option.</span></span>

    ![搜尋](./media/backup-azure-restore-windows-server-classic/search.png)
8. <span data-ttu-id="fe29d-210">Hello 下一個畫面中，選取 hello 磁碟區和日期。</span><span class="sxs-lookup"><span data-stu-id="fe29d-210">Select hello volume and date in hello next screen.</span></span> <span data-ttu-id="fe29d-211">搜尋您想 toorestore hello 資料夾/檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="fe29d-211">Search for hello folder/file name you want toorestore.</span></span>

    ![搜尋項目](./media/backup-azure-restore-windows-server-classic/searchitems.png)
9. <span data-ttu-id="fe29d-213">選取需要 hello 檔案還原 toobe hello 位置。</span><span class="sxs-lookup"><span data-stu-id="fe29d-213">Select hello location where hello files need toobe restored.</span></span>

    ![還原位置](./media/backup-azure-restore-windows-server-classic/restorelocation.png)
10. <span data-ttu-id="fe29d-215">提供在過程中提供的 hello 加密複雜密碼*來源機器*註冊太*範例保存庫*。</span><span class="sxs-lookup"><span data-stu-id="fe29d-215">Provide hello encryption passphrase that was provided during *Source machine’s* registration too*Sample vault*.</span></span>

    ![加密](./media/backup-azure-restore-windows-server-classic/encryption.png)
11. <span data-ttu-id="fe29d-217">一旦提供 hello 輸入，按一下 **復原**，此觸發程序 hello hello 檔案 toohello 目的地提供備份的還原。</span><span class="sxs-lookup"><span data-stu-id="fe29d-217">Once hello input is provided, click **Recover**, which triggers hello restore of hello backed up files toohello destination provided.</span></span>

## <a name="use-instant-restore-toorestore-data-tooan-alternate-machine"></a><span data-ttu-id="fe29d-218">使用 立即還原 toorestore 資料 tooan 替代機器</span><span class="sxs-lookup"><span data-stu-id="fe29d-218">Use Instant Restore toorestore data tooan alternate machine</span></span>
<span data-ttu-id="fe29d-219">整個伺服器遺失時，您仍然可以從 Azure Backup tooa 不同電腦中復原資料。</span><span class="sxs-lookup"><span data-stu-id="fe29d-219">If your entire server is lost, you can still recover data from Azure Backup tooa different machine.</span></span> <span data-ttu-id="fe29d-220">hello 下列步驟說明 hello 工作流程。</span><span class="sxs-lookup"><span data-stu-id="fe29d-220">hello following steps illustrate hello workflow.</span></span>

<span data-ttu-id="fe29d-221">包含下列步驟中所使用的 hello 術語：</span><span class="sxs-lookup"><span data-stu-id="fe29d-221">hello terminology used in these steps includes:</span></span>

* <span data-ttu-id="fe29d-222">*來源機器*– 拍攝 hello 從哪個 hello 備份的原始電腦，這是目前無法使用。</span><span class="sxs-lookup"><span data-stu-id="fe29d-222">*Source machine* – hello original machine from which hello backup was taken and which is currently unavailable.</span></span>
* <span data-ttu-id="fe29d-223">*目標電腦*– hello 機器 toowhich hello 資料要復原的目的地。</span><span class="sxs-lookup"><span data-stu-id="fe29d-223">*Target machine* – hello machine toowhich hello data is being recovered.</span></span>
* <span data-ttu-id="fe29d-224">*範例保存庫*– hello 復原服務保存庫 toowhich hello*來源機器*和*目標機器*註冊。</span><span class="sxs-lookup"><span data-stu-id="fe29d-224">*Sample vault* – hello Recovery Services vault toowhich hello *Source machine* and *Target machine* are registered.</span></span> <br/>

> [!NOTE]
> <span data-ttu-id="fe29d-225">備份無法還原的 tooa 目標電腦執行舊版的 hello 作業系統。</span><span class="sxs-lookup"><span data-stu-id="fe29d-225">Backups can't be restored tooa target machine running an earlier version of hello operating system.</span></span> <span data-ttu-id="fe29d-226">例如，從 Windows 7 電腦建立的備份可以還原至 Windows 8 或更新版本的電腦。</span><span class="sxs-lookup"><span data-stu-id="fe29d-226">For example, a backup taken from a Windows 7 computer can be restored on a Windows 8, or later, computer.</span></span> <span data-ttu-id="fe29d-227">執行 Windows 8 電腦的備份無法還原的 tooa Windows 7 電腦。</span><span class="sxs-lookup"><span data-stu-id="fe29d-227">A backup taken from a Windows 8 computer cannot be restored tooa Windows 7 computer.</span></span>
>
>

1. <span data-ttu-id="fe29d-228">開啟 hello **Microsoft Azure 備份**在 hello 上對齊*目標機器*。</span><span class="sxs-lookup"><span data-stu-id="fe29d-228">Open hello **Microsoft Azure Backup** snap in on hello *Target machine*.</span></span>

2. <span data-ttu-id="fe29d-229">請確定 hello*目標電腦*和 hello*來源機器*是相同的復原服務保存庫註冊的 toohello。</span><span class="sxs-lookup"><span data-stu-id="fe29d-229">Ensure hello *Target machine* and hello *Source machine* are registered toohello same Recovery Services vault.</span></span>

3. <span data-ttu-id="fe29d-230">按一下**復原資料**tooopen hello**復原資料精靈**。</span><span class="sxs-lookup"><span data-stu-id="fe29d-230">Click **Recover Data** tooopen hello **Recover Data wizard**.</span></span>

    ![復原資料](./media/backup-azure-restore-windows-server/recover.png)

4. <span data-ttu-id="fe29d-232">在 hello**入門**窗格中，選取**另一部伺服器**</span><span class="sxs-lookup"><span data-stu-id="fe29d-232">On hello **Getting Started** pane, select **Another server**</span></span>

    ![其他伺服器](./media/backup-azure-restore-windows-server/alternatemachine_gettingstarted_instantrestore.png)

5. <span data-ttu-id="fe29d-234">提供對應 toohello hello 保存庫認證檔案*範例保存庫*，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="fe29d-234">Provide hello vault credential file that corresponds toohello *Sample vault*, and click **Next**.</span></span>

    <span data-ttu-id="fe29d-235">如果 hello 保存庫認證檔案無效 （或已過期），下載新的保存庫認證檔案從 hello*範例保存庫*hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="fe29d-235">If hello vault credential file is invalid (or expired), download a new vault credential file from hello *Sample vault* in hello Azure portal.</span></span> <span data-ttu-id="fe29d-236">一旦您提供有效的保存庫認證，hello 的 hello 對應的備份保存庫會出現的名稱。</span><span class="sxs-lookup"><span data-stu-id="fe29d-236">Once you provide a valid vault credential, hello name of hello corresponding Backup Vault appears.</span></span>

6. <span data-ttu-id="fe29d-237">在 hello**選取備份伺服器**窗格中，選取 hello*來源機器*從 hello 清單中顯示的機器，並提供 hello 複雜密碼。</span><span class="sxs-lookup"><span data-stu-id="fe29d-237">On hello **Select Backup Server** pane, select hello *Source machine* from hello list of displayed machines and provide hello passphrase.</span></span> <span data-ttu-id="fe29d-238">然後按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="fe29d-238">Then click **Next**.</span></span>

    ![電腦清單](./media/backup-azure-restore-windows-server/alternatemachine_selectmachine_instantrestore.png)

7. <span data-ttu-id="fe29d-240">在 hello**選取復原模式**窗格中，選取**個別檔案及資料夾**按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="fe29d-240">On hello **Select Recovery Mode** pane, select **Individual files and folders** and click **Next**.</span></span>

    ![搜尋](./media/backup-azure-restore-windows-server/alternatemachine_selectrecoverymode_instantrestore.png)

8. <span data-ttu-id="fe29d-242">在 hello**選取磁碟區和日期**窗格中，選取 hello 磁碟區，其中包含 hello 檔案及/或您想要 toorestore 的資料夾。</span><span class="sxs-lookup"><span data-stu-id="fe29d-242">On hello **Select Volume and Date** pane, select hello volume that contains hello files and/or folders you want toorestore.</span></span>

    <span data-ttu-id="fe29d-243">Hello 日曆上選取的復原點。</span><span class="sxs-lookup"><span data-stu-id="fe29d-243">On hello calendar, select a recovery point.</span></span> <span data-ttu-id="fe29d-244">您可以從任何時間的復原點還原。</span><span class="sxs-lookup"><span data-stu-id="fe29d-244">You can restore from any recovery point in time.</span></span> <span data-ttu-id="fe29d-245">日期**粗體**表示 hello 至少一個復原點的可用性。</span><span class="sxs-lookup"><span data-stu-id="fe29d-245">Dates in **bold** indicate hello availability of at least one recovery point.</span></span> <span data-ttu-id="fe29d-246">一旦您選取日期，如果有多個復原點可用，請選擇 hello 特定的復原點從 hello**時間**下拉式功能表。</span><span class="sxs-lookup"><span data-stu-id="fe29d-246">Once you select a date, if multiple recovery points are available, choose hello specific recovery point from hello **Time** drop-down menu.</span></span>

    ![搜尋項目](./media/backup-azure-restore-windows-server/alternatemachine_selectvolumedate_instantrestore.png)

9. <span data-ttu-id="fe29d-248">按一下**掛接**toolocally 掛接 hello 復原點復原磁碟區上為您*目標機器*。</span><span class="sxs-lookup"><span data-stu-id="fe29d-248">Click **Mount** toolocally mount hello recovery point as a recovery volume on your *Target machine*.</span></span>

10. <span data-ttu-id="fe29d-249">在 hello**瀏覽和復原檔案** 窗格中，按一下 **瀏覽**想 tooopen Windows 檔案總管 並尋找 hello 檔案及資料夾。</span><span class="sxs-lookup"><span data-stu-id="fe29d-249">On hello **Browse and Recover Files** pane, click **Browse** tooopen Windows Explorer and find hello files and folders you want.</span></span>

    ![加密](./media/backup-azure-restore-windows-server/alternatemachine_browserecover_instantrestore.png)

11. <span data-ttu-id="fe29d-251">在 Windows 檔案總管中，將複製 hello 檔案及/或資料夾從 hello 復原磁碟區並貼 tooyour*目標機器*位置。</span><span class="sxs-lookup"><span data-stu-id="fe29d-251">In Windows Explorer, copy hello files and/or folders from hello recovery volume and paste them tooyour *Target machine* location.</span></span> <span data-ttu-id="fe29d-252">您可以開啟或資料流 hello 檔案直接從 hello 復原磁碟區，並確認 hello 正確版本會復原。</span><span class="sxs-lookup"><span data-stu-id="fe29d-252">You can open or stream hello files directly from hello recovery volume and verify hello correct versions are recovered.</span></span>

    ![加密](./media/backup-azure-restore-windows-server/alternatemachine_copy_instantrestore.png)

12. <span data-ttu-id="fe29d-254">完成還原 hello 檔案及/或資料夾，在 hello**瀏覽和修復檔案** 窗格中，按一下 **卸載**。</span><span class="sxs-lookup"><span data-stu-id="fe29d-254">When you are finished restoring hello files and/or folders, on hello **Browse and Recovery Files** pane, click **Unmount**.</span></span> <span data-ttu-id="fe29d-255">然後按一下 **是**tooconfirm 想 toounmount hello 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="fe29d-255">Then click **Yes** tooconfirm that you want toounmount hello volume.</span></span>

    ![加密](./media/backup-azure-restore-windows-server/alternatemachine_unmount_instantrestore.png)

    > [!Important]
    > <span data-ttu-id="fe29d-257">如果您沒有按一下 取消掛接，hello 復原磁碟區會保持已掛接六個小時，從 hello 裝載時的時間。</span><span class="sxs-lookup"><span data-stu-id="fe29d-257">If you do not click Unmount, hello Recovery Volume will remain mounted for six hours from hello time when it was mounted.</span></span> <span data-ttu-id="fe29d-258">掛上 hello 磁碟區時，將會不執行任何備份作業。</span><span class="sxs-lookup"><span data-stu-id="fe29d-258">No backup operations will run while hello volume is mounted.</span></span> <span data-ttu-id="fe29d-259">Hello 復原磁碟區未裝載任何的排程備份作業 toorun 期間 hello 當 hello 掛上磁碟區，會執行。</span><span class="sxs-lookup"><span data-stu-id="fe29d-259">Any backup operation scheduled toorun during hello time when hello volume is mounted, will run after hello recovery volume is unmounted.</span></span>
    >


## <a name="next-steps"></a><span data-ttu-id="fe29d-260">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fe29d-260">Next steps</span></span>
* [<span data-ttu-id="fe29d-261">Azure 備份常見問題集</span><span class="sxs-lookup"><span data-stu-id="fe29d-261">Azure Backup FAQ</span></span>](backup-azure-backup-faq.md)
* <span data-ttu-id="fe29d-262">請瀏覽 hello [Azure 備份論壇](http://go.microsoft.com/fwlink/p/?LinkId=290933)。</span><span class="sxs-lookup"><span data-stu-id="fe29d-262">Visit hello [Azure Backup Forum](http://go.microsoft.com/fwlink/p/?LinkId=290933).</span></span>

## <a name="learn-more"></a><span data-ttu-id="fe29d-263">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="fe29d-263">Learn more</span></span>
* [<span data-ttu-id="fe29d-264">Azure 備份概觀</span><span class="sxs-lookup"><span data-stu-id="fe29d-264">Azure Backup Overview</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=222425)
* [<span data-ttu-id="fe29d-265">備份 Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="fe29d-265">Backup Azure virtual machines</span></span>](backup-azure-vms-introduction.md)
* [<span data-ttu-id="fe29d-266">備份 Microsoft 工作負載</span><span class="sxs-lookup"><span data-stu-id="fe29d-266">Backup up Microsoft workloads</span></span>](backup-azure-dpm-introduction.md)
