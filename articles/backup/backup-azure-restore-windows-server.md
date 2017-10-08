---
title: "aaaRestore 資料在 Azure tooa Windows Server 或 Windows 電腦 |Microsoft 文件"
description: "了解 toorestore 資料如何儲存在 Azure tooa Windows Server 或 Windows 電腦。"
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
ms.openlocfilehash: 11335495e448986a74f1733406f87e04331641d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="restore-files-tooa-windows-server-or-windows-client-machine-using-resource-manager-deployment-model"></a><span data-ttu-id="45a49-103">還原檔案 tooa Windows server 或 Windows 用戶端電腦使用資源管理員部署模型</span><span class="sxs-lookup"><span data-stu-id="45a49-103">Restore files tooa Windows server or Windows client machine using Resource Manager deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="45a49-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="45a49-104">Azure portal</span></span>](backup-azure-restore-windows-server.md)
> * [<span data-ttu-id="45a49-105">傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="45a49-105">Classic portal</span></span>](backup-azure-restore-windows-server-classic.md)
>
>

<span data-ttu-id="45a49-106">這篇文章說明如何從備份保存庫 toorestore 資料。</span><span class="sxs-lookup"><span data-stu-id="45a49-106">This article explains how toorestore data from a backup vault.</span></span> <span data-ttu-id="45a49-107">toorestore 資料，您會使用 hello 復原資料精靈在 hello Microsoft Azure 復原服務 」 (MARS) 代理程式。</span><span class="sxs-lookup"><span data-stu-id="45a49-107">toorestore data, you use hello Recover Data wizard in hello Microsoft Azure Recovery Services (MARS) agent.</span></span> <span data-ttu-id="45a49-108">當您還原資料時，您可以︰</span><span class="sxs-lookup"><span data-stu-id="45a49-108">When you restore data, it is possible to:</span></span>

* <span data-ttu-id="45a49-109">相同電腦中的 hello 備份還原資料 toohello 拍攝。</span><span class="sxs-lookup"><span data-stu-id="45a49-109">Restore data toohello same machine from which hello backups were taken.</span></span>
* <span data-ttu-id="45a49-110">還原資料 tooan 其他機器。</span><span class="sxs-lookup"><span data-stu-id="45a49-110">Restore data tooan alternate machine.</span></span>

<span data-ttu-id="45a49-111">年 1 月 2017，Microsoft 發行預覽更新 toohello MARS 代理程式。</span><span class="sxs-lookup"><span data-stu-id="45a49-111">In January 2017, Microsoft released a Preview update toohello MARS agent.</span></span> <span data-ttu-id="45a49-112">Bug 修正，以及這項更新啟用立即還原，可讓您 toomount 可寫入的復原點快照集以復原磁碟區。</span><span class="sxs-lookup"><span data-stu-id="45a49-112">Along with bug fixes, this update enables Instant Restore, which allows you toomount a writeable recovery point snapshot as a recovery volume.</span></span> <span data-ttu-id="45a49-113">然後，您可以瀏覽 hello 復原磁碟區並將複製檔案 tooa 本機電腦藉此選擇性地還原檔案。</span><span class="sxs-lookup"><span data-stu-id="45a49-113">You can then explore hello recovery volume and copy files tooa local computer thereby selectively restoring files.</span></span>

