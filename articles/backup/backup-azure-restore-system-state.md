---
title: "Azure 備份： Windows Server 還原系統狀態 tooa |Microsoft 文件"
description: "如何從 Azure 中的備份來還原 Windows Server 系統狀態的逐步解說。"
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: 
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/18/2017
ms.author: saurse;trinadhk;markgal;
ms.openlocfilehash: a45506507f53e2744350d3b6b2e52f1db415de4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="restore-system-state-toowindows-server"></a><span data-ttu-id="2f296-103">還原系統狀態 tooWindows 伺服器</span><span class="sxs-lookup"><span data-stu-id="2f296-103">Restore System State tooWindows Server</span></span>

<span data-ttu-id="2f296-104">本文說明如何從 Azure 復原服務 toorestore Windows 伺服器系統狀態備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="2f296-104">This article explains how toorestore Windows Server System State backups from an Azure Recovery Services vault.</span></span> <span data-ttu-id="2f296-105">toorestore 系統狀態，您必須有系統狀態備份 (使用中的 hello 指示建立[備份系統狀態](backup-azure-system-state.md#back-up-windows-server-system-state-preview))，並確定您已安裝 hello[最新版本的 Microsoft Azure Recovery hello服務 (MARS) 代理程式](http://aka.ms/azurebackup_agent)。</span><span class="sxs-lookup"><span data-stu-id="2f296-105">toorestore System State, you must have a System State backup (created using hello instructions in [Back up System State](backup-azure-system-state.md#back-up-windows-server-system-state-preview)), and make sure you have installed hello [latest version of hello Microsoft Azure Recovery Services (MARS) agent](http://aka.ms/azurebackup_agent).</span></span> <span data-ttu-id="2f296-106">從 Azure 復原服務保存庫來復原 Windows Server 系統狀態資料的程序需要兩個步驟：</span><span class="sxs-lookup"><span data-stu-id="2f296-106">Recovering Windows Server System State data from an Azure Recovery Services vault is a two-step process:</span></span>

1. <span data-ttu-id="2f296-107">從 Azure 備份來還原檔案形式的系統狀態。</span><span class="sxs-lookup"><span data-stu-id="2f296-107">Restore System State as files from Azure Backup.</span></span> <span data-ttu-id="2f296-108">在從 Azure 備份來還原檔案形式的系統狀態時，您可以：</span><span class="sxs-lookup"><span data-stu-id="2f296-108">When restoring System State as files from Azure Backup, you can either:</span></span>
  * <span data-ttu-id="2f296-109">還原系統狀態 toohello 相同的伺服器，其中 hello 備份在進行，或</span><span class="sxs-lookup"><span data-stu-id="2f296-109">Restore System State toohello same server where hello backups were taken, or</span></span>
  * <span data-ttu-id="2f296-110">還原系統狀態檔案 tooan 替代伺服器。</span><span class="sxs-lookup"><span data-stu-id="2f296-110">Restore System State file tooan alternate server.</span></span>

2. <span data-ttu-id="2f296-111">適用於 hello 還原系統狀態檔案 tooa Windows 伺服器。</span><span class="sxs-lookup"><span data-stu-id="2f296-111">Apply hello restored System State files tooa Windows Server.</span></span>


## <a name="recover-system-state-files-toohello-same-server"></a><span data-ttu-id="2f296-112">復原系統狀態檔案 toohello 相同的伺服器</span><span class="sxs-lookup"><span data-stu-id="2f296-112">Recover System State files toohello same server</span></span>
<span data-ttu-id="2f296-113">hello 下列步驟說明如何 tooroll 回您 Windows Server 設定 tooa 先前的狀態。</span><span class="sxs-lookup"><span data-stu-id="2f296-113">hello following steps explain how tooroll back your Windows Server configuration tooa previous state.</span></span> <span data-ttu-id="2f296-114">復原您的伺服器設定後 tooa 已知，穩定的狀態，可以是非常重要。</span><span class="sxs-lookup"><span data-stu-id="2f296-114">Rolling your server configuration back tooa known, stable state, can be extremely valuable.</span></span> <span data-ttu-id="2f296-115">hello 復原服務保存庫中的下列步驟還原 hello 伺服器的系統狀態。</span><span class="sxs-lookup"><span data-stu-id="2f296-115">hello following steps restore hello server's System State from a Recovery Services vault.</span></span> 

1. <span data-ttu-id="2f296-116">開啟 hello **Microsoft Azure 備份**嵌入式管理單元。</span><span class="sxs-lookup"><span data-stu-id="2f296-116">Open hello **Microsoft Azure Backup** snap-in.</span></span> <span data-ttu-id="2f296-117">如果您不知道 hello 嵌入式管理單元安裝所在，搜尋 hello 電腦或伺服器**Microsoft Azure 備份**。</span><span class="sxs-lookup"><span data-stu-id="2f296-117">If you don't know where hello snap-in was installed, search hello computer or server for **Microsoft Azure Backup**.</span></span>

    <span data-ttu-id="2f296-118">hello 桌面應用程式應該會出現在 hello 搜尋結果中。</span><span class="sxs-lookup"><span data-stu-id="2f296-118">hello desktop app should appear in hello search results.</span></span>

2. <span data-ttu-id="2f296-119">按一下**復原資料**toostart hello 精靈。</span><span class="sxs-lookup"><span data-stu-id="2f296-119">Click **Recover Data** toostart hello wizard.</span></span>

    ![復原資料](./media/backup-azure-restore-windows-server/recover.png)

3. <span data-ttu-id="2f296-121">Hello 上**入門**窗格中，toorestore hello 資料 toohello 相同伺服器或電腦上，選取**這部伺服器 (`<server name>`)**按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="2f296-121">On hello **Getting Started** pane, toorestore hello data toohello same server or computer, select **This server (`<server name>`)** and click **Next**.</span></span>

    ![選擇此伺服器選項 toorestore hello 資料 toohello 同一部電腦](./media/backup-azure-restore-system-state/samemachine.png)

4. <span data-ttu-id="2f296-123">在 [hello**選取復原模式**] 窗格中，選擇**系統狀態**，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="2f296-123">On hello **Select Recovery Mode** pane, choose **System State** and then click **Next**.</span></span>

    ![瀏覽檔案](./media/backup-azure-restore-system-state/recover-type-selection.png)

5. <span data-ttu-id="2f296-125">中的 hello 行事曆上**選取磁碟區和日期**窗格中，選取復原點。</span><span class="sxs-lookup"><span data-stu-id="2f296-125">On hello calendar in **Select Volume and Date** pane, select a recovery point.</span></span> 

    <span data-ttu-id="2f296-126">您可以從任何時間的復原點還原。</span><span class="sxs-lookup"><span data-stu-id="2f296-126">You can restore from any recovery point in time.</span></span> <span data-ttu-id="2f296-127">日期**粗體**表示 hello 至少一個復原點的可用性。</span><span class="sxs-lookup"><span data-stu-id="2f296-127">Dates in **bold** indicate hello availability of at least one recovery point.</span></span> <span data-ttu-id="2f296-128">一旦您選取日期，如果有多個復原點可用，請選擇 hello 特定的復原點從 hello**時間**下拉式功能表。</span><span class="sxs-lookup"><span data-stu-id="2f296-128">Once you select a date, if multiple recovery points are available, choose hello specific recovery point from hello **Time** drop-down menu.</span></span>

    ![磁碟區和日期](./media/backup-azure-restore-system-state/select-date.png)

6. <span data-ttu-id="2f296-130">一旦您已選擇 hello 復原點 toorestore，按一下 **下一步**。</span><span class="sxs-lookup"><span data-stu-id="2f296-130">Once you have chosen hello recovery point toorestore, click **Next**.</span></span>

    <span data-ttu-id="2f296-131">Azure 備份掛接 hello 本機復原點，並使用它做為復原磁碟區。</span><span class="sxs-lookup"><span data-stu-id="2f296-131">Azure Backup mounts hello local recovery point, and uses it as a recovery volume.</span></span>

7. <span data-ttu-id="2f296-132">在 hello 下一步 窗格中，指定 hello 的 hello 目的地復原系統狀態檔案，然後按一下**瀏覽**想 tooopen Windows 檔案總管 並尋找 hello 檔案及資料夾。</span><span class="sxs-lookup"><span data-stu-id="2f296-132">On hello next pane, specify hello destination for hello recovered System State files and click **Browse** tooopen Windows Explorer and find hello files and folders you want.</span></span> <span data-ttu-id="2f296-133">hello 選項，**建立複本，以擁有兩個版本**，而不是建立 hello 副本 hello 整個系統的狀態保存現有系統狀態檔案封存中建立個別的檔案複製。</span><span class="sxs-lookup"><span data-stu-id="2f296-133">hello option, **Create copies so that you have both versions**, creates copies of individual files in an existing System State file archive instead of creating hello copy of hello entire System State archive.</span></span>

    ![修復選項](./media/backup-azure-restore-system-state/recover-as-files.png)

8. <span data-ttu-id="2f296-135">請確認 hello 詳細資料的復原在 hello**確認**按一下**復原**。</span><span class="sxs-lookup"><span data-stu-id="2f296-135">Verify hello details of recovery on hello **Confirmation** pane and click **Recover**.</span></span>

   ![按一下 復原 tooacknowledge hello 復原動作](./media/backup-azure-restore-system-state/confirm-recovery.png)

9. <span data-ttu-id="2f296-137">複製 hello *WindowsImageBackup*目錄 hello 復原目的地 tooa 非重要磁碟區的 hello 伺服器中。</span><span class="sxs-lookup"><span data-stu-id="2f296-137">Copy hello *WindowsImageBackup* directory in hello Recovery destination tooa non-critical volume of hello server.</span></span> <span data-ttu-id="2f296-138">通常，hello Windows 作業系統磁碟區是 hello 重要磁碟區。</span><span class="sxs-lookup"><span data-stu-id="2f296-138">Usually, hello Windows OS volume is hello critical volume.</span></span>

10. <span data-ttu-id="2f296-139">Hello 復原成功之後，請遵循 hello 區段中的 hello 步驟[套用還原系統狀態檔案 toohello Windows Server](backup-azure-restore-system-state.md#apply-restored-system-state-files-to-the-windows-server)，toocomplete hello 系統狀態復原程序。</span><span class="sxs-lookup"><span data-stu-id="2f296-139">Once hello recovery is successful, follow hello steps in hello section, [Apply restored System State files toohello Windows Server](backup-azure-restore-system-state.md#apply-restored-system-state-files-to-the-windows-server), toocomplete hello System State recovery process.</span></span>

## <a name="recover-system-state-files-tooan-alternate-server"></a><span data-ttu-id="2f296-140">復原系統狀態檔案 tooan 替代伺服器</span><span class="sxs-lookup"><span data-stu-id="2f296-140">Recover System State files tooan alternate server</span></span>

<span data-ttu-id="2f296-141">如果您的 Windows 伺服器已損毀或無法存取，而且您想 toorestore 它 tooa 穩定的狀態復原 hello Windows 伺服器系統狀態，您可以從另一部伺服器還原 hello 損毀的伺服器的系統狀態。</span><span class="sxs-lookup"><span data-stu-id="2f296-141">If your Windows Server is corrupted or inaccessible, and you want toorestore it tooa stable state by recovering hello Windows Server System State, you can restore hello corrupted server's System State from another server.</span></span> <span data-ttu-id="2f296-142">使用下列步驟 toohello 還原系統狀態不同的伺服器上的 hello。</span><span class="sxs-lookup"><span data-stu-id="2f296-142">Use hello following steps toohello restore System State on a separate server.</span></span>  

<span data-ttu-id="2f296-143">包含下列步驟中所使用的 hello 術語：</span><span class="sxs-lookup"><span data-stu-id="2f296-143">hello terminology used in these steps includes:</span></span>

- <span data-ttu-id="2f296-144">*來源機器*– 拍攝 hello 從哪個 hello 備份的原始電腦，這是目前無法使用。</span><span class="sxs-lookup"><span data-stu-id="2f296-144">*Source machine* – hello original machine from which hello backup was taken and which is currently unavailable.</span></span>
- <span data-ttu-id="2f296-145">*目標電腦*– hello 機器 toowhich hello 資料要復原的目的地。</span><span class="sxs-lookup"><span data-stu-id="2f296-145">*Target machine* – hello machine toowhich hello data is being recovered.</span></span>
- <span data-ttu-id="2f296-146">*範例保存庫*– hello 復原服務保存庫 toowhich hello*來源機器*和*目標機器*註冊。</span><span class="sxs-lookup"><span data-stu-id="2f296-146">*Sample vault* – hello Recovery Services vault toowhich hello *Source machine* and *Target machine* are registered.</span></span> <br/>

> [!NOTE]
> <span data-ttu-id="2f296-147">從一部電腦的備份無法還原的 tooa 執行舊版的 hello 作業系統的電腦。</span><span class="sxs-lookup"><span data-stu-id="2f296-147">Backups taken from one machine cannot be restored tooa machine running an earlier version of hello operating system.</span></span> <span data-ttu-id="2f296-148">比方說，Windows Server 2016 機器不能從備份還原 tooWindows Server 2012 R2。</span><span class="sxs-lookup"><span data-stu-id="2f296-148">For example, backups taken from a Windows Server 2016 machine can't be restored tooWindows Server 2012 R2.</span></span> <span data-ttu-id="2f296-149">然而，反向 hello 有可能。</span><span class="sxs-lookup"><span data-stu-id="2f296-149">However, hello inverse is possible.</span></span> <span data-ttu-id="2f296-150">您可以使用從 Windows Server 2012 R2 toorestore Windows Server 2016 的備份。</span><span class="sxs-lookup"><span data-stu-id="2f296-150">You can use backups from Windows Server 2012 R2 toorestore Windows Server 2016.</span></span>
>

1. <span data-ttu-id="2f296-151">開啟 hello **Microsoft Azure 備份**嵌入式管理單元在 hello*目標機器*。</span><span class="sxs-lookup"><span data-stu-id="2f296-151">Open hello **Microsoft Azure Backup** snap-in on hello *Target machine*.</span></span>
2. <span data-ttu-id="2f296-152">請確定該 hello*目標機器*和 hello*來源機器*是相同的復原服務保存庫註冊的 toohello。</span><span class="sxs-lookup"><span data-stu-id="2f296-152">Ensure that hello *Target machine* and hello *Source machine* are registered toohello same Recovery Services vault.</span></span>
3. <span data-ttu-id="2f296-153">按一下**復原資料**tooinitiate hello 工作流程。</span><span class="sxs-lookup"><span data-stu-id="2f296-153">Click **Recover Data** tooinitiate hello workflow.</span></span>

    ![復原資料](./media/backup-azure-restore-windows-server-classic/recover.png)

4. <span data-ttu-id="2f296-155">選取 [其他伺服器] </span><span class="sxs-lookup"><span data-stu-id="2f296-155">Select **Another server**</span></span>

    ![其他伺服器](./media/backup-azure-restore-system-state/anotherserver.png)

5. <span data-ttu-id="2f296-157">提供對應 toohello hello 保存庫認證檔案*範例保存庫*。</span><span class="sxs-lookup"><span data-stu-id="2f296-157">Provide hello vault credential file that corresponds toohello *Sample vault*.</span></span> <span data-ttu-id="2f296-158">如果 hello 保存庫認證檔案無效 （或已過期），下載新的保存庫認證檔案從 hello*範例保存庫*hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="2f296-158">If hello vault credential file is invalid (or expired), download a new vault credential file from hello *Sample vault* in hello Azure portal.</span></span> <span data-ttu-id="2f296-159">一旦提供 hello 保存庫認證檔案，則會出現 hello 與 hello 保存庫認證檔案相關聯的復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="2f296-159">Once hello vault credential file is provided, hello Recovery Services vault associated with hello vault credential file appears.</span></span>

6. <span data-ttu-id="2f296-160">在 hello 選取備份伺服器 窗格中，選取 hello*來源機器*從 hello 顯示的電腦清單。</span><span class="sxs-lookup"><span data-stu-id="2f296-160">On hello Select Backup Server pane, select hello *Source machine* from hello list of displayed machines.</span></span>

    ![電腦清單](./media/backup-azure-restore-windows-server-classic/machinelist.png)

7. <span data-ttu-id="2f296-162">在 hello 選取復原模式 窗格中，選擇 **系統狀態**按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="2f296-162">On hello Select Recovery Mode pane, choose **System State** and click **Next**.</span></span> 

    ![搜尋](./media/backup-azure-restore-system-state/recover-type-selection.png)

8. <span data-ttu-id="2f296-164">在 hello hello 行事曆上**選取磁碟區和日期**窗格中，選取復原點。</span><span class="sxs-lookup"><span data-stu-id="2f296-164">On hello Calendar in hello **Select Volume and Date** pane, select a recovery point.</span></span> <span data-ttu-id="2f296-165">您可以從任何時間的復原點還原。</span><span class="sxs-lookup"><span data-stu-id="2f296-165">You can restore from any recovery point in time.</span></span> <span data-ttu-id="2f296-166">日期**粗體**表示 hello 至少一個復原點的可用性。</span><span class="sxs-lookup"><span data-stu-id="2f296-166">Dates in **bold** indicate hello availability of at least one recovery point.</span></span> <span data-ttu-id="2f296-167">一旦您選取日期，如果有多個復原點可用，請選擇 hello 特定的復原點從 hello**時間**下拉式功能表。</span><span class="sxs-lookup"><span data-stu-id="2f296-167">Once  you select a date, if multiple recovery points are available, choose hello specific recovery point from hello **Time** drop-down menu.</span></span> 

    ![搜尋項目](./media/backup-azure-restore-system-state/select-date.png)

9. <span data-ttu-id="2f296-169">一旦您已選擇 hello 復原點 toorestore，按一下 **下一步**。</span><span class="sxs-lookup"><span data-stu-id="2f296-169">Once you have chosen hello recovery point toorestore, click **Next**.</span></span>

10. <span data-ttu-id="2f296-170">在 hello**選取系統狀態復原模式** 窗格中，指定您想執行系統狀態檔案的復原，toobe hello 目的地，然後按一下 **下一步**。</span><span class="sxs-lookup"><span data-stu-id="2f296-170">On hello **Select System State Recovery Mode** pane, specify hello destination where you want System State files toobe recovered, then click **Next**.</span></span>

    ![加密](./media/backup-azure-restore-system-state/recover-as-files.png)

    <span data-ttu-id="2f296-172">hello 選項，**建立複本，以擁有兩個版本**，而不是建立 hello 副本 hello 整個系統的狀態保存現有系統狀態檔案封存中建立個別的檔案複製。</span><span class="sxs-lookup"><span data-stu-id="2f296-172">hello option, **Create copies so that you have both versions**, creates copies of individual files in an existing System State file archive instead of creating hello copy of hello entire System State archive.</span></span>

11. <span data-ttu-id="2f296-173">確認 hello 詳細資料的復原在 hello 確認窗格中，然後按一下 **復原**。</span><span class="sxs-lookup"><span data-stu-id="2f296-173">Verify hello details of recovery on hello Confirmation pane, and click **Recover**.</span></span> 

    ![按一下 hello 復原按鈕 tooconfirm hello 復原程序](./media/backup-azure-restore-system-state/confirm-recovery.png)

12. <span data-ttu-id="2f296-175">複製 hello *WindowsImageBackup*目錄 tooa 非重要磁碟區的 hello 伺服器 (例如 d:\)。</span><span class="sxs-lookup"><span data-stu-id="2f296-175">Copy hello *WindowsImageBackup* directory tooa non-critical volume of hello server (for example D:\).</span></span> <span data-ttu-id="2f296-176">通常 hello Windows 作業系統磁碟區是 hello 重要磁碟區。</span><span class="sxs-lookup"><span data-stu-id="2f296-176">Usually hello Windows OS volume is hello critical volume.</span></span>

13. <span data-ttu-id="2f296-177">toocomplete hello 復原程序，使用 hello 下列區段太[適用於 Windows Server 上的 hello 還原系統狀態檔案](backup-azure-restore-system-state.md#apply-restored-system-state-on-a-windows-server)。</span><span class="sxs-lookup"><span data-stu-id="2f296-177">toocomplete hello recovery process, use hello following section too[apply hello restored System State files on a Windows Server](backup-azure-restore-system-state.md#apply-restored-system-state-on-a-windows-server).</span></span>




## <a name="apply-restored-system-state-on-a-windows-server"></a><span data-ttu-id="2f296-178">將還原的系統狀態套用到 Windows Server 上</span><span class="sxs-lookup"><span data-stu-id="2f296-178">Apply restored System State on a Windows Server</span></span>

<span data-ttu-id="2f296-179">一旦您已經復原系統狀態，以使用 Azure 復原服務代理程式的檔案，使用 hello Windows Server Backup 公用程式 tooapply hello 復原系統狀態 tooWindows 伺服器。</span><span class="sxs-lookup"><span data-stu-id="2f296-179">Once you have recovered System State as files using Azure Recovery Services Agent, use hello Windows Server Backup utility tooapply hello recovered System State tooWindows Server.</span></span> <span data-ttu-id="2f296-180">hello Windows Server Backup 公用程式已有 hello 伺服器上。</span><span class="sxs-lookup"><span data-stu-id="2f296-180">hello Windows Server Backup utility is already available on hello server.</span></span> <span data-ttu-id="2f296-181">hello 下列步驟說明如何 tooapply hello 復原系統狀態。</span><span class="sxs-lookup"><span data-stu-id="2f296-181">hello following steps explain how tooapply hello recovered System State.</span></span>

1. <span data-ttu-id="2f296-182">使用 hello 下列命令 tooreboot 伺服器*目錄服務修復模式*。</span><span class="sxs-lookup"><span data-stu-id="2f296-182">Use hello following commands tooreboot your server in *Directory Services Repair Mode*.</span></span> <span data-ttu-id="2f296-183">在提高權限的命令提示字元上：</span><span class="sxs-lookup"><span data-stu-id="2f296-183">In an elevated command prompt:</span></span>

    ```
    PS C:\> Bcdedit /set safeboot dsrepair
    PS C:\> Shutdown /r /t 0
    ```

2. <span data-ttu-id="2f296-184">Hello 重新開機後，開啟 hello Windows Server Backup 嵌入式管理單元。</span><span class="sxs-lookup"><span data-stu-id="2f296-184">After hello reboot, open hello Windows Server Backup snap-in.</span></span> <span data-ttu-id="2f296-185">如果您不知道 hello 嵌入式管理單元安裝所在，搜尋 hello 電腦或伺服器**Windows Server Backup**。</span><span class="sxs-lookup"><span data-stu-id="2f296-185">If you don't know where hello snap-in was installed, search hello computer or server for **Windows Server Backup**.</span></span>

    <span data-ttu-id="2f296-186">hello 桌面應用程式會出現在 hello 搜尋結果。</span><span class="sxs-lookup"><span data-stu-id="2f296-186">hello desktop app appears in hello search results.</span></span>

3. <span data-ttu-id="2f296-187">在 [hello] 嵌入式管理單元，選取**本機備份**。</span><span class="sxs-lookup"><span data-stu-id="2f296-187">In hello snap-in, select **Local Backup**.</span></span>

    ![從該處選取 本機備份 toorestore](./media/backup-azure-restore-system-state/win-server-backup-local-backup.png)

4. <span data-ttu-id="2f296-189">Hello 本機備份在主控台上，在 hello**動作 窗格**，按一下 **復原**tooopen hello 復原精靈。</span><span class="sxs-lookup"><span data-stu-id="2f296-189">On hello Local Backup console, in hello **Actions Pane**, click **Recover** tooopen hello Recovery Wizard.</span></span>

5. <span data-ttu-id="2f296-190">選取 hello 選項**儲存在另一個位置的備份**，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="2f296-190">Select hello option, **A backup stored in another location**, and click **Next**.</span></span>

   ![選擇 toorecover tooa 不同的伺服器](./media/backup-azure-restore-system-state/backup-stored-in-diff-location.png)

6. <span data-ttu-id="2f296-192">指定 hello 位置類型，請選取**遠端共用資料夾**如果您的系統狀態備份復原的 tooanother 伺服器。</span><span class="sxs-lookup"><span data-stu-id="2f296-192">When specifying hello location type, select **Remote shared folder** if your System State backup was recovered tooanother server.</span></span> <span data-ttu-id="2f296-193">如果您在本機復原系統狀態，則請選取 [本機磁碟機]。</span><span class="sxs-lookup"><span data-stu-id="2f296-193">If your System State was recovered locally, then select **Local drives**.</span></span> 

    ![選取是否從本機伺服器或另一個 toorecovery](./media/backup-azure-restore-system-state/ss-recovery-remote-shared-folder.png)

7. <span data-ttu-id="2f296-195">輸入 hello 路徑 toohello *WindowsImageBackup*目錄，或選擇包含使用 「 Azure 復原 hello 系統狀態檔案復原過程復原此目錄 (例如，D:\WindowsImageBackup) hello 本機磁碟機服務代理程式和按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="2f296-195">Enter hello path toohello *WindowsImageBackup* directory, or choose hello local drive containing this directory (for example, D:\WindowsImageBackup), recovered as part of hello System State files recovery using Azure Recovery Services Agent and click **Next**.</span></span>

    ![路徑 toohello 共用的檔案](./media/backup-azure-restore-system-state/ss-recovery-remote-folder.png)

8. <span data-ttu-id="2f296-197">選取 hello 系統狀態版本，您想 toorestore，然後按一下 **下一步**。</span><span class="sxs-lookup"><span data-stu-id="2f296-197">Select hello System State version that you want toorestore, and click **Next**.</span></span>

9. <span data-ttu-id="2f296-198">在 hello 選取復原類型 窗格中，選取 **系統狀態**按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="2f296-198">In hello Select Recovery Type pane, select **System State** and click **Next**.</span></span>

10. <span data-ttu-id="2f296-199">Hello 的 hello 系統狀態復原的位置，請選取**原始位置**，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="2f296-199">For hello location of hello System State Recovery, select **Original Location**, and click **Next**.</span></span>

11. <span data-ttu-id="2f296-200">檢閱 hello 確認詳細資料，請檢查 hello 重新開機設定，然後按一下**復原**tooapplly hello 還原系統狀態檔案。</span><span class="sxs-lookup"><span data-stu-id="2f296-200">Review hello confirmation details, verify hello reboot settings, and click **Recover** tooapplly hello restored System State files.</span></span>

    ![啟動 hello 還原系統狀態檔案](./media/backup-azure-restore-system-state/launch-ss-recovery.png)

## <a name="special-considerations-for-system-state-recovery-on-active-directory-server"></a><span data-ttu-id="2f296-202">在 Active Directory 伺服器上復原系統狀態的特殊考量</span><span class="sxs-lookup"><span data-stu-id="2f296-202">Special considerations for System State recovery on Active Directory server</span></span>

<span data-ttu-id="2f296-203">系統狀態備份中包含了 Active Directory 資料。</span><span class="sxs-lookup"><span data-stu-id="2f296-203">System State backup includes Active Directory data.</span></span> <span data-ttu-id="2f296-204">使用下列步驟 toorestore Active Directory 網域服務 (AD DS) 從目前的狀態 tooa 先前狀態的 hello。</span><span class="sxs-lookup"><span data-stu-id="2f296-204">Use hello following steps toorestore Active Directory Domain Service (AD DS) from its current state tooa previous state.</span></span>

1. <span data-ttu-id="2f296-205">重新啟動 hello 網域控制站在目錄服務還原模式 (DSRM)。</span><span class="sxs-lookup"><span data-stu-id="2f296-205">Restart hello domain controller in Directory Services Restore Mode (DSRM).</span></span>
2. <span data-ttu-id="2f296-206">請依照下列步驟 hello[這裡](https://technet.microsoft.com/en-us/library/cc794755(v=ws.10).aspx)toouse Windows Server Backup cmdlet toorecover AD DS。</span><span class="sxs-lookup"><span data-stu-id="2f296-206">Follow hello steps [here](https://technet.microsoft.com/en-us/library/cc794755(v=ws.10).aspx) toouse Windows Server Backup cmdlets toorecover AD DS.</span></span>


## <a name="troubleshoot-failed-system-state-restore"></a><span data-ttu-id="2f296-207">針對失敗的系統狀態還原進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="2f296-207">Troubleshoot failed System State restore</span></span>

<span data-ttu-id="2f296-208">Hello 套用系統狀態的上一個程序未成功完成時，如果使用 Windows Server hello Windows 修復環境 (Win RE) toorecover。</span><span class="sxs-lookup"><span data-stu-id="2f296-208">If hello previous process of applying System State does not complete successfully, use hello Windows Recovery Environment (Win RE) toorecover your Windows Server.</span></span> <span data-ttu-id="2f296-209">hello 下列步驟說明如何使用 Win RE toorecover。</span><span class="sxs-lookup"><span data-stu-id="2f296-209">hello following steps explain how toorecover using Win RE.</span></span> <span data-ttu-id="2f296-210">請在 Windows Server 不會於系統狀態還原後正常開機時，才使用此選項。</span><span class="sxs-lookup"><span data-stu-id="2f296-210">Use This option only if Windows Server does not boot normally after a System State restore.</span></span> <span data-ttu-id="2f296-211">hello 程序之後清除非系統資料，請留意。</span><span class="sxs-lookup"><span data-stu-id="2f296-211">hello following process erases non-system data, use caution.</span></span> 

1. <span data-ttu-id="2f296-212">您的 Windows 伺服器開機進入 Windows 修復環境 (Win RE) hello。</span><span class="sxs-lookup"><span data-stu-id="2f296-212">Boot your Windows Server into hello Windows Recovery Environment (Win RE).</span></span>

2. <span data-ttu-id="2f296-213">選取從 hello 三個可用選項的疑難排解。</span><span class="sxs-lookup"><span data-stu-id="2f296-213">Select Troubleshoot from hello three available options.</span></span>

    ![開啟功能表](./media/backup-azure-restore-system-state/winre-1.png)

3. <span data-ttu-id="2f296-215">從 hello**進階選項**畫面上，選取**命令提示字元**提供 hello 伺服器系統管理員使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="2f296-215">From hello **Advanced Options** screen, select **Command Prompt** and provide hello server administrator username and password.</span></span>

   ![開啟功能表](./media/backup-azure-restore-system-state/winre-2.png)

4. <span data-ttu-id="2f296-217">提供 hello 伺服器系統管理員使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="2f296-217">Provide hello server administrator username and password.</span></span>

    ![開啟功能表](./media/backup-azure-restore-system-state/winre-3.png)

5. <span data-ttu-id="2f296-219">當您以系統管理員模式開啟 hello 命令提示字元時，執行下列命令 tooget hello 系統狀態備份版本。</span><span class="sxs-lookup"><span data-stu-id="2f296-219">When you open hello command prompt in administrator mode, run following command tooget hello System State backup versions.</span></span>

    ```
    Wbadmin get versions -backuptarget:<Volume where WindowsImageBackup folder is copied>:
    ```
    ![取得系統狀態備份版本](./media/backup-azure-restore-system-state/winre-4.png)

6. <span data-ttu-id="2f296-221">執行下列命令 tooget hello hello 備份中可用的所有磁碟區。</span><span class="sxs-lookup"><span data-stu-id="2f296-221">Run hello following command tooget all volumes available in hello backup.</span></span>

    ```
    Wbadmin get items -version:<copy version from above step> -backuptarget:<Backup volume>
    ```

    ![取得系統狀態備份版本](./media/backup-azure-restore-system-state/winre-5.png)

7. <span data-ttu-id="2f296-223">hello 下列命令會復原所有磁碟區屬於 hello 系統狀態備份。</span><span class="sxs-lookup"><span data-stu-id="2f296-223">hello following command recovers all volumes that are part of hello System State Backup.</span></span> <span data-ttu-id="2f296-224">請注意此步驟中復原只 hello 重要磁碟區屬於 hello 系統狀態。</span><span class="sxs-lookup"><span data-stu-id="2f296-224">Note that this step recovers only hello critical volumes that are part of hello System State.</span></span> <span data-ttu-id="2f296-225">非系統資料全都會遭到清除。</span><span class="sxs-lookup"><span data-stu-id="2f296-225">All non-System data is erased.</span></span>

    ```
    Wbadmin start recovery -items:C: -itemtype:Volume -version:<Backupversion> -backuptarget:<backup target volume>
    ```
     ![取得系統狀態備份版本](./media/backup-azure-restore-system-state/winre-6.png)



## <a name="next-steps"></a><span data-ttu-id="2f296-227">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2f296-227">Next steps</span></span>
* <span data-ttu-id="2f296-228">現在您已復原檔案和資料夾，接下來您可以 [管理您的備份](backup-azure-manage-windows-server.md)。</span><span class="sxs-lookup"><span data-stu-id="2f296-228">Now that you've recovered your files and folders, you can [manage your backups](backup-azure-manage-windows-server.md).</span></span>
