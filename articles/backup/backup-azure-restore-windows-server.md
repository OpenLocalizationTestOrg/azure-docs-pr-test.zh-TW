---
title: "將 Azure 中的資料還原至 Windows Server 或 Windows 電腦 | Microsoft Docs"
description: "了解如何將儲存於 Azure 中的資料還原至 Windows Server 或 Windows 電腦。"
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: 742f4b9e-c0ab-4eeb-8e22-ee29b83c22c4
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/16/2017
ms.author: saurse;trinadhk;markgal;
ms.openlocfilehash: 231dd61f95267b3a504ed70e9b3a5abc470b69b2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="restore-files-to-a-windows-server-or-windows-client-machine-using-resource-manager-deployment-model"></a><span data-ttu-id="9e6f9-103">使用 Resource Manager 部署模型將檔案還原到 Windows Server 或 Windows 用戶端電腦</span><span class="sxs-lookup"><span data-stu-id="9e6f9-103">Restore files to a Windows server or Windows client machine using Resource Manager deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9e6f9-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="9e6f9-104">Azure portal</span></span>](backup-azure-restore-windows-server.md)
> * [<span data-ttu-id="9e6f9-105">傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="9e6f9-105">Classic portal</span></span>](backup-azure-restore-windows-server-classic.md)
>
>

<span data-ttu-id="9e6f9-106">此文章說明如何從備份保存庫還原資料。</span><span class="sxs-lookup"><span data-stu-id="9e6f9-106">This article explains how to restore data from a backup vault.</span></span> <span data-ttu-id="9e6f9-107">若要還原資料，您可以使用 Microsoft Azure 復原服務 (MARS) 代理程式中的 [復原資料精靈]。</span><span class="sxs-lookup"><span data-stu-id="9e6f9-107">To restore data, you use the Recover Data wizard in the Microsoft Azure Recovery Services (MARS) agent.</span></span> <span data-ttu-id="9e6f9-108">當您還原資料時，您可以︰</span><span class="sxs-lookup"><span data-stu-id="9e6f9-108">When you restore data, it is possible to:</span></span>

* <span data-ttu-id="9e6f9-109">將資料還原到進行備份的相同電腦。</span><span class="sxs-lookup"><span data-stu-id="9e6f9-109">Restore data to the same machine from which the backups were taken.</span></span>
* <span data-ttu-id="9e6f9-110">將資料還原至其他電腦。</span><span class="sxs-lookup"><span data-stu-id="9e6f9-110">Restore data to an alternate machine.</span></span>

<span data-ttu-id="9e6f9-111">2017 年 1 月，Microsoft 推出 MARS 代理程式預覽更新。</span><span class="sxs-lookup"><span data-stu-id="9e6f9-111">In January 2017, Microsoft released a Preview update to the MARS agent.</span></span> <span data-ttu-id="9e6f9-112">這項更新除了錯誤修正之外，還啟用了「立即還原」，允許您掛接可寫入的復原點快照來做為復原磁碟區。</span><span class="sxs-lookup"><span data-stu-id="9e6f9-112">Along with bug fixes, this update enables Instant Restore, which allows you to mount a writeable recovery point snapshot as a recovery volume.</span></span> <span data-ttu-id="9e6f9-113">您接著可以探索復磁碟區並將檔案複製至本機電腦，藉此選擇性地還原檔案。</span><span class="sxs-lookup"><span data-stu-id="9e6f9-113">You can then explore the recovery volume and copy files to a local computer thereby selectively restoring files.</span></span>

