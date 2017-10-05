---
title: "Azure 備份：將系統狀態還原到 Windows Server | Microsoft Docs"
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
ms.openlocfilehash: 320c85f8045d9b72cf7f430d2e2736ba8e5ec269
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="restore-system-state-to-windows-server"></a><span data-ttu-id="bb311-103">將系統狀態還原到 Windows Server</span><span class="sxs-lookup"><span data-stu-id="bb311-103">Restore System State to Windows Server</span></span>

<span data-ttu-id="bb311-104">本文說明如何從 Azure 復原服務保存庫來還原 Windows Server 系統狀態備份。</span><span class="sxs-lookup"><span data-stu-id="bb311-104">This article explains how to restore Windows Server System State backups from an Azure Recovery Services vault.</span></span> <span data-ttu-id="bb311-105">若要還原系統狀態，您必須有系統狀態備份 (使用[備份系統狀態](backup-azure-system-state.md#back-up-windows-server-system-state-preview)中的指示所建立)，並確定您已安裝[最新版的 Microsoft Azure 復原服務 (MARS) 代理程式](http://aka.ms/azurebackup_agent)。</span><span class="sxs-lookup"><span data-stu-id="bb311-105">To restore System State, you must have a System State backup (created using the instructions in [Back up System State](backup-azure-system-state.md#back-up-windows-server-system-state-preview)), and make sure you have installed the [latest version of the Microsoft Azure Recovery Services (MARS) agent](http://aka.ms/azurebackup_agent).</span></span> <span data-ttu-id="bb311-106">從 Azure 復原服務保存庫來復原 Windows Server 系統狀態資料的程序需要兩個步驟：</span><span class="sxs-lookup"><span data-stu-id="bb311-106">Recovering Windows Server System State data from an Azure Recovery Services vault is a two-step process:</span></span>

1. <span data-ttu-id="bb311-107">從 Azure 備份來還原檔案形式的系統狀態。</span><span class="sxs-lookup"><span data-stu-id="bb311-107">Restore System State as files from Azure Backup.</span></span> <span data-ttu-id="bb311-108">在從 Azure 備份來還原檔案形式的系統狀態時，您可以：</span><span class="sxs-lookup"><span data-stu-id="bb311-108">When restoring System State as files from Azure Backup, you can either:</span></span>
  * <span data-ttu-id="bb311-109">將系統狀態還原到進行備份時所在的相同伺服器，或</span><span class="sxs-lookup"><span data-stu-id="bb311-109">Restore System State to the same server where the backups were taken, or</span></span>
  * <span data-ttu-id="bb311-110">將系統狀態檔案還原到替代伺服器。</span><span class="sxs-lookup"><span data-stu-id="bb311-110">Restore System State file to an alternate server.</span></span>

2. <span data-ttu-id="bb311-111">將還原的系統狀態檔案套用到 Windows Server。</span><span class="sxs-lookup"><span data-stu-id="bb311-111">Apply the restored System State files to a Windows Server.</span></span>


## <a name="recover-system-state-files-to-the-same-server"></a><span data-ttu-id="bb311-112">將系統狀態檔案復原到相同伺服器</span><span class="sxs-lookup"><span data-stu-id="bb311-112">Recover System State files to the same server</span></span>
<span data-ttu-id="bb311-113">下列步驟說明如何將 Windows Server 組態復原到先前的狀態。</span><span class="sxs-lookup"><span data-stu-id="bb311-113">The following steps explain how to roll back your Windows Server configuration to a previous state.</span></span> <span data-ttu-id="bb311-114">將伺服器組態復原到已知的穩定狀態是非常有價值的作業。</span><span class="sxs-lookup"><span data-stu-id="bb311-114">Rolling your server configuration back to a known, stable state, can be extremely valuable.</span></span> <span data-ttu-id="bb311-115">下列步驟會從復原服務保存庫還原伺服器的系統狀態。</span><span class="sxs-lookup"><span data-stu-id="bb311-115">The following steps restore the server's System State from a Recovery Services vault.</span></span> 

1. <span data-ttu-id="bb311-116">開啟 **Microsoft Azure 備份**嵌入式管理單元。</span><span class="sxs-lookup"><span data-stu-id="bb311-116">Open the **Microsoft Azure Backup** snap-in.</span></span> <span data-ttu-id="bb311-117">如果您不知道快照安裝的位置，請在電腦或伺服器上搜尋 **Microsoft Azure 備份**。</span><span class="sxs-lookup"><span data-stu-id="bb311-117">If you don't know where the snap-in was installed, search the computer or server for **Microsoft Azure Backup**.</span></span>

    <span data-ttu-id="bb311-118">傳統型應用程式應該會出現在搜尋結果中。</span><span class="sxs-lookup"><span data-stu-id="bb311-118">The desktop app should appear in the search results.</span></span>

2. <span data-ttu-id="bb311-119">按一下 [復原資料] 以啟動精靈。</span><span class="sxs-lookup"><span data-stu-id="bb311-119">Click **Recover Data** to start the wizard.</span></span>

    ![復原資料](./media/backup-azure-restore-windows-server/recover.png)

3. <span data-ttu-id="bb311-121">在 [開始使用] 窗格中，若要將資料還原至同一台伺服器或電腦，請選取 [這台伺服器 (`<server name>`)] 並按一下 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="bb311-121">On the **Getting Started** pane, to restore the data to the same server or computer, select **This server (`<server name>`)** and click **Next**.</span></span>

    ![選擇 [這台伺服器] 選項以將資料還原到同一台電腦](./media/backup-azure-restore-system-state/samemachine.png)

4. <span data-ttu-id="bb311-123">在 [選取復原模式] 窗格上，選擇 [系統狀態]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="bb311-123">On the **Select Recovery Mode** pane, choose **System State** and then click **Next**.</span></span>

    ![瀏覽檔案](./media/backup-azure-restore-system-state/recover-type-selection.png)

5. <span data-ttu-id="bb311-125">在 [選取磁碟區和日期] 窗格的行事曆上，選取復原點。</span><span class="sxs-lookup"><span data-stu-id="bb311-125">On the calendar in **Select Volume and Date** pane, select a recovery point.</span></span> 

    <span data-ttu-id="bb311-126">您可以從任何時間的復原點還原。</span><span class="sxs-lookup"><span data-stu-id="bb311-126">You can restore from any recovery point in time.</span></span> <span data-ttu-id="bb311-127">**粗體**的日期表示至少有一個復原點可用。</span><span class="sxs-lookup"><span data-stu-id="bb311-127">Dates in **bold** indicate the availability of at least one recovery point.</span></span> <span data-ttu-id="bb311-128">一旦您選取一個日期，如果有多個復原點可用，您可以從 [時間] 下拉式功能表選擇特定的復原點。</span><span class="sxs-lookup"><span data-stu-id="bb311-128">Once you select a date, if multiple recovery points are available, choose the specific recovery point from the **Time** drop-down menu.</span></span>

    ![磁碟區和日期](./media/backup-azure-restore-system-state/select-date.png)

6. <span data-ttu-id="bb311-130">選擇要還原的復原點之後，請按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="bb311-130">Once you have chosen the recovery point to restore, click **Next**.</span></span>

    <span data-ttu-id="bb311-131">Azure 備份會掛接本機復原點，並且使用它做為復原磁碟區。</span><span class="sxs-lookup"><span data-stu-id="bb311-131">Azure Backup mounts the local recovery point, and uses it as a recovery volume.</span></span>

7. <span data-ttu-id="bb311-132">在下一個窗格中，指定所復原之系統狀態檔案的目的地，然後按一下 [瀏覽] 以開啟 Windows 檔案總管，並找到您要的檔案和資料夾。</span><span class="sxs-lookup"><span data-stu-id="bb311-132">On the next pane, specify the destination for the recovered System State files and click **Browse** to open Windows Explorer and find the files and folders you want.</span></span> <span data-ttu-id="bb311-133">[建立複本，以擁有兩個版本] 選項會在現有系統狀態檔案封存中建立個別檔案的複本，而不是建立整個系統狀態封存的複本。</span><span class="sxs-lookup"><span data-stu-id="bb311-133">The option, **Create copies so that you have both versions**, creates copies of individual files in an existing System State file archive instead of creating the copy of the entire System State archive.</span></span>

    ![修復選項](./media/backup-azure-restore-system-state/recover-as-files.png)

8. <span data-ttu-id="bb311-135">確認 [確認] 窗格上的復原詳細資料，然後按一下 [復原]。</span><span class="sxs-lookup"><span data-stu-id="bb311-135">Verify the details of recovery on the **Confirmation** pane and click **Recover**.</span></span>

   ![按一下 [復原] 以認可復原動作](./media/backup-azure-restore-system-state/confirm-recovery.png)

9. <span data-ttu-id="bb311-137">將復原目的地中的 WindowsImageBackup 目錄複製到伺服器的非重要磁碟區。</span><span class="sxs-lookup"><span data-stu-id="bb311-137">Copy the *WindowsImageBackup* directory in the Recovery destination to a non-critical volume of the server.</span></span> <span data-ttu-id="bb311-138">Windows 作業系統磁碟區通常是重要磁碟區。</span><span class="sxs-lookup"><span data-stu-id="bb311-138">Usually, the Windows OS volume is the critical volume.</span></span>

10. <span data-ttu-id="bb311-139">復原成功之後，請遵循[將還原的系統狀態檔案套用到 Windows Server](backup-azure-restore-system-state.md#apply-restored-system-state-files-to-the-windows-server) 一節中的步驟，以完成系統狀態復原程序。</span><span class="sxs-lookup"><span data-stu-id="bb311-139">Once the recovery is successful, follow the steps in the section, [Apply restored System State files to the Windows Server](backup-azure-restore-system-state.md#apply-restored-system-state-files-to-the-windows-server), to complete the System State recovery process.</span></span>

## <a name="recover-system-state-files-to-an-alternate-server"></a><span data-ttu-id="bb311-140">將系統狀態檔案復原到替代伺服器</span><span class="sxs-lookup"><span data-stu-id="bb311-140">Recover System State files to an alternate server</span></span>

<span data-ttu-id="bb311-141">如果您的 Windows Server 已損毀或無法存取，而且您想要藉由復原 Windows Server 系統狀態將它還原到穩定狀態，您可以從其他伺服器還原已損毀之伺服器的系統狀態。</span><span class="sxs-lookup"><span data-stu-id="bb311-141">If your Windows Server is corrupted or inaccessible, and you want to restore it to a stable state by recovering the Windows Server System State, you can restore the corrupted server's System State from another server.</span></span> <span data-ttu-id="bb311-142">請使用下列步驟在不同的伺服器上還原系統狀態。</span><span class="sxs-lookup"><span data-stu-id="bb311-142">Use the following steps to the restore System State on a separate server.</span></span>  

<span data-ttu-id="bb311-143">這些步驟中所使用的術語包含：</span><span class="sxs-lookup"><span data-stu-id="bb311-143">The terminology used in these steps includes:</span></span>

- <span data-ttu-id="bb311-144"> – 用來進行備份且目前無法使用的的原始電腦。</span><span class="sxs-lookup"><span data-stu-id="bb311-144">*Source machine* – The original machine from which the backup was taken and which is currently unavailable.</span></span>
- <span data-ttu-id="bb311-145"> – 復原資料時的目標電腦。</span><span class="sxs-lookup"><span data-stu-id="bb311-145">*Target machine* – The machine to which the data is being recovered.</span></span>
- <span data-ttu-id="bb311-146">「範例保存庫」–「來源電腦」和「目標電腦」註冊的復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="bb311-146">*Sample vault* – The Recovery Services vault to which the *Source machine* and *Target machine* are registered.</span></span> <br/>

> [!NOTE]
> <span data-ttu-id="bb311-147">從某個電腦擷取的備份無法還原到執行舊版作業系統的電腦上。</span><span class="sxs-lookup"><span data-stu-id="bb311-147">Backups taken from one machine cannot be restored to a machine running an earlier version of the operating system.</span></span> <span data-ttu-id="bb311-148">例如，從 Windows Server 2016 電腦擷取的備份便無法還原到 Windows Server 2012 R2。</span><span class="sxs-lookup"><span data-stu-id="bb311-148">For example, backups taken from a Windows Server 2016 machine can't be restored to Windows Server 2012 R2.</span></span> <span data-ttu-id="bb311-149">不過，反過來則可行。</span><span class="sxs-lookup"><span data-stu-id="bb311-149">However, the inverse is possible.</span></span> <span data-ttu-id="bb311-150">您可以使用 Windows Server 2012 R2 的備份來還原 Windows Server 2016。</span><span class="sxs-lookup"><span data-stu-id="bb311-150">You can use backups from Windows Server 2012 R2 to restore Windows Server 2016.</span></span>
>

1. <span data-ttu-id="bb311-151">在「目標電腦」上開啟 [Microsoft Azure 備份] 嵌入式管理單元。</span><span class="sxs-lookup"><span data-stu-id="bb311-151">Open the **Microsoft Azure Backup** snap-in on the *Target machine*.</span></span>
2. <span data-ttu-id="bb311-152">確定「目標電腦」和「來源電腦」均已註冊到相同的復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="bb311-152">Ensure that the *Target machine* and the *Source machine* are registered to the same Recovery Services vault.</span></span>
3. <span data-ttu-id="bb311-153">按一下 [復原資料]  初始化工作流程。</span><span class="sxs-lookup"><span data-stu-id="bb311-153">Click **Recover Data** to initiate the workflow.</span></span>

    ![復原資料](./media/backup-azure-restore-windows-server-classic/recover.png)

4. <span data-ttu-id="bb311-155">選取 [其他伺服器] </span><span class="sxs-lookup"><span data-stu-id="bb311-155">Select **Another server**</span></span>

    ![其他伺服器](./media/backup-azure-restore-system-state/anotherserver.png)

5. <span data-ttu-id="bb311-157">提供與「範例保存庫」 相對應的保存庫認證檔。</span><span class="sxs-lookup"><span data-stu-id="bb311-157">Provide the vault credential file that corresponds to the *Sample vault*.</span></span> <span data-ttu-id="bb311-158">如果保存庫認證檔無效 (或已過期)，請從 Azure 入口網站中的「範例保存庫」下載新的保存庫認證檔。</span><span class="sxs-lookup"><span data-stu-id="bb311-158">If the vault credential file is invalid (or expired), download a new vault credential file from the *Sample vault* in the Azure portal.</span></span> <span data-ttu-id="bb311-159">一旦提供保存庫認證檔，即會顯示與保存庫認證檔相關聯的復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="bb311-159">Once the vault credential file is provided, the Recovery Services vault associated with the vault credential file appears.</span></span>

6. <span data-ttu-id="bb311-160">在 [選取備份伺服器] 窗格上，從顯示的電腦清單選取 [來源電腦]。</span><span class="sxs-lookup"><span data-stu-id="bb311-160">On the Select Backup Server pane, select the *Source machine* from the list of displayed machines.</span></span>

    ![電腦清單](./media/backup-azure-restore-windows-server-classic/machinelist.png)

7. <span data-ttu-id="bb311-162">在 [選取復原模式] 窗格上，選擇 [系統狀態]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="bb311-162">On the Select Recovery Mode pane, choose **System State** and click **Next**.</span></span> 

    ![搜尋](./media/backup-azure-restore-system-state/recover-type-selection.png)

8. <span data-ttu-id="bb311-164">在 [選取磁碟區和日期] 窗格的行事曆上，選取復原點。</span><span class="sxs-lookup"><span data-stu-id="bb311-164">On the Calendar in the **Select Volume and Date** pane, select a recovery point.</span></span> <span data-ttu-id="bb311-165">您可以從任何時間的復原點還原。</span><span class="sxs-lookup"><span data-stu-id="bb311-165">You can restore from any recovery point in time.</span></span> <span data-ttu-id="bb311-166">**粗體**的日期表示至少有一個復原點可用。</span><span class="sxs-lookup"><span data-stu-id="bb311-166">Dates in **bold** indicate the availability of at least one recovery point.</span></span> <span data-ttu-id="bb311-167">一旦您選取一個日期，如果有多個復原點可用，您可以從 [時間] 下拉式功能表選擇特定的復原點。</span><span class="sxs-lookup"><span data-stu-id="bb311-167">Once  you select a date, if multiple recovery points are available, choose the specific recovery point from the **Time** drop-down menu.</span></span> 

    ![搜尋項目](./media/backup-azure-restore-system-state/select-date.png)

9. <span data-ttu-id="bb311-169">選擇要還原的復原點之後，請按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="bb311-169">Once you have chosen the recovery point to restore, click **Next**.</span></span>

10. <span data-ttu-id="bb311-170">在 [選取系統狀態復原模式] 窗格中，指定您想要作為系統狀態檔案復原位置的目的地，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="bb311-170">On the **Select System State Recovery Mode** pane, specify the destination where you want System State files to be recovered, then click **Next**.</span></span>

    ![加密](./media/backup-azure-restore-system-state/recover-as-files.png)

    <span data-ttu-id="bb311-172">[建立複本，以擁有兩個版本] 選項會在現有系統狀態檔案封存中建立個別檔案的複本，而不是建立整個系統狀態封存的複本。</span><span class="sxs-lookup"><span data-stu-id="bb311-172">The option, **Create copies so that you have both versions**, creates copies of individual files in an existing System State file archive instead of creating the copy of the entire System State archive.</span></span>

11. <span data-ttu-id="bb311-173">確認 [確認] 窗格上的復原詳細資料，然後按一下 [復原]。</span><span class="sxs-lookup"><span data-stu-id="bb311-173">Verify the details of recovery on the Confirmation pane, and click **Recover**.</span></span> 

    ![按一下 [復原] 按鈕以確認復原程序](./media/backup-azure-restore-system-state/confirm-recovery.png)

12. <span data-ttu-id="bb311-175">將 WindowsImageBackup 目錄複製到伺服器的非重要磁碟區 (例如 D:\)。</span><span class="sxs-lookup"><span data-stu-id="bb311-175">Copy the *WindowsImageBackup* directory to a non-critical volume of the server (for example D:\).</span></span> <span data-ttu-id="bb311-176">Windows 作業系統磁碟區通常是重要磁碟區。</span><span class="sxs-lookup"><span data-stu-id="bb311-176">Usually the Windows OS volume is the critical volume.</span></span>

13. <span data-ttu-id="bb311-177">若要完成復原程序，請使用下一節的步驟[將還原的系統狀態檔案套用到 Windows Server 上](backup-azure-restore-system-state.md#apply-restored-system-state-on-a-windows-server)。</span><span class="sxs-lookup"><span data-stu-id="bb311-177">To complete the recovery process, use the following section to [apply the restored System State files on a Windows Server](backup-azure-restore-system-state.md#apply-restored-system-state-on-a-windows-server).</span></span>




## <a name="apply-restored-system-state-on-a-windows-server"></a><span data-ttu-id="bb311-178">將還原的系統狀態套用到 Windows Server 上</span><span class="sxs-lookup"><span data-stu-id="bb311-178">Apply restored System State on a Windows Server</span></span>

<span data-ttu-id="bb311-179">在使用 Azure 復原服務代理程式復原了檔案形式的系統狀態後，請使用 Windows Server Backup 公用程式將復原的系統狀態套用到 Windows Server。</span><span class="sxs-lookup"><span data-stu-id="bb311-179">Once you have recovered System State as files using Azure Recovery Services Agent, use the Windows Server Backup utility to apply the recovered System State to Windows Server.</span></span> <span data-ttu-id="bb311-180">伺服器上已有 Windows Server Backup 公用程式可供使用。</span><span class="sxs-lookup"><span data-stu-id="bb311-180">The Windows Server Backup utility is already available on the server.</span></span> <span data-ttu-id="bb311-181">下列步驟說明如何套用復原的系統狀態。</span><span class="sxs-lookup"><span data-stu-id="bb311-181">The following steps explain how to apply the recovered System State.</span></span>

1. <span data-ttu-id="bb311-182">使用下列命令以「目錄服務修復模式」重新啟動您的伺服器。</span><span class="sxs-lookup"><span data-stu-id="bb311-182">Use the following commands to reboot your server in *Directory Services Repair Mode*.</span></span> <span data-ttu-id="bb311-183">在提高權限的命令提示字元上：</span><span class="sxs-lookup"><span data-stu-id="bb311-183">In an elevated command prompt:</span></span>

    ```
    PS C:\> Bcdedit /set safeboot dsrepair
    PS C:\> Shutdown /r /t 0
    ```

2. <span data-ttu-id="bb311-184">在重新啟動後，開啟 Windows Server Backup 嵌入式管理單元。</span><span class="sxs-lookup"><span data-stu-id="bb311-184">After the reboot, open the Windows Server Backup snap-in.</span></span> <span data-ttu-id="bb311-185">如果您不知道快照安裝的位置，請在電腦或伺服器上搜尋 **Windows Server Backup**。</span><span class="sxs-lookup"><span data-stu-id="bb311-185">If you don't know where the snap-in was installed, search the computer or server for **Windows Server Backup**.</span></span>

    <span data-ttu-id="bb311-186">傳統型應用程式就會出現在搜尋結果中。</span><span class="sxs-lookup"><span data-stu-id="bb311-186">The desktop app appears in the search results.</span></span>

3. <span data-ttu-id="bb311-187">在嵌入式管理單元中，選取 [本機備份]。</span><span class="sxs-lookup"><span data-stu-id="bb311-187">In the snap-in, select **Local Backup**.</span></span>

    ![選取要從中還原的本機備份](./media/backup-azure-restore-system-state/win-server-backup-local-backup.png)

4. <span data-ttu-id="bb311-189">在本機備份主控台的 [動作] 窗格中，按一下 [復原] 以開啟復原精靈。</span><span class="sxs-lookup"><span data-stu-id="bb311-189">On the Local Backup console, in the **Actions Pane**, click **Recover** to open the Recovery Wizard.</span></span>

5. <span data-ttu-id="bb311-190">選取 [儲存在其他位置的備份] 選項，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="bb311-190">Select the option, **A backup stored in another location**, and click **Next**.</span></span>

   ![選擇復原到不同伺服器](./media/backup-azure-restore-system-state/backup-stored-in-diff-location.png)

6. <span data-ttu-id="bb311-192">在指定位置類型時，如果您的系統狀態備份已復原到其他伺服器，請選取 [遠端共用資料夾]。</span><span class="sxs-lookup"><span data-stu-id="bb311-192">When specifying the location type, select **Remote shared folder** if your System State backup was recovered to another server.</span></span> <span data-ttu-id="bb311-193">如果您在本機復原系統狀態，則請選取 [本機磁碟機]。</span><span class="sxs-lookup"><span data-stu-id="bb311-193">If your System State was recovered locally, then select **Local drives**.</span></span> 

    ![選取要從本機伺服器還是其他伺服器來復原](./media/backup-azure-restore-system-state/ss-recovery-remote-shared-folder.png)

7. <span data-ttu-id="bb311-195">輸入 WindowsImageBackup 目錄的路徑，或選擇包含此目錄的本機磁碟機 (例如，D:\WindowsImageBackup) (使用 Azure 復原服務代理程式隨著系統狀態檔案的復原而復原)，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="bb311-195">Enter the path to the *WindowsImageBackup* directory, or choose the local drive containing this directory (for example, D:\WindowsImageBackup), recovered as part of the System State files recovery using Azure Recovery Services Agent and click **Next**.</span></span>

    ![共用檔案的路徑](./media/backup-azure-restore-system-state/ss-recovery-remote-folder.png)

8. <span data-ttu-id="bb311-197">選取您想要還原的系統狀態版本，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="bb311-197">Select the System State version that you want to restore, and click **Next**.</span></span>

9. <span data-ttu-id="bb311-198">在 [選取復原類型] 窗格中選取 [系統狀態]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="bb311-198">In the Select Recovery Type pane, select **System State** and click **Next**.</span></span>

10. <span data-ttu-id="bb311-199">在系統狀態復原的位置中，選取 [原始位置]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="bb311-199">For the location of the System State Recovery, select **Original Location**, and click **Next**.</span></span>

11. <span data-ttu-id="bb311-200">檢閱確認詳細資料，確認重新啟動設定，然後按一下 [復原] 以套用還原的系統狀態檔案。</span><span class="sxs-lookup"><span data-stu-id="bb311-200">Review the confirmation details, verify the reboot settings, and click **Recover** to applly the restored System State files.</span></span>

    ![啟動系統狀態檔案的還原](./media/backup-azure-restore-system-state/launch-ss-recovery.png)

## <a name="special-considerations-for-system-state-recovery-on-active-directory-server"></a><span data-ttu-id="bb311-202">在 Active Directory 伺服器上復原系統狀態的特殊考量</span><span class="sxs-lookup"><span data-stu-id="bb311-202">Special considerations for System State recovery on Active Directory server</span></span>

<span data-ttu-id="bb311-203">系統狀態備份中包含了 Active Directory 資料。</span><span class="sxs-lookup"><span data-stu-id="bb311-203">System State backup includes Active Directory data.</span></span> <span data-ttu-id="bb311-204">請使用下列步驟將 Active Directory Domain Services (AD DS) 從目前的狀態還原到先前的狀態。</span><span class="sxs-lookup"><span data-stu-id="bb311-204">Use the following steps to restore Active Directory Domain Service (AD DS) from its current state to a previous state.</span></span>

1. <span data-ttu-id="bb311-205">將網域控制站重新啟動為目錄服務還原模式 (DSRM)。</span><span class="sxs-lookup"><span data-stu-id="bb311-205">Restart the domain controller in Directory Services Restore Mode (DSRM).</span></span>
2. <span data-ttu-id="bb311-206">遵循[此處](https://technet.microsoft.com/en-us/library/cc794755(v=ws.10).aspx)的步驟，以使用 Windows Server Backup Cmdlet 來復原 AD DS。</span><span class="sxs-lookup"><span data-stu-id="bb311-206">Follow the steps [here](https://technet.microsoft.com/en-us/library/cc794755(v=ws.10).aspx) to use Windows Server Backup cmdlets to recover AD DS.</span></span>


## <a name="troubleshoot-failed-system-state-restore"></a><span data-ttu-id="bb311-207">針對失敗的系統狀態還原進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="bb311-207">Troubleshoot failed System State restore</span></span>

<span data-ttu-id="bb311-208">如果先前用來套用系統狀態的程序未順利完成，請使用 Windows 修復環境 (Win RE) 來復原您的 Windows Server。</span><span class="sxs-lookup"><span data-stu-id="bb311-208">If the previous process of applying System State does not complete successfully, use the Windows Recovery Environment (Win RE) to recover your Windows Server.</span></span> <span data-ttu-id="bb311-209">下列步驟說明如何使用 Win RE 來進行復原。</span><span class="sxs-lookup"><span data-stu-id="bb311-209">The following steps explain how to recover using Win RE.</span></span> <span data-ttu-id="bb311-210">請在 Windows Server 不會於系統狀態還原後正常開機時，才使用此選項。</span><span class="sxs-lookup"><span data-stu-id="bb311-210">Use This option only if Windows Server does not boot normally after a System State restore.</span></span> <span data-ttu-id="bb311-211">下列程序會清除非系統資料，請小心使用。</span><span class="sxs-lookup"><span data-stu-id="bb311-211">The following process erases non-system data, use caution.</span></span> 

1. <span data-ttu-id="bb311-212">將您的 Windows Server 開機到 Windows 修復環境 (Win RE)。</span><span class="sxs-lookup"><span data-stu-id="bb311-212">Boot your Windows Server into the Windows Recovery Environment (Win RE).</span></span>

2. <span data-ttu-id="bb311-213">在三個可用選項中選取 [疑難排解]。</span><span class="sxs-lookup"><span data-stu-id="bb311-213">Select Troubleshoot from the three available options.</span></span>

    ![開啟功能表](./media/backup-azure-restore-system-state/winre-1.png)

3. <span data-ttu-id="bb311-215">從 [進階選項] 畫面上選取 [命令提示字元]，然後提供伺服器系統管理員使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="bb311-215">From the **Advanced Options** screen, select **Command Prompt** and provide the server administrator username and password.</span></span>

   ![開啟功能表](./media/backup-azure-restore-system-state/winre-2.png)

4. <span data-ttu-id="bb311-217">提供伺服器系統管理員使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="bb311-217">Provide the server administrator username and password.</span></span>

    ![開啟功能表](./media/backup-azure-restore-system-state/winre-3.png)

5. <span data-ttu-id="bb311-219">當您以系統管理員模式開啟命令提示字元時，請執行下列命令來取得系統狀態備份版本。</span><span class="sxs-lookup"><span data-stu-id="bb311-219">When you open the command prompt in administrator mode, run following command to get the System State backup versions.</span></span>

    ```
    Wbadmin get versions -backuptarget:<Volume where WindowsImageBackup folder is copied>:
    ```
    ![取得系統狀態備份版本](./media/backup-azure-restore-system-state/winre-4.png)

6. <span data-ttu-id="bb311-221">執行下列命令以取得備份中可用的所有磁碟區。</span><span class="sxs-lookup"><span data-stu-id="bb311-221">Run the following command to get all volumes available in the backup.</span></span>

    ```
    Wbadmin get items -version:<copy version from above step> -backuptarget:<Backup volume>
    ```

    ![取得系統狀態備份版本](./media/backup-azure-restore-system-state/winre-5.png)

7. <span data-ttu-id="bb311-223">下列命令會復原所有屬於系統狀態備份的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="bb311-223">The following command recovers all volumes that are part of the System State Backup.</span></span> <span data-ttu-id="bb311-224">請注意，此步驟只會復原屬於系統狀態的重要磁碟區。</span><span class="sxs-lookup"><span data-stu-id="bb311-224">Note that this step recovers only the critical volumes that are part of the System State.</span></span> <span data-ttu-id="bb311-225">非系統資料全都會遭到清除。</span><span class="sxs-lookup"><span data-stu-id="bb311-225">All non-System data is erased.</span></span>

    ```
    Wbadmin start recovery -items:C: -itemtype:Volume -version:<Backupversion> -backuptarget:<backup target volume>
    ```
     ![取得系統狀態備份版本](./media/backup-azure-restore-system-state/winre-6.png)



## <a name="next-steps"></a><span data-ttu-id="bb311-227">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bb311-227">Next steps</span></span>
* <span data-ttu-id="bb311-228">現在您已復原檔案和資料夾，接下來您可以 [管理您的備份](backup-azure-manage-windows-server.md)。</span><span class="sxs-lookup"><span data-stu-id="bb311-228">Now that you've recovered your files and folders, you can [manage your backups](backup-azure-manage-windows-server.md).</span></span>
