---
title: "使用傳統部署模型將資料從 Azure 還原到 Windows Server 或 Windows 用戶端 | Microsoft Docs"
description: "了解如何從 Windows Server 或 Windows 用戶端進行還原。"
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
ms.openlocfilehash: 300b2b17b44e21ed446fd63d572a2461e2fc1343
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="restore-files-to-a-windows-server-or-windows-client-machine-using-the-classic-deployment-model"></a><span data-ttu-id="a06f3-103">使用傳統部署模型將檔案還原到 Windows Server 或 Windows 用戶端電腦</span><span class="sxs-lookup"><span data-stu-id="a06f3-103">Restore files to a Windows server or Windows client machine using the classic deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a06f3-104">傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="a06f3-104">Classic portal</span></span>](backup-azure-restore-windows-server-classic.md)
> * [<span data-ttu-id="a06f3-105">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="a06f3-105">Azure portal</span></span>](backup-azure-restore-windows-server.md)
>
>

<span data-ttu-id="a06f3-106">本文說明如何從備份保存庫復原資料，並將資料還原到伺服器或電腦。</span><span class="sxs-lookup"><span data-stu-id="a06f3-106">This article explains how to recover data from a backup vault and restore it to a server or computer.</span></span> <span data-ttu-id="a06f3-107">從 2017 年 3 月開始，您無法再於傳統入口網站中建立備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="a06f3-107">Starting in March 2017, you can no longer create backup vaults in the classic portal.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a06f3-108">您現在可以將備份保存庫升級至復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="a06f3-108">You can now upgrade your Backup vaults to Recovery Services vaults.</span></span> <span data-ttu-id="a06f3-109">如需詳細資訊，請參閱[將備份保存庫升級至復原服務保存庫](backup-azure-upgrade-backup-to-recovery-services.md)文章。</span><span class="sxs-lookup"><span data-stu-id="a06f3-109">For details, see the article [Upgrade a Backup vault to a Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="a06f3-110">Microsoft 鼓勵您將備份保存庫升級至復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="a06f3-110">Microsoft encourages you to upgrade your Backup vaults to Recovery Services vaults.</span></span><br/> <span data-ttu-id="a06f3-111">在 **2017 年 10 月 15 日**之後，您就無法使用 PowerShell 建立備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="a06f3-111">**October 15, 2017**, you will no longer be able to use PowerShell to create Backup vaults.</span></span> <br/> <span data-ttu-id="a06f3-112">**自 2017 年 11 月 1 日起**：</span><span class="sxs-lookup"><span data-stu-id="a06f3-112">**Starting November 1, 2017**:</span></span>
>- <span data-ttu-id="a06f3-113">任何其餘的備份保存庫都會自動升級至復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="a06f3-113">Any remaining Backup vaults will be automatically upgraded to Recovery Services vaults.</span></span>
>- <span data-ttu-id="a06f3-114">您將無法在傳統入口網站中存取您的備份資料。</span><span class="sxs-lookup"><span data-stu-id="a06f3-114">You won't be able to access your backup data in the classic portal.</span></span> <span data-ttu-id="a06f3-115">相反地，使用 Azure 入口網站來存取您在復原服務保存庫中的備份資料。</span><span class="sxs-lookup"><span data-stu-id="a06f3-115">Instead, use the Azure portal to access your backup data in Recovery Services vaults.</span></span>
>

<span data-ttu-id="a06f3-116">若要還原資料，您可以使用 Microsoft Azure 復原服務 (MARS) 代理程式中的 [復原資料精靈]。</span><span class="sxs-lookup"><span data-stu-id="a06f3-116">To restore data, you use the Recover Data wizard in the Microsoft Azure Recovery Services (MARS) agent.</span></span> <span data-ttu-id="a06f3-117">當您還原資料時，您可以︰</span><span class="sxs-lookup"><span data-stu-id="a06f3-117">When you restore data, it is possible to:</span></span>

* <span data-ttu-id="a06f3-118">將資料還原到進行備份的相同電腦。</span><span class="sxs-lookup"><span data-stu-id="a06f3-118">Restore data to the same machine from which the backups were taken.</span></span>
* <span data-ttu-id="a06f3-119">將資料還原至其他電腦。</span><span class="sxs-lookup"><span data-stu-id="a06f3-119">Restore data to an alternate machine.</span></span>

<span data-ttu-id="a06f3-120">2017 年 1 月，Microsoft 推出 MARS 代理程式預覽更新。</span><span class="sxs-lookup"><span data-stu-id="a06f3-120">In January 2017, Microsoft released a Preview update to the MARS agent.</span></span> <span data-ttu-id="a06f3-121">這項更新除了錯誤修正之外，還啟用了「立即還原」，允許您掛接可寫入的復原點快照來做為復原磁碟區。</span><span class="sxs-lookup"><span data-stu-id="a06f3-121">Along with bug fixes, this update enables Instant Restore, which allows you to mount a writeable recovery point snapshot as a recovery volume.</span></span> <span data-ttu-id="a06f3-122">您接著可以探索復磁碟區並將檔案複製至本機電腦，藉此選擇性地還原檔案。</span><span class="sxs-lookup"><span data-stu-id="a06f3-122">You can then explore the recovery volume and copy files to a local computer thereby selectively restoring files.</span></span>