> [!NOTE]
> <span data-ttu-id="9e6f9-114">如果您要使用「立即還原」來還原資料，必須要有 [2017 年 1 月 Azure 備份更新](https://support.microsoft.com/en-us/help/3216528?preview)。</span><span class="sxs-lookup"><span data-stu-id="9e6f9-114">The [January 2017 Azure Backup update](https://support.microsoft.com/en-us/help/3216528?preview) is required if you want to use Instant Restore to restore data.</span></span> <span data-ttu-id="9e6f9-115">另外，您也必須在支援文章列出之地區設定的保存庫中，保護備份資料。</span><span class="sxs-lookup"><span data-stu-id="9e6f9-115">Also the backup data must be protected in vaults in locales listed in the support article.</span></span> <span data-ttu-id="9e6f9-116">請參閱 [2017 年 1 月 Azure 備份更新](https://support.microsoft.com/en-us/help/3216528?preview)，了解支援「立即還原」的最新地區設定清單。</span><span class="sxs-lookup"><span data-stu-id="9e6f9-116">Consult the [January 2017 Azure Backup update](https://support.microsoft.com/en-us/help/3216528?preview) for the latest list of locales that support Instant Restore.</span></span> <span data-ttu-id="9e6f9-117">「立即還原」目前**無法**在所有地區設定中使用。</span><span class="sxs-lookup"><span data-stu-id="9e6f9-117">Instant Restore is **not** currently available in all locales.</span></span>
>

<span data-ttu-id="9e6f9-118">「立即還原」可用於 Azure 入口網站中的復原服務保存庫以及傳統入口網站中的備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="9e6f9-118">Instant Restore is available for use in Recovery Services vaults in the Azure portal and Backup vaults in the classic portal.</span></span> <span data-ttu-id="9e6f9-119">如果您想要使用「立即還原」，請下載 MARS 更新，並依照提及「立即還原」部分中的程序進行操作。</span><span class="sxs-lookup"><span data-stu-id="9e6f9-119">If you want to use Instant Restore, download the MARS update, and follow the procedures that mention Instant Restore.</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="use-instant-restore-to-recover-data-to-the-same-machine"></a><span data-ttu-id="9e6f9-120">使用「立即還原」將資料還原至同一台電腦</span><span class="sxs-lookup"><span data-stu-id="9e6f9-120">Use Instant Restore to recover data to the same machine</span></span>

<span data-ttu-id="9e6f9-121">如果您不小心刪除檔案，而您想要將它還原到相同的電腦 (備份進行處)，下列步驟可協助您復原資料。</span><span class="sxs-lookup"><span data-stu-id="9e6f9-121">If you accidentally deleted a file and wish to restore it to the same machine (from which the backup is taken), the following steps will help you recover the data.</span></span>

1. <span data-ttu-id="9e6f9-122">開啟 **Microsoft Azure 備份** 嵌入式管理單元。</span><span class="sxs-lookup"><span data-stu-id="9e6f9-122">Open the **Microsoft Azure Backup** snap in.</span></span> <span data-ttu-id="9e6f9-123">如果您不知道快照安裝的位置，請在電腦或伺服器上搜尋 **Microsoft Azure 備份**。</span><span class="sxs-lookup"><span data-stu-id="9e6f9-123">If you don't know where the snap in was installed, search the computer or server for **Microsoft Azure Backup**.</span></span>

    <span data-ttu-id="9e6f9-124">傳統型應用程式應該會出現在搜尋結果中。</span><span class="sxs-lookup"><span data-stu-id="9e6f9-124">The desktop app should appear in the search results.</span></span>

2. <span data-ttu-id="9e6f9-125">按一下 [復原資料] 以啟動精靈。</span><span class="sxs-lookup"><span data-stu-id="9e6f9-125">Click **Recover Data** to start the wizard.</span></span>

    ![復原資料](./media/backup-azure-restore-windows-server/recover.png)

3. <span data-ttu-id="9e6f9-127">在 [開始使用] 窗格中，若要將資料還原至同一台伺服器或電腦，請選取 [這台伺服器 (`<server name>`)] 並按一下 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="9e6f9-127">On the **Getting Started** pane, to restore the data to the same server or computer, select **This server (`<server name>`)** and click **Next**.</span></span>

    ![選擇 [這台伺服器] 選項以將資料還原到同一台電腦](./media/backup-azure-restore-windows-server/samemachine_gettingstarted_instantrestore.png)

4. <span data-ttu-id="9e6f9-129">在 [選取復原模式] 窗格上，選擇 [個別檔案與資料夾]，然後按一下 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="9e6f9-129">On the **Select Recovery Mode** pane, choose **Individual files and folders** and then click **Next**.</span></span>

    ![瀏覽檔案](./media/backup-azure-restore-windows-server/samemachine_selectrecoverymode_instantrestore.png)

5. <span data-ttu-id="9e6f9-131">在 [選取磁碟區和日期] 窗格上，選取包含您要還原之檔案和/或資料夾的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="9e6f9-131">On the **Select Volume and Date** pane, select the volume that contains the files and/or folders you want to restore.</span></span>

    <span data-ttu-id="9e6f9-132">在日曆上，選取復原點。</span><span class="sxs-lookup"><span data-stu-id="9e6f9-132">On the calendar, select a recovery point.</span></span> <span data-ttu-id="9e6f9-133">您可以從任何時間的復原點還原。</span><span class="sxs-lookup"><span data-stu-id="9e6f9-133">You can restore from any recovery point in time.</span></span> <span data-ttu-id="9e6f9-134">**粗體**的日期表示至少有一個復原點可用。</span><span class="sxs-lookup"><span data-stu-id="9e6f9-134">Dates in **bold** indicate the availability of at least one recovery point.</span></span> <span data-ttu-id="9e6f9-135">一旦您選取一個日期，如果有多個復原點可用，您可以從 [時間] 下拉式功能表選擇特定的復原點。</span><span class="sxs-lookup"><span data-stu-id="9e6f9-135">Once you select a date, if multiple recovery points are available, choose the specific recovery point from the **Time** drop-down menu.</span></span>

    ![磁碟區和日期](./media/backup-azure-restore-windows-server/samemachine_selectvolumedate_instantrestore.png)

6. <span data-ttu-id="9e6f9-137">選擇要還原的復原點之後，按一下 [掛接]。</span><span class="sxs-lookup"><span data-stu-id="9e6f9-137">Once you have chosen the recovery point to restore, click **Mount**.</span></span>

    <span data-ttu-id="9e6f9-138">Azure 備份會掛接本機復原點，並且使用它做為復原磁碟區。</span><span class="sxs-lookup"><span data-stu-id="9e6f9-138">Azure Backup mounts the local recovery point, and uses it as a recovery volume.</span></span>

7. <span data-ttu-id="9e6f9-139">在 [瀏覽及復原檔案] 窗格上，按一下 [瀏覽] 以開啟 [Windows 檔案總管]，然後尋找所需的檔案和資料夾。</span><span class="sxs-lookup"><span data-stu-id="9e6f9-139">On the **Browse and Recover Files** pane, click **Browse** to open Windows Explorer and find the files and folders you want.</span></span>

    ![修復選項](./media/backup-azure-restore-windows-server/samemachine_browserecover_instantrestore.png)


8. <span data-ttu-id="9e6f9-141">在 [Windows 檔案總管] 中，複製要還原的檔案和/或資料夾，並將它們貼上至伺服器或電腦的任意本機位置。</span><span class="sxs-lookup"><span data-stu-id="9e6f9-141">In Windows Explorer, copy the files and/or folders you want to restore and paste them to any location local to the server or computer.</span></span> <span data-ttu-id="9e6f9-142">您可以直接從復原磁碟區開啟或串流檔案，並確認是否復原正確的版本。</span><span class="sxs-lookup"><span data-stu-id="9e6f9-142">You can open or stream the files directly from the recovery volume and verify the correct versions are recovered.</span></span>

    ![複製掛接磁碟區的檔案和資料夾，並貼上至本機位置](./media/backup-azure-restore-windows-server/samemachine_copy_instantrestore.png)

9. <span data-ttu-id="9e6f9-144">當您完成還原檔案和/或資料夾後，請在 [瀏覽及復原檔案] 窗格上，按一下 [卸載]。</span><span class="sxs-lookup"><span data-stu-id="9e6f9-144">When you are finished restoring the files and/or folders, on the **Browse and Recovery Files** pane, click **Unmount**.</span></span> <span data-ttu-id="9e6f9-145">按一下 [是] 以確認要卸載磁碟區。</span><span class="sxs-lookup"><span data-stu-id="9e6f9-145">Then click **Yes** to confirm that you want to unmount the volume.</span></span>

    ![卸載磁碟區並確認](./media/backup-azure-restore-windows-server/samemachine_unmount_instantrestore.png)

    > [!Important]
    > <span data-ttu-id="9e6f9-147">如果您並未按一下 [卸載]，復原磁碟區會保持掛接 6 個小時 (從掛接後開始計算)。</span><span class="sxs-lookup"><span data-stu-id="9e6f9-147">If you do not click Unmount, the Recovery Volume will remain mounted for 6 hours from the time when it was mounted.</span></span> <span data-ttu-id="9e6f9-148">不過，如果是進行中的檔案複製，掛接時間可擴充至高達 24 小時。</span><span class="sxs-lookup"><span data-stu-id="9e6f9-148">However, the mount time is extended upto a maximum of 24 hours in case of an ongoing file-copy.</span></span> <span data-ttu-id="9e6f9-149">當磁碟區處於掛接狀態時，不會執行任何備份作業。</span><span class="sxs-lookup"><span data-stu-id="9e6f9-149">No backup operations will run while the volume is mounted.</span></span> <span data-ttu-id="9e6f9-150">當掛接磁碟區時，任何排定要執行的備份作業會在復原磁碟區卸載之後才執行。</span><span class="sxs-lookup"><span data-stu-id="9e6f9-150">Any backup operation scheduled to run during the time when the volume is mounted, will run after the recovery volume is unmounted.</span></span>
    >


## <a name="use-instant-restore-to-restore-data-to-an-alternate-machine"></a><span data-ttu-id="9e6f9-151">使用「立即還原」將資料還原至其他電腦</span><span class="sxs-lookup"><span data-stu-id="9e6f9-151">Use Instant Restore to restore data to an alternate machine</span></span>
<span data-ttu-id="9e6f9-152">若您遺失整個伺服器，您仍然可從 Azure 備份將資料還原到其他電腦。</span><span class="sxs-lookup"><span data-stu-id="9e6f9-152">If your entire server is lost, you can still recover data from Azure Backup to a different machine.</span></span> <span data-ttu-id="9e6f9-153">下列步驟說明工作流程。</span><span class="sxs-lookup"><span data-stu-id="9e6f9-153">The following steps illustrate the workflow.</span></span>


<span data-ttu-id="9e6f9-154">這些步驟中所使用的術語包含：</span><span class="sxs-lookup"><span data-stu-id="9e6f9-154">The terminology used in these steps includes:</span></span>

* <span data-ttu-id="9e6f9-155"> – 用來進行備份且目前無法使用的的原始電腦。</span><span class="sxs-lookup"><span data-stu-id="9e6f9-155">*Source machine* – The original machine from which the backup was taken and which is currently unavailable.</span></span>
* <span data-ttu-id="9e6f9-156"> – 復原資料時的目標電腦。</span><span class="sxs-lookup"><span data-stu-id="9e6f9-156">*Target machine* – The machine to which the data is being recovered.</span></span>
* <span data-ttu-id="9e6f9-157">「範例保存庫」–「來源電腦」和「目標電腦」註冊的復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="9e6f9-157">*Sample vault* – The Recovery Services vault to which the *Source machine* and *Target machine* are registered.</span></span> <br/>

> [!NOTE]
> <span data-ttu-id="9e6f9-158">備份無法還原到執行舊版作業系統的目標電腦。</span><span class="sxs-lookup"><span data-stu-id="9e6f9-158">Backups can't be restored to a target machine running an earlier version of the operating system.</span></span> <span data-ttu-id="9e6f9-159">例如，從 Windows 7 電腦建立的備份可以還原至 Windows 8 或更新版本的電腦。</span><span class="sxs-lookup"><span data-stu-id="9e6f9-159">For example, a backup taken from a Windows 7 computer can be restored on a Windows 8, or later, computer.</span></span> <span data-ttu-id="9e6f9-160">從 Windows 8 電腦建立的備份無法還原至 Windows 7 電腦。</span><span class="sxs-lookup"><span data-stu-id="9e6f9-160">A backup taken from a Windows 8 computer cannot be restored to a Windows 7 computer.</span></span>
>
>

1. <span data-ttu-id="9e6f9-161">在「目標電腦」上開啟 [Microsoft Azure 備份] 嵌入式管理單元。</span><span class="sxs-lookup"><span data-stu-id="9e6f9-161">Open the **Microsoft Azure Backup** snap in on the *Target machine*.</span></span>

2. <span data-ttu-id="9e6f9-162">確定 [目標電腦] 和 [來源電腦] 已註冊到同一個復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="9e6f9-162">Ensure the *Target machine* and the *Source machine* are registered to the same Recovery Services vault.</span></span>

3. <span data-ttu-id="9e6f9-163">按一下 [復原資料] 以開啟 [復原資料精靈]。</span><span class="sxs-lookup"><span data-stu-id="9e6f9-163">Click **Recover Data** to open the **Recover Data wizard**.</span></span>

    ![復原資料](./media/backup-azure-restore-windows-server/recover.png)

4. <span data-ttu-id="9e6f9-165">在 [開始使用] 窗格上，選取 [其他伺服器]</span><span class="sxs-lookup"><span data-stu-id="9e6f9-165">On the **Getting Started** pane, select **Another server**</span></span>

    ![其他伺服器](./media/backup-azure-restore-windows-server/alternatemachine_gettingstarted_instantrestore.png)

5. <span data-ttu-id="9e6f9-167">提供與「範例保存庫」相對應的保存庫認證檔，然後按一下 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="9e6f9-167">Provide the vault credential file that corresponds to the *Sample vault*, and click **Next**.</span></span>

    <span data-ttu-id="9e6f9-168">如果保存庫認證檔無效 (或已過期)，請從 Azure 入口網站中的「範例保存庫」下載新的保存庫認證檔。</span><span class="sxs-lookup"><span data-stu-id="9e6f9-168">If the vault credential file is invalid (or expired), download a new vault credential file from the *Sample vault* in the Azure portal.</span></span> <span data-ttu-id="9e6f9-169">一旦您提供有效的保存庫認證檔之後，就會顯示對應的備份保存庫名稱。</span><span class="sxs-lookup"><span data-stu-id="9e6f9-169">Once you provide a valid vault credential, the name of the corresponding Backup Vault appears.</span></span>


6. <span data-ttu-id="9e6f9-170">在 [選取備份伺服器] 窗格上，從顯示的電腦清單選取 [來源電腦]，並提供複雜密碼。</span><span class="sxs-lookup"><span data-stu-id="9e6f9-170">On the **Select Backup Server** pane, select the *Source machine* from the list of displayed machines and provide the passphrase.</span></span> <span data-ttu-id="9e6f9-171">然後按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="9e6f9-171">Then click **Next**.</span></span>

    ![電腦清單](./media/backup-azure-restore-windows-server/alternatemachine_selectmachine_instantrestore.png)

7. <span data-ttu-id="9e6f9-173">在 [選取復原模式] 窗格上，選取 [個別檔案和資料夾] 並按一下 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="9e6f9-173">On the **Select Recovery Mode** pane, select **Individual files and folders** and click **Next**.</span></span>

    ![搜尋](./media/backup-azure-restore-windows-server/alternatemachine_selectrecoverymode_instantrestore.png)

8. <span data-ttu-id="9e6f9-175">在 [選取磁碟區和日期] 窗格上，選取包含您要還原之檔案和/或資料夾的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="9e6f9-175">On the **Select Volume and Date** pane, select the volume that contains the files and/or folders you want to restore.</span></span>

    <span data-ttu-id="9e6f9-176">在日曆上，選取復原點。</span><span class="sxs-lookup"><span data-stu-id="9e6f9-176">On the calendar, select a recovery point.</span></span> <span data-ttu-id="9e6f9-177">您可以從任何時間的復原點還原。</span><span class="sxs-lookup"><span data-stu-id="9e6f9-177">You can restore from any recovery point in time.</span></span> <span data-ttu-id="9e6f9-178">**粗體**的日期表示至少有一個復原點可用。</span><span class="sxs-lookup"><span data-stu-id="9e6f9-178">Dates in **bold** indicate the availability of at least one recovery point.</span></span> <span data-ttu-id="9e6f9-179">一旦您選取一個日期，如果有多個復原點可用，您可以從 [時間] 下拉式功能表選擇特定的復原點。</span><span class="sxs-lookup"><span data-stu-id="9e6f9-179">Once you select a date, if multiple recovery points are available, choose the specific recovery point from the **Time** drop-down menu.</span></span>

    ![搜尋項目](./media/backup-azure-restore-windows-server/alternatemachine_selectvolumedate_instantrestore.png)

9. <span data-ttu-id="9e6f9-181">按一下 [掛接] 以掛接本機的復原點，做為 [目標電腦] 的復原磁碟區。</span><span class="sxs-lookup"><span data-stu-id="9e6f9-181">Click **Mount** to locally mount the recovery point as a recovery volume on your *Target machine*.</span></span>

10. <span data-ttu-id="9e6f9-182">在 [瀏覽及復原檔案] 窗格上，按一下 [瀏覽] 以開啟 [Windows 檔案總管]，然後尋找所需的檔案和資料夾。</span><span class="sxs-lookup"><span data-stu-id="9e6f9-182">On the **Browse and Recover Files** pane, click **Browse** to open Windows Explorer and find the files and folders you want.</span></span>

    ![加密](./media/backup-azure-restore-windows-server/alternatemachine_browserecover_instantrestore.png)

11. <span data-ttu-id="9e6f9-184">在 [Windows 檔案總管] 中，從復原磁碟區複製檔案和/或資料夾，然後貼上至 [目標電腦] 位置。</span><span class="sxs-lookup"><span data-stu-id="9e6f9-184">In Windows Explorer, copy the files and/or folders from the recovery volume and paste them to your *Target machine* location.</span></span> <span data-ttu-id="9e6f9-185">您可以直接從復原磁碟區開啟或串流檔案，並確認是否復原正確的版本。</span><span class="sxs-lookup"><span data-stu-id="9e6f9-185">You can open or stream the files directly from the recovery volume and verify the correct versions are recovered.</span></span>

    ![加密](./media/backup-azure-restore-windows-server/alternatemachine_copy_instantrestore.png)

12. <span data-ttu-id="9e6f9-187">當您完成還原檔案和/或資料夾後，請在 [瀏覽及復原檔案] 窗格上，按一下 [卸載]。</span><span class="sxs-lookup"><span data-stu-id="9e6f9-187">When you are finished restoring the files and/or folders, on the **Browse and Recovery Files** pane, click **Unmount**.</span></span> <span data-ttu-id="9e6f9-188">按一下 [是] 以確認要卸載磁碟區。</span><span class="sxs-lookup"><span data-stu-id="9e6f9-188">Then click **Yes** to confirm that you want to unmount the volume.</span></span>

    ![加密](./media/backup-azure-restore-windows-server/alternatemachine_unmount_instantrestore.png)

    > [!Important]
    > <span data-ttu-id="9e6f9-190">如果您並未按一下 [卸載]，復原磁碟區會保持掛接 6 個小時 (從掛接後開始計算)。</span><span class="sxs-lookup"><span data-stu-id="9e6f9-190">If you do not click Unmount, the Recovery Volume will remain mounted for 6 hours from the time when it was mounted.</span></span> <span data-ttu-id="9e6f9-191">不過，如果是進行中的檔案複製，掛接時間可擴充至高達 24 小時。</span><span class="sxs-lookup"><span data-stu-id="9e6f9-191">However, the mount time is extended upto a maximum of 24 hours in case of an ongoing file-copy.</span></span> <span data-ttu-id="9e6f9-192">當磁碟區處於掛接狀態時，不會執行任何備份作業。</span><span class="sxs-lookup"><span data-stu-id="9e6f9-192">No backup operations will run while the volume is mounted.</span></span> <span data-ttu-id="9e6f9-193">當掛接磁碟區時，任何排定要執行的備份作業會在復原磁碟區卸載之後才執行。</span><span class="sxs-lookup"><span data-stu-id="9e6f9-193">Any backup operation scheduled to run during the time when the volume is mounted, will run after the recovery volume is unmounted.</span></span>
    >

## <a name="troubleshooting"></a><span data-ttu-id="9e6f9-194">疑難排解</span><span class="sxs-lookup"><span data-stu-id="9e6f9-194">Troubleshooting</span></span>
<span data-ttu-id="9e6f9-195">如果即使按一下 [掛接] 數分鐘之後，Azure 備份仍未成功掛接復原磁碟區，或者無法掛接復原磁碟區且有一或多個錯誤，請遵循以下步驟來開始一般復原。</span><span class="sxs-lookup"><span data-stu-id="9e6f9-195">If Azure Backup does not successfully mount the recovery volume even after several minutes of clicking **Mount** or fails to mount the recovery volume with one or more errors, follow the steps below to begin recovering normally.</span></span>

1.  <span data-ttu-id="9e6f9-196">如果已執行數分鐘，請取消進行中的掛接程序。</span><span class="sxs-lookup"><span data-stu-id="9e6f9-196">Cancel the ongoing mount process in case it has been running for several minutes.</span></span>

2.  <span data-ttu-id="9e6f9-197">確認您使用最新版本的 Azure 備份代理程式。</span><span class="sxs-lookup"><span data-stu-id="9e6f9-197">Ensure that you are on the latest version of the Azure Backup agent.</span></span> <span data-ttu-id="9e6f9-198">若要了解 Azure 備份代理程式的版本資訊，按一下 Microsoft Azure 備份主控台之 [動作] 窗格中的 [關於 Microsoft Azure 復原服務代理程式]，並且確定**版本**號碼等於或高於[本文](https://go.microsoft.com/fwlink/?linkid=229525)中所述的版本。</span><span class="sxs-lookup"><span data-stu-id="9e6f9-198">To find out the version information of Azure Backup agent, click on **About Microsoft Azure Recovery Services Agent** on the **Actions** pane of Microsoft Azure Backup console and ensure that the **Version** number is equal to or higher than the version mentioned in [this article](https://go.microsoft.com/fwlink/?linkid=229525).</span></span> <span data-ttu-id="9e6f9-199">您可以從[這裡](https://go.microsoft.com/fwLink/?LinkID=288905)下載最新版本</span><span class="sxs-lookup"><span data-stu-id="9e6f9-199">You can download the latest version from [here](https://go.microsoft.com/fwLink/?LinkID=288905)</span></span>

3.  <span data-ttu-id="9e6f9-200">移至 [裝置管理員]  ->  [儲存體控制器]，並確保您可以找出 **Microsoft iSCSI 啟動器**。</span><span class="sxs-lookup"><span data-stu-id="9e6f9-200">Go to **Device Manager** -> **Storage Controllers** and ensure that you can locate **Microsoft iSCSI Initiator**.</span></span> <span data-ttu-id="9e6f9-201">如果您可以找到它，請直接前往以下的步驟 7。</span><span class="sxs-lookup"><span data-stu-id="9e6f9-201">If you can locate it, directly go to step 7 below.</span></span> 

4.  <span data-ttu-id="9e6f9-202">如果您無法如步驟 3 中所述，找到 Microsoft iSCSI 啟動器服務，請查看是否可以在名為 [不明裝置]、硬體識別碼為**ROOT\ISCSIPRT** 的 [裝置管理員]  ->  [儲存體控制器]項目。</span><span class="sxs-lookup"><span data-stu-id="9e6f9-202">If you cannot locate Microsoft iSCSI Initiator service as mentioned in step 3, check to see if you can find an entry under **Device Manager** -> **Storage Controllers** called **Unknown Device** with Hardware ID **ROOT\ISCSIPRT**.</span></span>

5.  <span data-ttu-id="9e6f9-203">以滑鼠右鍵按一下 [不明裝置]，然後選取 [更新驅動程式軟體]。</span><span class="sxs-lookup"><span data-stu-id="9e6f9-203">Right click on **Unknown Device** and select **Update Driver Software**.</span></span>

6.  <span data-ttu-id="9e6f9-204">藉由選取 [自動搜尋更新的驅動程式軟體] 的選項，以更新驅動程式。</span><span class="sxs-lookup"><span data-stu-id="9e6f9-204">Update the driver by selecting the option to  **Search automatically for updated driver software**.</span></span> <span data-ttu-id="9e6f9-205">完成更新應該會將 [不明裝置] 變更為 [Microsoft iSCSI 啟動器]如下所示。</span><span class="sxs-lookup"><span data-stu-id="9e6f9-205">Completion of the update should change **Unknown Device** to **Microsoft iSCSI Initiator** as shown below.</span></span> 

    ![加密](./media/backup-azure-restore-windows-server/UnknowniSCSIDevice.png)

7.  <span data-ttu-id="9e6f9-207">移至 [工作管理員]  ->  [服務 (本機)]  ->  [Microsoft iSCSI 啟動器服務]。</span><span class="sxs-lookup"><span data-stu-id="9e6f9-207">Go to **Task Manager** -> **Services (Local)** -> **Microsoft iSCSI Initiator Service**.</span></span> 

    ![加密](./media/backup-azure-restore-windows-server/MicrosoftInitiatorServiceRunning.png)
    
8.  <span data-ttu-id="9e6f9-209">以滑鼠右鍵按一下服務，以重新啟動 Microsoft iSCSI 啟動器服務，按一下 [停止] 並且再次以滑鼠右鍵按一下，然後按一下 [啟動]。</span><span class="sxs-lookup"><span data-stu-id="9e6f9-209">Restart the Microsoft iSCSI Initiator service by right-clicking on the service, clicking on **Stop** and further right clicking again and clicking on **Start**.</span></span>

9.  <span data-ttu-id="9e6f9-210">使用即時還原重試復原。</span><span class="sxs-lookup"><span data-stu-id="9e6f9-210">Retry recovering using Instant Restore.</span></span> 

<span data-ttu-id="9e6f9-211">如果復原仍然失敗，請重新啟動您的伺服器/用戶端。</span><span class="sxs-lookup"><span data-stu-id="9e6f9-211">If the recovery still fails, reboot your server/client.</span></span> <span data-ttu-id="9e6f9-212">如果不想要重新開機，或者即使在重新啟動伺服器之後復原仍然失敗，請嘗試從其他電腦復原，移至 [Azure 入口網站](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)連絡 Azure 支援並且提交支援要求。</span><span class="sxs-lookup"><span data-stu-id="9e6f9-212">If a reboot is not desirable or the recovery still fails even after rebooting the server, try recovering from an Alternate Machine, and contact Azure Support by going to [Azure Portal](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) and submitting a support request.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9e6f9-213">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9e6f9-213">Next steps</span></span>
* <span data-ttu-id="9e6f9-214">現在您已復原檔案和資料夾，接下來您可以 [管理您的備份](backup-azure-manage-windows-server.md)。</span><span class="sxs-lookup"><span data-stu-id="9e6f9-214">Now that you've recovered your files and folders, you can [manage your backups](backup-azure-manage-windows-server.md).</span></span>