> [!NOTE]
> <span data-ttu-id="45a49-114">hello [2017 年 1 月更新 Azure Backup](https://support.microsoft.com/en-us/help/3216528?preview)如果您想要立即還原 toorestore 資料 toouse，則需要。</span><span class="sxs-lookup"><span data-stu-id="45a49-114">hello [January 2017 Azure Backup update](https://support.microsoft.com/en-us/help/3216528?preview) is required if you want toouse Instant Restore toorestore data.</span></span> <span data-ttu-id="45a49-115">也在保存庫在 hello 技術支援文件中所列的地區設定必須加以保護 hello 備份資料。</span><span class="sxs-lookup"><span data-stu-id="45a49-115">Also hello backup data must be protected in vaults in locales listed in hello support article.</span></span> <span data-ttu-id="45a49-116">請參閱 hello [2017 年 1 月更新 Azure Backup](https://support.microsoft.com/en-us/help/3216528?preview) hello 支援 立即還原的地區設定的最新的清單。</span><span class="sxs-lookup"><span data-stu-id="45a49-116">Consult hello [January 2017 Azure Backup update](https://support.microsoft.com/en-us/help/3216528?preview) for hello latest list of locales that support Instant Restore.</span></span> <span data-ttu-id="45a49-117">「立即還原」目前**無法**在所有地區設定中使用。</span><span class="sxs-lookup"><span data-stu-id="45a49-117">Instant Restore is **not** currently available in all locales.</span></span>
>

<span data-ttu-id="45a49-118">立即還原適用於在 hello Azure 入口網站中的 復原服務保存庫中使用與備份保存庫 hello 傳統入口網站中。</span><span class="sxs-lookup"><span data-stu-id="45a49-118">Instant Restore is available for use in Recovery Services vaults in hello Azure portal and Backup vaults in hello classic portal.</span></span> <span data-ttu-id="45a49-119">如果您想 toouse 立即還原，下載 hello MARS 更新，並遵循提到立即還原 hello 程序。</span><span class="sxs-lookup"><span data-stu-id="45a49-119">If you want toouse Instant Restore, download hello MARS update, and follow hello procedures that mention Instant Restore.</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="use-instant-restore-toorecover-data-toohello-same-machine"></a><span data-ttu-id="45a49-120">使用 立即還原 toorecover 資料 toohello 同一部電腦</span><span class="sxs-lookup"><span data-stu-id="45a49-120">Use Instant Restore toorecover data toohello same machine</span></span>

<span data-ttu-id="45a49-121">如果您不小心刪除了檔案，並且想 toorestore 它 toohello 同一部電腦 （從哪些 hello 備份），hello 下列步驟將協助您復原 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="45a49-121">If you accidentally deleted a file and wish toorestore it toohello same machine (from which hello backup is taken), hello following steps will help you recover hello data.</span></span>

1. <span data-ttu-id="45a49-122">開啟 hello **Microsoft Azure 備份**中對齊。</span><span class="sxs-lookup"><span data-stu-id="45a49-122">Open hello **Microsoft Azure Backup** snap in.</span></span> <span data-ttu-id="45a49-123">如果您不知道 hello 嵌入式管理單元安裝所在，搜尋 hello 電腦或伺服器**Microsoft Azure 備份**。</span><span class="sxs-lookup"><span data-stu-id="45a49-123">If you don't know where hello snap in was installed, search hello computer or server for **Microsoft Azure Backup**.</span></span>

    <span data-ttu-id="45a49-124">hello 桌面應用程式應該會出現在 hello 搜尋結果中。</span><span class="sxs-lookup"><span data-stu-id="45a49-124">hello desktop app should appear in hello search results.</span></span>

2. <span data-ttu-id="45a49-125">按一下**復原資料**toostart hello 精靈。</span><span class="sxs-lookup"><span data-stu-id="45a49-125">Click **Recover Data** toostart hello wizard.</span></span>

    ![復原資料](./media/backup-azure-restore-windows-server/recover.png)

3. <span data-ttu-id="45a49-127">Hello 上**入門**窗格中，toorestore hello 資料 toohello 相同伺服器或電腦上，選取**這部伺服器 (`<server name>`)**按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="45a49-127">On hello **Getting Started** pane, toorestore hello data toohello same server or computer, select **This server (`<server name>`)** and click **Next**.</span></span>

    ![選擇此伺服器選項 toorestore hello 資料 toohello 同一部電腦](./media/backup-azure-restore-windows-server/samemachine_gettingstarted_instantrestore.png)

4. <span data-ttu-id="45a49-129">在 hello**選取復原模式** 窗格中，選擇**個別檔案及資料夾**，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="45a49-129">On hello **Select Recovery Mode** pane, choose **Individual files and folders** and then click **Next**.</span></span>

    ![瀏覽檔案](./media/backup-azure-restore-windows-server/samemachine_selectrecoverymode_instantrestore.png)

5. <span data-ttu-id="45a49-131">在 hello**選取磁碟區和日期**窗格中，選取 hello 磁碟區，其中包含 hello 檔案及/或您想要 toorestore 的資料夾。</span><span class="sxs-lookup"><span data-stu-id="45a49-131">On hello **Select Volume and Date** pane, select hello volume that contains hello files and/or folders you want toorestore.</span></span>

    <span data-ttu-id="45a49-132">Hello 日曆上選取的復原點。</span><span class="sxs-lookup"><span data-stu-id="45a49-132">On hello calendar, select a recovery point.</span></span> <span data-ttu-id="45a49-133">您可以從任何時間的復原點還原。</span><span class="sxs-lookup"><span data-stu-id="45a49-133">You can restore from any recovery point in time.</span></span> <span data-ttu-id="45a49-134">日期**粗體**表示 hello 至少一個復原點的可用性。</span><span class="sxs-lookup"><span data-stu-id="45a49-134">Dates in **bold** indicate hello availability of at least one recovery point.</span></span> <span data-ttu-id="45a49-135">一旦您選取日期，如果有多個復原點可用，請選擇 hello 特定的復原點從 hello**時間**下拉式功能表。</span><span class="sxs-lookup"><span data-stu-id="45a49-135">Once you select a date, if multiple recovery points are available, choose hello specific recovery point from hello **Time** drop-down menu.</span></span>

    ![磁碟區和日期](./media/backup-azure-restore-windows-server/samemachine_selectvolumedate_instantrestore.png)

6. <span data-ttu-id="45a49-137">一旦您已選擇 hello 復原點 toorestore，按一下 **掛接**。</span><span class="sxs-lookup"><span data-stu-id="45a49-137">Once you have chosen hello recovery point toorestore, click **Mount**.</span></span>

    <span data-ttu-id="45a49-138">Azure 備份掛接 hello 本機復原點，並使用它做為復原磁碟區。</span><span class="sxs-lookup"><span data-stu-id="45a49-138">Azure Backup mounts hello local recovery point, and uses it as a recovery volume.</span></span>

7. <span data-ttu-id="45a49-139">在 hello**瀏覽和復原檔案** 窗格中，按一下 **瀏覽**想 tooopen Windows 檔案總管 並尋找 hello 檔案及資料夾。</span><span class="sxs-lookup"><span data-stu-id="45a49-139">On hello **Browse and Recover Files** pane, click **Browse** tooopen Windows Explorer and find hello files and folders you want.</span></span>

    ![修復選項](./media/backup-azure-restore-windows-server/samemachine_browserecover_instantrestore.png)


8. <span data-ttu-id="45a49-141">在 Windows 檔案總管 中，複製 hello 檔案及/或資料夾想 toorestore，並將它們貼 tooany 位置 toohello 本機伺服器或電腦。</span><span class="sxs-lookup"><span data-stu-id="45a49-141">In Windows Explorer, copy hello files and/or folders you want toorestore and paste them tooany location local toohello server or computer.</span></span> <span data-ttu-id="45a49-142">您可以開啟或資料流 hello 檔案直接從 hello 復原磁碟區，並確認 hello 正確版本會復原。</span><span class="sxs-lookup"><span data-stu-id="45a49-142">You can open or stream hello files directly from hello recovery volume and verify hello correct versions are recovered.</span></span>

    ![複製並貼上檔案和資料夾從掛接的磁碟區 toolocal 位置](./media/backup-azure-restore-windows-server/samemachine_copy_instantrestore.png)

9. <span data-ttu-id="45a49-144">完成還原 hello 檔案及/或資料夾，在 hello**瀏覽和修復檔案** 窗格中，按一下 **卸載**。</span><span class="sxs-lookup"><span data-stu-id="45a49-144">When you are finished restoring hello files and/or folders, on hello **Browse and Recovery Files** pane, click **Unmount**.</span></span> <span data-ttu-id="45a49-145">然後按一下 **是**tooconfirm 想 toounmount hello 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="45a49-145">Then click **Yes** tooconfirm that you want toounmount hello volume.</span></span>

    ![取消掛接 hello 磁碟區，並確認](./media/backup-azure-restore-windows-server/samemachine_unmount_instantrestore.png)

    > [!Important]
    > <span data-ttu-id="45a49-147">如果您沒有按一下 取消掛接，hello 復原磁碟區會保持已掛接 hello 裝載時的時間從 6 小時。</span><span class="sxs-lookup"><span data-stu-id="45a49-147">If you do not click Unmount, hello Recovery Volume will remain mounted for 6 hours from hello time when it was mounted.</span></span> <span data-ttu-id="45a49-148">不過，hello 掛接時間是擴充高達 24 小時內進行中的檔案複製時的最大值。</span><span class="sxs-lookup"><span data-stu-id="45a49-148">However, hello mount time is extended upto a maximum of 24 hours in case of an ongoing file-copy.</span></span> <span data-ttu-id="45a49-149">掛上 hello 磁碟區時，將會不執行任何備份作業。</span><span class="sxs-lookup"><span data-stu-id="45a49-149">No backup operations will run while hello volume is mounted.</span></span> <span data-ttu-id="45a49-150">Hello 復原磁碟區未裝載任何的排程備份作業 toorun 期間 hello 當 hello 掛上磁碟區，會執行。</span><span class="sxs-lookup"><span data-stu-id="45a49-150">Any backup operation scheduled toorun during hello time when hello volume is mounted, will run after hello recovery volume is unmounted.</span></span>
    >


## <a name="use-instant-restore-toorestore-data-tooan-alternate-machine"></a><span data-ttu-id="45a49-151">使用 立即還原 toorestore 資料 tooan 替代機器</span><span class="sxs-lookup"><span data-stu-id="45a49-151">Use Instant Restore toorestore data tooan alternate machine</span></span>
<span data-ttu-id="45a49-152">整個伺服器遺失時，您仍然可以從 Azure Backup tooa 不同電腦中復原資料。</span><span class="sxs-lookup"><span data-stu-id="45a49-152">If your entire server is lost, you can still recover data from Azure Backup tooa different machine.</span></span> <span data-ttu-id="45a49-153">hello 下列步驟說明 hello 工作流程。</span><span class="sxs-lookup"><span data-stu-id="45a49-153">hello following steps illustrate hello workflow.</span></span>


<span data-ttu-id="45a49-154">包含下列步驟中所使用的 hello 術語：</span><span class="sxs-lookup"><span data-stu-id="45a49-154">hello terminology used in these steps includes:</span></span>

* <span data-ttu-id="45a49-155">*來源機器*– 拍攝 hello 從哪個 hello 備份的原始電腦，這是目前無法使用。</span><span class="sxs-lookup"><span data-stu-id="45a49-155">*Source machine* – hello original machine from which hello backup was taken and which is currently unavailable.</span></span>
* <span data-ttu-id="45a49-156">*目標電腦*– hello 機器 toowhich hello 資料要復原的目的地。</span><span class="sxs-lookup"><span data-stu-id="45a49-156">*Target machine* – hello machine toowhich hello data is being recovered.</span></span>
* <span data-ttu-id="45a49-157">*範例保存庫*– hello 復原服務保存庫 toowhich hello*來源機器*和*目標機器*註冊。</span><span class="sxs-lookup"><span data-stu-id="45a49-157">*Sample vault* – hello Recovery Services vault toowhich hello *Source machine* and *Target machine* are registered.</span></span> <br/>

> [!NOTE]
> <span data-ttu-id="45a49-158">備份無法還原的 tooa 目標電腦執行舊版的 hello 作業系統。</span><span class="sxs-lookup"><span data-stu-id="45a49-158">Backups can't be restored tooa target machine running an earlier version of hello operating system.</span></span> <span data-ttu-id="45a49-159">例如，從 Windows 7 電腦建立的備份可以還原至 Windows 8 或更新版本的電腦。</span><span class="sxs-lookup"><span data-stu-id="45a49-159">For example, a backup taken from a Windows 7 computer can be restored on a Windows 8, or later, computer.</span></span> <span data-ttu-id="45a49-160">執行 Windows 8 電腦的備份無法還原的 tooa Windows 7 電腦。</span><span class="sxs-lookup"><span data-stu-id="45a49-160">A backup taken from a Windows 8 computer cannot be restored tooa Windows 7 computer.</span></span>
>
>

1. <span data-ttu-id="45a49-161">開啟 hello **Microsoft Azure 備份**在 hello 上對齊*目標機器*。</span><span class="sxs-lookup"><span data-stu-id="45a49-161">Open hello **Microsoft Azure Backup** snap in on hello *Target machine*.</span></span>

2. <span data-ttu-id="45a49-162">請確定 hello*目標電腦*和 hello*來源機器*是相同的復原服務保存庫註冊的 toohello。</span><span class="sxs-lookup"><span data-stu-id="45a49-162">Ensure hello *Target machine* and hello *Source machine* are registered toohello same Recovery Services vault.</span></span>

3. <span data-ttu-id="45a49-163">按一下**復原資料**tooopen hello**復原資料精靈**。</span><span class="sxs-lookup"><span data-stu-id="45a49-163">Click **Recover Data** tooopen hello **Recover Data wizard**.</span></span>

    ![復原資料](./media/backup-azure-restore-windows-server/recover.png)

4. <span data-ttu-id="45a49-165">在 hello**入門**窗格中，選取**另一部伺服器**</span><span class="sxs-lookup"><span data-stu-id="45a49-165">On hello **Getting Started** pane, select **Another server**</span></span>

    ![其他伺服器](./media/backup-azure-restore-windows-server/alternatemachine_gettingstarted_instantrestore.png)

5. <span data-ttu-id="45a49-167">提供對應 toohello hello 保存庫認證檔案*範例保存庫*，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="45a49-167">Provide hello vault credential file that corresponds toohello *Sample vault*, and click **Next**.</span></span>

    <span data-ttu-id="45a49-168">如果 hello 保存庫認證檔案無效 （或已過期），下載新的保存庫認證檔案從 hello*範例保存庫*hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="45a49-168">If hello vault credential file is invalid (or expired), download a new vault credential file from hello *Sample vault* in hello Azure portal.</span></span> <span data-ttu-id="45a49-169">一旦您提供有效的保存庫認證，hello 的 hello 對應的備份保存庫會出現的名稱。</span><span class="sxs-lookup"><span data-stu-id="45a49-169">Once you provide a valid vault credential, hello name of hello corresponding Backup Vault appears.</span></span>


6. <span data-ttu-id="45a49-170">在 hello**選取備份伺服器**窗格中，選取 hello*來源機器*從 hello 清單中顯示的機器，並提供 hello 複雜密碼。</span><span class="sxs-lookup"><span data-stu-id="45a49-170">On hello **Select Backup Server** pane, select hello *Source machine* from hello list of displayed machines and provide hello passphrase.</span></span> <span data-ttu-id="45a49-171">然後按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="45a49-171">Then click **Next**.</span></span>

    ![電腦清單](./media/backup-azure-restore-windows-server/alternatemachine_selectmachine_instantrestore.png)

7. <span data-ttu-id="45a49-173">在 hello**選取復原模式**窗格中，選取**個別檔案及資料夾**按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="45a49-173">On hello **Select Recovery Mode** pane, select **Individual files and folders** and click **Next**.</span></span>

    ![搜尋](./media/backup-azure-restore-windows-server/alternatemachine_selectrecoverymode_instantrestore.png)

8. <span data-ttu-id="45a49-175">在 hello**選取磁碟區和日期**窗格中，選取 hello 磁碟區，其中包含 hello 檔案及/或您想要 toorestore 的資料夾。</span><span class="sxs-lookup"><span data-stu-id="45a49-175">On hello **Select Volume and Date** pane, select hello volume that contains hello files and/or folders you want toorestore.</span></span>

    <span data-ttu-id="45a49-176">Hello 日曆上選取的復原點。</span><span class="sxs-lookup"><span data-stu-id="45a49-176">On hello calendar, select a recovery point.</span></span> <span data-ttu-id="45a49-177">您可以從任何時間的復原點還原。</span><span class="sxs-lookup"><span data-stu-id="45a49-177">You can restore from any recovery point in time.</span></span> <span data-ttu-id="45a49-178">日期**粗體**表示 hello 至少一個復原點的可用性。</span><span class="sxs-lookup"><span data-stu-id="45a49-178">Dates in **bold** indicate hello availability of at least one recovery point.</span></span> <span data-ttu-id="45a49-179">一旦您選取日期，如果有多個復原點可用，請選擇 hello 特定的復原點從 hello**時間**下拉式功能表。</span><span class="sxs-lookup"><span data-stu-id="45a49-179">Once you select a date, if multiple recovery points are available, choose hello specific recovery point from hello **Time** drop-down menu.</span></span>

    ![搜尋項目](./media/backup-azure-restore-windows-server/alternatemachine_selectvolumedate_instantrestore.png)

9. <span data-ttu-id="45a49-181">按一下**掛接**toolocally 掛接 hello 復原點復原磁碟區上為您*目標機器*。</span><span class="sxs-lookup"><span data-stu-id="45a49-181">Click **Mount** toolocally mount hello recovery point as a recovery volume on your *Target machine*.</span></span>

10. <span data-ttu-id="45a49-182">在 hello**瀏覽和復原檔案** 窗格中，按一下 **瀏覽**想 tooopen Windows 檔案總管 並尋找 hello 檔案及資料夾。</span><span class="sxs-lookup"><span data-stu-id="45a49-182">On hello **Browse and Recover Files** pane, click **Browse** tooopen Windows Explorer and find hello files and folders you want.</span></span>

    ![加密](./media/backup-azure-restore-windows-server/alternatemachine_browserecover_instantrestore.png)

11. <span data-ttu-id="45a49-184">在 Windows 檔案總管中，將複製 hello 檔案及/或資料夾從 hello 復原磁碟區並貼 tooyour*目標機器*位置。</span><span class="sxs-lookup"><span data-stu-id="45a49-184">In Windows Explorer, copy hello files and/or folders from hello recovery volume and paste them tooyour *Target machine* location.</span></span> <span data-ttu-id="45a49-185">您可以開啟或資料流 hello 檔案直接從 hello 復原磁碟區，並確認 hello 正確版本會復原。</span><span class="sxs-lookup"><span data-stu-id="45a49-185">You can open or stream hello files directly from hello recovery volume and verify hello correct versions are recovered.</span></span>

    ![加密](./media/backup-azure-restore-windows-server/alternatemachine_copy_instantrestore.png)

12. <span data-ttu-id="45a49-187">完成還原 hello 檔案及/或資料夾，在 hello**瀏覽和修復檔案** 窗格中，按一下 **卸載**。</span><span class="sxs-lookup"><span data-stu-id="45a49-187">When you are finished restoring hello files and/or folders, on hello **Browse and Recovery Files** pane, click **Unmount**.</span></span> <span data-ttu-id="45a49-188">然後按一下 **是**tooconfirm 想 toounmount hello 磁碟區。</span><span class="sxs-lookup"><span data-stu-id="45a49-188">Then click **Yes** tooconfirm that you want toounmount hello volume.</span></span>

    ![加密](./media/backup-azure-restore-windows-server/alternatemachine_unmount_instantrestore.png)

    > [!Important]
    > <span data-ttu-id="45a49-190">如果您沒有按一下 取消掛接，hello 復原磁碟區會保持已掛接 hello 裝載時的時間從 6 小時。</span><span class="sxs-lookup"><span data-stu-id="45a49-190">If you do not click Unmount, hello Recovery Volume will remain mounted for 6 hours from hello time when it was mounted.</span></span> <span data-ttu-id="45a49-191">不過，hello 掛接時間是擴充高達 24 小時內進行中的檔案複製時的最大值。</span><span class="sxs-lookup"><span data-stu-id="45a49-191">However, hello mount time is extended upto a maximum of 24 hours in case of an ongoing file-copy.</span></span> <span data-ttu-id="45a49-192">掛上 hello 磁碟區時，將會不執行任何備份作業。</span><span class="sxs-lookup"><span data-stu-id="45a49-192">No backup operations will run while hello volume is mounted.</span></span> <span data-ttu-id="45a49-193">Hello 復原磁碟區未裝載任何的排程備份作業 toorun 期間 hello 當 hello 掛上磁碟區，會執行。</span><span class="sxs-lookup"><span data-stu-id="45a49-193">Any backup operation scheduled toorun during hello time when hello volume is mounted, will run after hello recovery volume is unmounted.</span></span>
    >

## <a name="troubleshooting"></a><span data-ttu-id="45a49-194">疑難排解</span><span class="sxs-lookup"><span data-stu-id="45a49-194">Troubleshooting</span></span>
<span data-ttu-id="45a49-195">如果 Azure 備份不成功掛接 hello 復原磁碟區的按一下的幾分鐘後，即使**掛接**或失敗 toomount hello 復原磁碟區與一個或多個錯誤，請遵循 hello toobegin 通常復原步驟。</span><span class="sxs-lookup"><span data-stu-id="45a49-195">If Azure Backup does not successfully mount hello recovery volume even after several minutes of clicking **Mount** or fails toomount hello recovery volume with one or more errors, follow hello steps below toobegin recovering normally.</span></span>

1.  <span data-ttu-id="45a49-196">如果已執行數分鐘，請取消 hello 持續掛接程序。</span><span class="sxs-lookup"><span data-stu-id="45a49-196">Cancel hello ongoing mount process in case it has been running for several minutes.</span></span>

2.  <span data-ttu-id="45a49-197">確認您是在 hello hello Azure 備份代理程式的最新版本。</span><span class="sxs-lookup"><span data-stu-id="45a49-197">Ensure that you are on hello latest version of hello Azure Backup agent.</span></span> <span data-ttu-id="45a49-198">toofind hello 版本資訊的 Azure 備份代理程式，按一下 **有關 Microsoft Azure Recovery Services Agent**上 hello**動作**窗格中的 Microsoft Azure Backup 主控台，並確保該 hello **版本**數字是相等 tooor 高於 hello 版本中所述[本文](https://go.microsoft.com/fwlink/?linkid=229525)。</span><span class="sxs-lookup"><span data-stu-id="45a49-198">toofind out hello version information of Azure Backup agent, click on **About Microsoft Azure Recovery Services Agent** on hello **Actions** pane of Microsoft Azure Backup console and ensure that hello **Version** number is equal tooor higher than hello version mentioned in [this article](https://go.microsoft.com/fwlink/?linkid=229525).</span></span> <span data-ttu-id="45a49-199">您可以下載從 hello 最新版本[這裡](https://go.microsoft.com/fwLink/?LinkID=288905)</span><span class="sxs-lookup"><span data-stu-id="45a49-199">You can download hello latest version from [here](https://go.microsoft.com/fwLink/?LinkID=288905)</span></span>

3.  <span data-ttu-id="45a49-200">跳過**裝置管理員** -> **存放裝置控制器**，並確保您可以找出**Microsoft iSCSI 啟動器**。</span><span class="sxs-lookup"><span data-stu-id="45a49-200">Go too**Device Manager** -> **Storage Controllers** and ensure that you can locate **Microsoft iSCSI Initiator**.</span></span> <span data-ttu-id="45a49-201">如果您可以找到它，直接移 toostep 7。</span><span class="sxs-lookup"><span data-stu-id="45a49-201">If you can locate it, directly go toostep 7 below.</span></span> 

4.  <span data-ttu-id="45a49-202">如果您無法找出 Microsoft iSCSI 啟動器服務，如步驟 3 中所述，檢查 toosee 是否可以尋找下的一個項目**裝置管理員** -> **存放裝置控制器**呼叫**無法辨識的裝置**硬體識別碼**ROOT\ISCSIPRT**。</span><span class="sxs-lookup"><span data-stu-id="45a49-202">If you cannot locate Microsoft iSCSI Initiator service as mentioned in step 3, check toosee if you can find an entry under **Device Manager** -> **Storage Controllers** called **Unknown Device** with Hardware ID **ROOT\ISCSIPRT**.</span></span>

5.  <span data-ttu-id="45a49-203">以滑鼠右鍵按一下 [不明裝置]，然後選取 [更新驅動程式軟體]。</span><span class="sxs-lookup"><span data-stu-id="45a49-203">Right click on **Unknown Device** and select **Update Driver Software**.</span></span>

6.  <span data-ttu-id="45a49-204">更新 hello 驅動程式選取 hello 選項太**自動搜尋更新的驅動程式軟體**。</span><span class="sxs-lookup"><span data-stu-id="45a49-204">Update hello driver by selecting hello option too **Search automatically for updated driver software**.</span></span> <span data-ttu-id="45a49-205">應該在變更完成 hello 更新**不明裝置**太**Microsoft iSCSI 啟動器**如下所示。</span><span class="sxs-lookup"><span data-stu-id="45a49-205">Completion of hello update should change **Unknown Device** too**Microsoft iSCSI Initiator** as shown below.</span></span> 

    ![加密](./media/backup-azure-restore-windows-server/UnknowniSCSIDevice.png)

7.  <span data-ttu-id="45a49-207">跳過**工作管理員** -> **服務 （本機）** -> **Microsoft iSCSI 啟動器服務**。</span><span class="sxs-lookup"><span data-stu-id="45a49-207">Go too**Task Manager** -> **Services (Local)** -> **Microsoft iSCSI Initiator Service**.</span></span> 

    ![加密](./media/backup-azure-restore-windows-server/MicrosoftInitiatorServiceRunning.png)
    
8.  <span data-ttu-id="45a49-209">以滑鼠右鍵按一下 hello 服務，按一下 重新啟動 hello Microsoft iSCSI 啟動器服務**停止**和進一步再次以滑鼠右鍵按一下，並按一下**啟動**。</span><span class="sxs-lookup"><span data-stu-id="45a49-209">Restart hello Microsoft iSCSI Initiator service by right-clicking on hello service, clicking on **Stop** and further right clicking again and clicking on **Start**.</span></span>

9.  <span data-ttu-id="45a49-210">使用即時還原重試復原。</span><span class="sxs-lookup"><span data-stu-id="45a49-210">Retry recovering using Instant Restore.</span></span> 

<span data-ttu-id="45a49-211">如果 hello 復原仍然失敗，請重新啟動您的伺服器/用戶端。</span><span class="sxs-lookup"><span data-stu-id="45a49-211">If hello recovery still fails, reboot your server/client.</span></span> <span data-ttu-id="45a49-212">如果不想要重新開機或 hello 復原仍然失敗甚至 hello 伺服器重新啟動之後，嘗試從其他機器，復原，並連絡 Azure 支援太移[Azure 入口網站](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)和提交支援要求。</span><span class="sxs-lookup"><span data-stu-id="45a49-212">If a reboot is not desirable or hello recovery still fails even after rebooting hello server, try recovering from an Alternate Machine, and contact Azure Support by going too[Azure Portal](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) and submitting a support request.</span></span>

## <a name="next-steps"></a><span data-ttu-id="45a49-213">後續步驟</span><span class="sxs-lookup"><span data-stu-id="45a49-213">Next steps</span></span>
* <span data-ttu-id="45a49-214">現在您已復原檔案和資料夾，接下來您可以 [管理您的備份](backup-azure-manage-windows-server.md)。</span><span class="sxs-lookup"><span data-stu-id="45a49-214">Now that you've recovered your files and folders, you can [manage your backups](backup-azure-manage-windows-server.md).</span></span>