> [!NOTE]
> <span data-ttu-id="a06f3-123">如果您要使用「立即還原」來還原資料，必須要有 [2017 年 1 月 Azure 備份更新](https://support.microsoft.com/en-us/help/3216528?preview)。</span><span class="sxs-lookup"><span data-stu-id="a06f3-123">The [January 2017 Azure Backup update](https://support.microsoft.com/en-us/help/3216528?preview) is required if you want to use Instant Restore to restore data.</span></span> <span data-ttu-id="a06f3-124">另外，您也必須在支援文章列出之地區設定的保存庫中，保護備份資料。</span><span class="sxs-lookup"><span data-stu-id="a06f3-124">Also the backup data must be protected in vaults in locales listed in the support article.</span></span> <span data-ttu-id="a06f3-125">請參閱 [2017 年 1 月 Azure 備份更新](https://support.microsoft.com/en-us/help/3216528?preview)，了解支援「立即還原」的最新地區設定清單。</span><span class="sxs-lookup"><span data-stu-id="a06f3-125">Consult the [January 2017 Azure Backup update](https://support.microsoft.com/en-us/help/3216528?preview) for the latest list of locales that support Instant Restore.</span></span> <span data-ttu-id="a06f3-126">「立即還原」目前**無法**在所有地區設定中使用。</span><span class="sxs-lookup"><span data-stu-id="a06f3-126">Instant Restore is **not** currently available in all locales.</span></span>
>

<span data-ttu-id="a06f3-127">「立即還原」可用於 Azure 入口網站中的復原服務保存庫以及傳統入口網站中的備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="a06f3-127">Instant Restore is available for use in Recovery Services vaults in the Azure portal and Backup vaults in the classic portal.</span></span> <span data-ttu-id="a06f3-128">如果您想要使用「立即還原」，請下載 MARS 更新，並依照提及「立即還原」部分中的程序進行操作。</span><span class="sxs-lookup"><span data-stu-id="a06f3-128">If you want to use Instant Restore, download the MARS update, and follow the procedures that mention Instant Restore.</span></span>


## <a name="use-instant-restore-to-recover-data-to-the-same-machine"></a><span data-ttu-id="a06f3-129">使用「立即還原」將資料還原至同一台電腦</span><span class="sxs-lookup"><span data-stu-id="a06f3-129">Use Instant Restore to recover data to the same machine</span></span>

<span data-ttu-id="a06f3-130">如果您不小心刪除檔案，而您想要將它還原到相同的電腦 (備份進行處)，下列步驟可協助您復原資料。</span><span class="sxs-lookup"><span data-stu-id="a06f3-130">If you accidentally deleted a file and wish to restore it to the same machine (from which the backup is taken), the following steps will help you recover the data.</span></span>

1. <span data-ttu-id="a06f3-131">開啟 **Microsoft Azure 備份** 嵌入式管理單元。</span><span class="sxs-lookup"><span data-stu-id="a06f3-131">Open the **Microsoft Azure Backup** snap in.</span></span> <span data-ttu-id="a06f3-132">如果您不知道快照安裝的位置，請在電腦或伺服器上搜尋 **Microsoft Azure 備份**。</span><span class="sxs-lookup"><span data-stu-id="a06f3-132">If you don't know where the snap in was installed, search the computer or server for **Microsoft Azure Backup**.</span></span>

    <span data-ttu-id="a06f3-133">傳統型應用程式應該會出現在搜尋結果中。</span><span class="sxs-lookup"><span data-stu-id="a06f3-133">The desktop app should appear in the search results.</span></span>

2. <span data-ttu-id="a06f3-134">按一下 [復原資料] 以啟動精靈。</span><span class="sxs-lookup"><span data-stu-id="a06f3-134">Click **Recover Data** to start the wizard.</span></span>

    ![復原資料](./media/backup-azure-restore-windows-server/recover.png)

3. <span data-ttu-id="a06f3-136">在 [開始使用] 窗格中，若要將資料還原至同一台伺服器或電腦，請選取 [這台伺服器 (`<server name>`)] 並按一下 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="a06f3-136">On the **Getting Started** pane, to restore the data to the same server or computer, select **This server (`<server name>`)** and click **Next**.</span></span>

    ![選擇 [這台伺服器] 選項以將資料還原到同一台電腦](./media/backup-azure-restore-windows-server/samemachine_gettingstarted_instantrestore.png)

4. <span data-ttu-id="a06f3-138">在 [選取復原模式] 窗格上，選擇 [個別檔案與資料夾]，然後按一下 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="a06f3-138">On the **Select Recovery Mode** pane, choose **Individual files and folders** and then click **Next**.</span></span>

    ![瀏覽檔案](./media/backup-azure-restore-windows-server/samemachine_selectrecoverymode_instantrestore.png)

5. <span data-ttu-id="a06f3-140">在 [選取磁碟區和日期] 窗格上，選取包含您要還原之檔案和/或資料夾的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="a06f3-140">On the **Select Volume and Date** pane, select the volume that contains the files and/or folders you want to restore.</span></span>

    <span data-ttu-id="a06f3-141">在日曆上，選取復原點。</span><span class="sxs-lookup"><span data-stu-id="a06f3-141">On the calendar, select a recovery point.</span></span> <span data-ttu-id="a06f3-142">您可以從任何時間的復原點還原。</span><span class="sxs-lookup"><span data-stu-id="a06f3-142">You can restore from any recovery point in time.</span></span> <span data-ttu-id="a06f3-143">**粗體**的日期表示至少有一個復原點可用。</span><span class="sxs-lookup"><span data-stu-id="a06f3-143">Dates in **bold** indicate the availability of at least one recovery point.</span></span> <span data-ttu-id="a06f3-144">一旦您選取一個日期，如果有多個復原點可用，您可以從 [時間] 下拉式功能表選擇特定的復原點。</span><span class="sxs-lookup"><span data-stu-id="a06f3-144">Once you select a date, if multiple recovery points are available, choose the specific recovery point from the **Time** drop-down menu.</span></span>

    ![磁碟區和日期](./media/backup-azure-restore-windows-server/samemachine_selectvolumedate_instantrestore.png)

6. <span data-ttu-id="a06f3-146">選擇要還原的復原點之後，按一下 [掛接]。</span><span class="sxs-lookup"><span data-stu-id="a06f3-146">Once you have chosen the recovery point to restore, click **Mount**.</span></span>

    <span data-ttu-id="a06f3-147">Azure 備份會掛接本機復原點，並且使用它做為復原磁碟區。</span><span class="sxs-lookup"><span data-stu-id="a06f3-147">Azure Backup mounts the local recovery point, and uses it as a recovery volume.</span></span>

7. <span data-ttu-id="a06f3-148">在 [瀏覽及復原檔案] 窗格上，按一下 [瀏覽] 以開啟 [Windows 檔案總管]，然後尋找所需的檔案和資料夾。</span><span class="sxs-lookup"><span data-stu-id="a06f3-148">On the **Browse and Recover Files** pane, click **Browse** to open Windows Explorer and find the files and folders you want.</span></span>

    ![修復選項](./media/backup-azure-restore-windows-server/samemachine_browserecover_instantrestore.png)


8. <span data-ttu-id="a06f3-150">在 [Windows 檔案總管] 中，複製要還原的檔案和/或資料夾，並將它們貼上至伺服器或電腦的任意本機位置。</span><span class="sxs-lookup"><span data-stu-id="a06f3-150">In Windows Explorer, copy the files and/or folders you want to restore and paste them to any location local to the server or computer.</span></span> <span data-ttu-id="a06f3-151">您可以直接從復原磁碟區開啟或串流檔案，並確認是否復原正確的版本。</span><span class="sxs-lookup"><span data-stu-id="a06f3-151">You can open or stream the files directly from the recovery volume and verify the correct versions are recovered.</span></span>

    ![複製掛接磁碟區的檔案和資料夾，並貼上至本機位置](./media/backup-azure-restore-windows-server/samemachine_copy_instantrestore.png)

9. <span data-ttu-id="a06f3-153">當您完成還原檔案和/或資料夾後，請在 [瀏覽及復原檔案] 窗格上，按一下 [卸載]。</span><span class="sxs-lookup"><span data-stu-id="a06f3-153">When you are finished restoring the files and/or folders, on the **Browse and Recovery Files** pane, click **Unmount**.</span></span> <span data-ttu-id="a06f3-154">按一下 [是] 以確認要卸載磁碟區。</span><span class="sxs-lookup"><span data-stu-id="a06f3-154">Then click **Yes** to confirm that you want to unmount the volume.</span></span>

    ![卸載磁碟區並確認](./media/backup-azure-restore-windows-server/samemachine_unmount_instantrestore.png)

    > [!Important]
    > <span data-ttu-id="a06f3-156">如果您並未按一下 [卸載]，復原磁碟區會保持掛接六個小時 (從掛接後開始計算)。</span><span class="sxs-lookup"><span data-stu-id="a06f3-156">If you do not click Unmount, the Recovery Volume will remain mounted for six hours from the time when it was mounted.</span></span> <span data-ttu-id="a06f3-157">當磁碟區處於掛接狀態時，不會執行任何備份作業。</span><span class="sxs-lookup"><span data-stu-id="a06f3-157">No backup operations will run while the volume is mounted.</span></span> <span data-ttu-id="a06f3-158">當掛接磁碟區時，任何排定要執行的備份作業會在復原磁碟區卸載之後才執行。</span><span class="sxs-lookup"><span data-stu-id="a06f3-158">Any backup operation scheduled to run during the time when the volume is mounted, will run after the recovery volume is unmounted.</span></span>
    >


## <a name="recover-data-to-the-same-machine"></a><span data-ttu-id="a06f3-159">將資料還原到相同電腦</span><span class="sxs-lookup"><span data-stu-id="a06f3-159">Recover data to the same machine</span></span>
<span data-ttu-id="a06f3-160">如果您不小心刪除檔案，而您想要將它還原到相同的電腦 (備份進行處)，下列步驟可協助您復原資料。</span><span class="sxs-lookup"><span data-stu-id="a06f3-160">If you accidentally deleted a file and wish to restore it to the same machine (from which the backup is taken), the following steps will help you recover the data.</span></span>

1. <span data-ttu-id="a06f3-161">開啟 **Microsoft Azure 備份** 嵌入式管理單元。</span><span class="sxs-lookup"><span data-stu-id="a06f3-161">Open the **Microsoft Azure Backup** snap in.</span></span>
2. <span data-ttu-id="a06f3-162">按一下 [復原資料]  初始化工作流程。</span><span class="sxs-lookup"><span data-stu-id="a06f3-162">Click **Recover Data** to initiate the workflow.</span></span>

    ![復原資料](./media/backup-azure-restore-windows-server-classic/recover.png)
3. <span data-ttu-id="a06f3-164">選取 **這台伺服器 (*yourmachinename*)** 選項，在同一部電腦上還原備份的檔案。</span><span class="sxs-lookup"><span data-stu-id="a06f3-164">Select the **This server (*yourmachinename*)** option to restore the backed up file on the same machine.</span></span>

    ![相同電腦](./media/backup-azure-restore-windows-server-classic/samemachine.png)
4. <span data-ttu-id="a06f3-166">選擇 [瀏覽檔案] 或 [搜尋檔案]。</span><span class="sxs-lookup"><span data-stu-id="a06f3-166">Choose to **Browse for files** or **Search for files**.</span></span>

    <span data-ttu-id="a06f3-167">如果您打算還原路徑已知的一個或多個檔案，請保留預設選項。</span><span class="sxs-lookup"><span data-stu-id="a06f3-167">Leave the default option if you plan to restore one or more files whose path is known.</span></span> <span data-ttu-id="a06f3-168">如果您不確定資料夾結構，但想要搜尋檔案，請挑選 [ **搜尋檔案** ] 選項。</span><span class="sxs-lookup"><span data-stu-id="a06f3-168">If you are not sure about the folder structure but would like to search for a file, pick the **Search for files** option.</span></span> <span data-ttu-id="a06f3-169">為了達成本章節的目的，我們將使用預設選項繼續進行。</span><span class="sxs-lookup"><span data-stu-id="a06f3-169">For the purpose of this section, we will proceed with the default option.</span></span>

    ![瀏覽檔案](./media/backup-azure-restore-windows-server-classic/browseandsearch.png)
5. <span data-ttu-id="a06f3-171">選取您要還原檔案所在的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="a06f3-171">Select the volume from which you wish to restore the file.</span></span>

    <span data-ttu-id="a06f3-172">您可以從任何時間點還原。</span><span class="sxs-lookup"><span data-stu-id="a06f3-172">You can restore from any point in time.</span></span> <span data-ttu-id="a06f3-173">日曆控制項中以 **粗體** 顯示的日期會指出還原點的可用性。</span><span class="sxs-lookup"><span data-stu-id="a06f3-173">Dates which appear in **bold** in the calendar control indicate the availability of a restore point.</span></span> <span data-ttu-id="a06f3-174">選取日期之後，您可以根據您的備份排程 (以及成功的備份作業)，從 [時間]  下拉式清單選取時間點。</span><span class="sxs-lookup"><span data-stu-id="a06f3-174">Once a date is selected, based on your backup schedule (and the success of a backup operation), you can select a point in time from the **Time** drop down.</span></span>

    ![磁碟區和日期](./media/backup-azure-restore-windows-server-classic/volanddate.png)
6. <span data-ttu-id="a06f3-176">選取要復原的項目。</span><span class="sxs-lookup"><span data-stu-id="a06f3-176">Select the items to recover.</span></span> <span data-ttu-id="a06f3-177">您可以複選想要還原的資料夾/檔案。</span><span class="sxs-lookup"><span data-stu-id="a06f3-177">You can multi-select folders/files you wish to restore.</span></span>

    ![選取檔案](./media/backup-azure-restore-windows-server-classic/selectfiles.png)
7. <span data-ttu-id="a06f3-179">指定復原參數。</span><span class="sxs-lookup"><span data-stu-id="a06f3-179">Specify the recovery parameters.</span></span>

    ![修復選項](./media/backup-azure-restore-windows-server-classic/recoveroptions.png)

   * <span data-ttu-id="a06f3-181">您可以選擇還原至原始位置 (其中的檔案/資料夾可能會遭到覆寫) 或相同電腦中的其他位置。</span><span class="sxs-lookup"><span data-stu-id="a06f3-181">You have an option of restoring to the original location (in which the file/folder would be overwritten) or to another location in the same machine.</span></span>
   * <span data-ttu-id="a06f3-182">如果目標位置有您想要還原的檔案/資料夾存在，您可以建立複本 (相同檔案的兩個版本)、覆寫目標位置中的檔案，或略過修復目標位置已存在的檔案。</span><span class="sxs-lookup"><span data-stu-id="a06f3-182">If the file/folder you wish to restore exists in the target location, you can create copies (two versions of the same file), overwrite the files in the target location, or skip the recovery of the files which exist in the target.</span></span>
   * <span data-ttu-id="a06f3-183">強烈建議您針對正在復原檔案上的 ACL 保留預設還原選項。</span><span class="sxs-lookup"><span data-stu-id="a06f3-183">It is highly recommended that you leave the default option of restoring the ACLs on the files which are being recovered.</span></span>
8. <span data-ttu-id="a06f3-184">提供這些輸入之後，按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="a06f3-184">Once these inputs are provided, click **Next**.</span></span> <span data-ttu-id="a06f3-185">就會開始執行將檔案還原到這部電腦的復原工作流程。</span><span class="sxs-lookup"><span data-stu-id="a06f3-185">The recovery workflow, which restores the files to this machine, will begin.</span></span>

## <a name="recover-to-an-alternate-machine"></a><span data-ttu-id="a06f3-186">還原至其他電腦</span><span class="sxs-lookup"><span data-stu-id="a06f3-186">Recover to an alternate machine</span></span>
<span data-ttu-id="a06f3-187">若您遺失整個伺服器，您仍然可從 Azure 備份將資料還原到其他電腦。</span><span class="sxs-lookup"><span data-stu-id="a06f3-187">If your entire server is lost, you can still recover data from Azure Backup to a different machine.</span></span> <span data-ttu-id="a06f3-188">下列步驟說明工作流程。</span><span class="sxs-lookup"><span data-stu-id="a06f3-188">The following steps illustrate the workflow.</span></span>  

<span data-ttu-id="a06f3-189">這些步驟中所使用的術語包含：</span><span class="sxs-lookup"><span data-stu-id="a06f3-189">The terminology used in these steps includes:</span></span>

* <span data-ttu-id="a06f3-190"> – 用來進行備份且目前無法使用的的原始電腦。</span><span class="sxs-lookup"><span data-stu-id="a06f3-190">*Source machine* – The original machine from which the backup was taken and which is currently unavailable.</span></span>
* <span data-ttu-id="a06f3-191"> – 復原資料時的目標電腦。</span><span class="sxs-lookup"><span data-stu-id="a06f3-191">*Target machine* – The machine to which the data is being recovered.</span></span>
* <span data-ttu-id="a06f3-192">「範例保存庫」–「來源電腦」和「目標電腦」註冊的備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="a06f3-192">*Sample vault* – The Backup vault to which the *Source machine* and *Target machine* are registered.</span></span> <br/>

> [!NOTE]
> <span data-ttu-id="a06f3-193">從電腦進行的備份無法在執行舊版作業系統的電腦上進行還原。</span><span class="sxs-lookup"><span data-stu-id="a06f3-193">Backups taken from a machine cannot be restored on a machine which is running an earlier version of the operating system.</span></span> <span data-ttu-id="a06f3-194">例如，如果從 Windows 7 電腦進行備份，則可以在 Windows 8 或更新版電腦上進行還原。</span><span class="sxs-lookup"><span data-stu-id="a06f3-194">For example, if backups are taken from a Windows 7 machine, it can be restored on a Windows 8 or above machine.</span></span> <span data-ttu-id="a06f3-195">不過若情況相反，便無法進行還原。</span><span class="sxs-lookup"><span data-stu-id="a06f3-195">However, the vice-versa does not hold true.</span></span>
>
>

1. <span data-ttu-id="a06f3-196">在「目標電腦」上開啟 [Microsoft Azure 備份] 嵌入式管理單元。</span><span class="sxs-lookup"><span data-stu-id="a06f3-196">Open the **Microsoft Azure Backup** snap in on the *Target machine*.</span></span>
2. <span data-ttu-id="a06f3-197">確定「目標電腦」和「來源電腦」均已註冊到相同的備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="a06f3-197">Ensure that the *Target machine* and the *Source machine* are registered to the same backup vault.</span></span>
3. <span data-ttu-id="a06f3-198">按一下 [復原資料]  初始化工作流程。</span><span class="sxs-lookup"><span data-stu-id="a06f3-198">Click **Recover Data** to initiate the workflow.</span></span>

    ![復原資料](./media/backup-azure-restore-windows-server-classic/recover.png)
4. <span data-ttu-id="a06f3-200">選取 [其他伺服器] </span><span class="sxs-lookup"><span data-stu-id="a06f3-200">Select **Another server**</span></span>

    ![其他伺服器](./media/backup-azure-restore-windows-server-classic/anotherserver.png)
5. <span data-ttu-id="a06f3-202">提供與「範例保存庫」 相對應的保存庫認證檔。</span><span class="sxs-lookup"><span data-stu-id="a06f3-202">Provide the vault credential file that corresponds to the *Sample vault*.</span></span> <span data-ttu-id="a06f3-203">如果保存庫認證檔無效 (或已過期)，請從 Azure 傳統入口網站中的「範例保存庫」  下載新的保存庫認證檔。</span><span class="sxs-lookup"><span data-stu-id="a06f3-203">If the vault credential file is invalid (or expired) download a new vault credential file from the *Sample vault* in the Azure classic portal.</span></span> <span data-ttu-id="a06f3-204">一旦提供保存庫認證檔，即會顯示保存庫認證檔的備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="a06f3-204">Once the vault credential file is provided, the backup vault against the vault credential file is displayed.</span></span>
6. <span data-ttu-id="a06f3-205">在顯示電腦的清單中選取 [來源電腦]  。</span><span class="sxs-lookup"><span data-stu-id="a06f3-205">Select the *Source machine* from the list of displayed machines.</span></span>

    ![電腦清單](./media/backup-azure-restore-windows-server-classic/machinelist.png)
7. <span data-ttu-id="a06f3-207">選取 [搜尋檔案] 或 [瀏覽檔案] 選項。</span><span class="sxs-lookup"><span data-stu-id="a06f3-207">Select either the **Search for files** or **Browse for files** option.</span></span> <span data-ttu-id="a06f3-208">為了達成本章節的目的，我們將使用 [搜尋檔案]  選項。</span><span class="sxs-lookup"><span data-stu-id="a06f3-208">For the purpose of this section, we will use the **Search for files** option.</span></span>

    ![Search](./media/backup-azure-restore-windows-server-classic/search.png)
8. <span data-ttu-id="a06f3-210">在下一個畫面中選取磁碟區和日期。</span><span class="sxs-lookup"><span data-stu-id="a06f3-210">Select the volume and date in the next screen.</span></span> <span data-ttu-id="a06f3-211">搜尋您想要還原的資料夾/檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="a06f3-211">Search for the folder/file name you want to restore.</span></span>

    ![搜尋項目](./media/backup-azure-restore-windows-server-classic/searchitems.png)
9. <span data-ttu-id="a06f3-213">選取需要還原之檔案的位置。</span><span class="sxs-lookup"><span data-stu-id="a06f3-213">Select the location where the files need to be restored.</span></span>

    ![還原位置](./media/backup-azure-restore-windows-server-classic/restorelocation.png)
10. <span data-ttu-id="a06f3-215">提供「來源電腦」註冊至「範例保存庫」期間所提供的加密複雜密碼。</span><span class="sxs-lookup"><span data-stu-id="a06f3-215">Provide the encryption passphrase that was provided during *Source machine’s* registration to *Sample vault*.</span></span>

    ![加密](./media/backup-azure-restore-windows-server-classic/encryption.png)
11. <span data-ttu-id="a06f3-217">一旦提供輸入，則按一下 [復原] ，將會觸發還原備份檔案到所提供目的地的程序。</span><span class="sxs-lookup"><span data-stu-id="a06f3-217">Once the input is provided, click **Recover**, which triggers the restore of the backed up files to the destination provided.</span></span>

## <a name="use-instant-restore-to-restore-data-to-an-alternate-machine"></a><span data-ttu-id="a06f3-218">使用「立即還原」將資料還原至其他電腦</span><span class="sxs-lookup"><span data-stu-id="a06f3-218">Use Instant Restore to restore data to an alternate machine</span></span>
<span data-ttu-id="a06f3-219">若您遺失整個伺服器，您仍然可從 Azure 備份將資料還原到其他電腦。</span><span class="sxs-lookup"><span data-stu-id="a06f3-219">If your entire server is lost, you can still recover data from Azure Backup to a different machine.</span></span> <span data-ttu-id="a06f3-220">下列步驟說明工作流程。</span><span class="sxs-lookup"><span data-stu-id="a06f3-220">The following steps illustrate the workflow.</span></span>

<span data-ttu-id="a06f3-221">這些步驟中所使用的術語包含：</span><span class="sxs-lookup"><span data-stu-id="a06f3-221">The terminology used in these steps includes:</span></span>

* <span data-ttu-id="a06f3-222"> – 用來進行備份且目前無法使用的的原始電腦。</span><span class="sxs-lookup"><span data-stu-id="a06f3-222">*Source machine* – The original machine from which the backup was taken and which is currently unavailable.</span></span>
* <span data-ttu-id="a06f3-223"> – 復原資料時的目標電腦。</span><span class="sxs-lookup"><span data-stu-id="a06f3-223">*Target machine* – The machine to which the data is being recovered.</span></span>
* <span data-ttu-id="a06f3-224">「範例保存庫」–「來源電腦」和「目標電腦」註冊的復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="a06f3-224">*Sample vault* – The Recovery Services vault to which the *Source machine* and *Target machine* are registered.</span></span> <br/>

> [!NOTE]
> <span data-ttu-id="a06f3-225">備份無法還原到執行舊版作業系統的目標電腦。</span><span class="sxs-lookup"><span data-stu-id="a06f3-225">Backups can't be restored to a target machine running an earlier version of the operating system.</span></span> <span data-ttu-id="a06f3-226">例如，從 Windows 7 電腦建立的備份可以還原至 Windows 8 或更新版本的電腦。</span><span class="sxs-lookup"><span data-stu-id="a06f3-226">For example, a backup taken from a Windows 7 computer can be restored on a Windows 8, or later, computer.</span></span> <span data-ttu-id="a06f3-227">從 Windows 8 電腦建立的備份無法還原至 Windows 7 電腦。</span><span class="sxs-lookup"><span data-stu-id="a06f3-227">A backup taken from a Windows 8 computer cannot be restored to a Windows 7 computer.</span></span>
>
>

1. <span data-ttu-id="a06f3-228">在「目標電腦」上開啟 [Microsoft Azure 備份] 嵌入式管理單元。</span><span class="sxs-lookup"><span data-stu-id="a06f3-228">Open the **Microsoft Azure Backup** snap in on the *Target machine*.</span></span>

2. <span data-ttu-id="a06f3-229">確定 [目標電腦] 和 [來源電腦] 已註冊到同一個復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="a06f3-229">Ensure the *Target machine* and the *Source machine* are registered to the same Recovery Services vault.</span></span>

3. <span data-ttu-id="a06f3-230">按一下 [復原資料] 以開啟 [復原資料精靈]。</span><span class="sxs-lookup"><span data-stu-id="a06f3-230">Click **Recover Data** to open the **Recover Data wizard**.</span></span>

    ![復原資料](./media/backup-azure-restore-windows-server/recover.png)

4. <span data-ttu-id="a06f3-232">在 [開始使用] 窗格上，選取 [其他伺服器]</span><span class="sxs-lookup"><span data-stu-id="a06f3-232">On the **Getting Started** pane, select **Another server**</span></span>

    ![其他伺服器](./media/backup-azure-restore-windows-server/alternatemachine_gettingstarted_instantrestore.png)

5. <span data-ttu-id="a06f3-234">提供與「範例保存庫」相對應的保存庫認證檔，然後按一下 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="a06f3-234">Provide the vault credential file that corresponds to the *Sample vault*, and click **Next**.</span></span>

    <span data-ttu-id="a06f3-235">如果保存庫認證檔無效 (或已過期)，請從 Azure 入口網站中的「範例保存庫」下載新的保存庫認證檔。</span><span class="sxs-lookup"><span data-stu-id="a06f3-235">If the vault credential file is invalid (or expired), download a new vault credential file from the *Sample vault* in the Azure portal.</span></span> <span data-ttu-id="a06f3-236">一旦您提供有效的保存庫認證檔之後，就會顯示對應的備份保存庫名稱。</span><span class="sxs-lookup"><span data-stu-id="a06f3-236">Once you provide a valid vault credential, the name of the corresponding Backup Vault appears.</span></span>

6. <span data-ttu-id="a06f3-237">在 [選取備份伺服器] 窗格上，從顯示的電腦清單選取 [來源電腦]，並提供複雜密碼。</span><span class="sxs-lookup"><span data-stu-id="a06f3-237">On the **Select Backup Server** pane, select the *Source machine* from the list of displayed machines and provide the passphrase.</span></span> <span data-ttu-id="a06f3-238">然後按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="a06f3-238">Then click **Next**.</span></span>

    ![電腦清單](./media/backup-azure-restore-windows-server/alternatemachine_selectmachine_instantrestore.png)

7. <span data-ttu-id="a06f3-240">在 [選取復原模式] 窗格上，選取 [個別檔案和資料夾] 並按一下 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="a06f3-240">On the **Select Recovery Mode** pane, select **Individual files and folders** and click **Next**.</span></span>

    ![搜尋](./media/backup-azure-restore-windows-server/alternatemachine_selectrecoverymode_instantrestore.png)

8. <span data-ttu-id="a06f3-242">在 [選取磁碟區和日期] 窗格上，選取包含您要還原之檔案和/或資料夾的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="a06f3-242">On the **Select Volume and Date** pane, select the volume that contains the files and/or folders you want to restore.</span></span>

    <span data-ttu-id="a06f3-243">在日曆上，選取復原點。</span><span class="sxs-lookup"><span data-stu-id="a06f3-243">On the calendar, select a recovery point.</span></span> <span data-ttu-id="a06f3-244">您可以從任何時間的復原點還原。</span><span class="sxs-lookup"><span data-stu-id="a06f3-244">You can restore from any recovery point in time.</span></span> <span data-ttu-id="a06f3-245">**粗體**的日期表示至少有一個復原點可用。</span><span class="sxs-lookup"><span data-stu-id="a06f3-245">Dates in **bold** indicate the availability of at least one recovery point.</span></span> <span data-ttu-id="a06f3-246">一旦您選取一個日期，如果有多個復原點可用，您可以從 [時間] 下拉式功能表選擇特定的復原點。</span><span class="sxs-lookup"><span data-stu-id="a06f3-246">Once you select a date, if multiple recovery points are available, choose the specific recovery point from the **Time** drop-down menu.</span></span>

    ![搜尋項目](./media/backup-azure-restore-windows-server/alternatemachine_selectvolumedate_instantrestore.png)

9. <span data-ttu-id="a06f3-248">按一下 [掛接] 以掛接本機的復原點，做為 [目標電腦] 的復原磁碟區。</span><span class="sxs-lookup"><span data-stu-id="a06f3-248">Click **Mount** to locally mount the recovery point as a recovery volume on your *Target machine*.</span></span>

10. <span data-ttu-id="a06f3-249">在 [瀏覽及復原檔案] 窗格上，按一下 [瀏覽] 以開啟 [Windows 檔案總管]，然後尋找所需的檔案和資料夾。</span><span class="sxs-lookup"><span data-stu-id="a06f3-249">On the **Browse and Recover Files** pane, click **Browse** to open Windows Explorer and find the files and folders you want.</span></span>

    ![加密](./media/backup-azure-restore-windows-server/alternatemachine_browserecover_instantrestore.png)

11. <span data-ttu-id="a06f3-251">在 [Windows 檔案總管] 中，從復原磁碟區複製檔案和/或資料夾，然後貼上至 [目標電腦] 位置。</span><span class="sxs-lookup"><span data-stu-id="a06f3-251">In Windows Explorer, copy the files and/or folders from the recovery volume and paste them to your *Target machine* location.</span></span> <span data-ttu-id="a06f3-252">您可以直接從復原磁碟區開啟或串流檔案，並確認是否復原正確的版本。</span><span class="sxs-lookup"><span data-stu-id="a06f3-252">You can open or stream the files directly from the recovery volume and verify the correct versions are recovered.</span></span>

    ![加密](./media/backup-azure-restore-windows-server/alternatemachine_copy_instantrestore.png)

12. <span data-ttu-id="a06f3-254">當您完成還原檔案和/或資料夾後，請在 [瀏覽及復原檔案] 窗格上，按一下 [卸載]。</span><span class="sxs-lookup"><span data-stu-id="a06f3-254">When you are finished restoring the files and/or folders, on the **Browse and Recovery Files** pane, click **Unmount**.</span></span> <span data-ttu-id="a06f3-255">按一下 [是] 以確認要卸載磁碟區。</span><span class="sxs-lookup"><span data-stu-id="a06f3-255">Then click **Yes** to confirm that you want to unmount the volume.</span></span>

    ![加密](./media/backup-azure-restore-windows-server/alternatemachine_unmount_instantrestore.png)

    > [!Important]
    > <span data-ttu-id="a06f3-257">如果您並未按一下 [卸載]，復原磁碟區會保持掛接六個小時 (從掛接後開始計算)。</span><span class="sxs-lookup"><span data-stu-id="a06f3-257">If you do not click Unmount, the Recovery Volume will remain mounted for six hours from the time when it was mounted.</span></span> <span data-ttu-id="a06f3-258">當磁碟區處於掛接狀態時，不會執行任何備份作業。</span><span class="sxs-lookup"><span data-stu-id="a06f3-258">No backup operations will run while the volume is mounted.</span></span> <span data-ttu-id="a06f3-259">當掛接磁碟區時，任何排定要執行的備份作業會在復原磁碟區卸載之後才執行。</span><span class="sxs-lookup"><span data-stu-id="a06f3-259">Any backup operation scheduled to run during the time when the volume is mounted, will run after the recovery volume is unmounted.</span></span>
    >


## <a name="next-steps"></a><span data-ttu-id="a06f3-260">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a06f3-260">Next steps</span></span>
* [<span data-ttu-id="a06f3-261">Azure 備份常見問題集</span><span class="sxs-lookup"><span data-stu-id="a06f3-261">Azure Backup FAQ</span></span>](backup-azure-backup-faq.md)
* <span data-ttu-id="a06f3-262">造訪 [Azure 備份論壇](http://go.microsoft.com/fwlink/p/?LinkId=290933)(英文)。</span><span class="sxs-lookup"><span data-stu-id="a06f3-262">Visit the [Azure Backup Forum](http://go.microsoft.com/fwlink/p/?LinkId=290933).</span></span>

## <a name="learn-more"></a><span data-ttu-id="a06f3-263">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="a06f3-263">Learn more</span></span>
* [<span data-ttu-id="a06f3-264">Azure 備份概觀</span><span class="sxs-lookup"><span data-stu-id="a06f3-264">Azure Backup Overview</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=222425)
* [<span data-ttu-id="a06f3-265">備份 Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="a06f3-265">Backup Azure virtual machines</span></span>](backup-azure-vms-introduction.md)
* [<span data-ttu-id="a06f3-266">備份 Microsoft 工作負載</span><span class="sxs-lookup"><span data-stu-id="a06f3-266">Backup up Microsoft workloads</span></span>](backup-azure-dpm-introduction.md)
