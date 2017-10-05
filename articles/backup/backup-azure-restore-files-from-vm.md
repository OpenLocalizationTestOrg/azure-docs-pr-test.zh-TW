---
title: "Azure 備份︰從 Azure VM 備份復原檔案和資料夾 | Microsoft Docs"
description: "從 Azure 虛擬機器的復原點復原檔案"
services: backup
documentationcenter: dev-center-name
author: pvrk
manager: shivamg
keywords: "項目層級復原；從 Azure VM 備份檔案復原；從 Azure VM 中還原檔案"
ms.assetid: f1c067a2-4826-4da4-b97a-c5fd6c189a77
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/20/2017
ms.author: pullabhk;markgal
ms.openlocfilehash: ae7c345c11a7db25413d60ad822f16f84ca37362
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="recover-files-from-azure-virtual-machine-backup"></a><span data-ttu-id="ae111-104">從 Azure 虛擬機器備份復原檔案</span><span class="sxs-lookup"><span data-stu-id="ae111-104">Recover files from Azure virtual machine backup</span></span>

<span data-ttu-id="ae111-105">Azure 備份能夠讓您從 Azure VM 備份還原 [Azure VM 和磁碟](./backup-azure-arm-restore-vms.md)。</span><span class="sxs-lookup"><span data-stu-id="ae111-105">Azure backup provides the capability to restore [Azure VMs and disks](./backup-azure-arm-restore-vms.md) from Azure VM backups.</span></span> <span data-ttu-id="ae111-106">現在本文說明如何從 Azure VM 備份復原檔案和資料夾等項目。</span><span class="sxs-lookup"><span data-stu-id="ae111-106">Now this article explains how you can recover items such as files and folders from an Azure VM backup.</span></span>

> [!Note]
> <span data-ttu-id="ae111-107">這項功能可使用 Resource Manager 模式供 Azure VM 部署使用，而且受保護復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="ae111-107">This feature is available for Azure VMs deployed using the Resource Manager model and protected to a Recovery services vault.</span></span>
> <span data-ttu-id="ae111-108">不支援從加密 VM 備份的檔案復原。</span><span class="sxs-lookup"><span data-stu-id="ae111-108">File recovery from an encrypted VM backup is not supported.</span></span>
>

## <a name="mount-the-volume-and-copy-files"></a><span data-ttu-id="ae111-109">掛接磁碟區和複製檔案</span><span class="sxs-lookup"><span data-stu-id="ae111-109">Mount the volume and copy files</span></span>

1. <span data-ttu-id="ae111-110">登入 [Azure 入口網站](http://portal.Azure.com)。</span><span class="sxs-lookup"><span data-stu-id="ae111-110">Sign into the [Azure portal](http://portal.Azure.com).</span></span> <span data-ttu-id="ae111-111">尋找相關的復原服務保存庫和必要的備份項目。</span><span class="sxs-lookup"><span data-stu-id="ae111-111">Find the relevant Recovery services vault and the required backup item.</span></span>

2. <span data-ttu-id="ae111-112">在 [備份項目] 刀鋒視窗中，按一下 [檔案修復]。</span><span class="sxs-lookup"><span data-stu-id="ae111-112">On the Backup Item blade, click **File Recovery**</span></span>

    ![開啟復原服務保存庫備份項目](./media/backup-azure-restore-files-from-vm/open-vault-item.png)

    <span data-ttu-id="ae111-114">[檔案復原] 刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="ae111-114">The **File Recovery** blade opens.</span></span>

    ![[檔案復原] 刀鋒視窗](./media/backup-azure-restore-files-from-vm/file-recovery-blade.png)

3. <span data-ttu-id="ae111-116">從 [選取復原點] 下拉式選單中，選取包含您所需檔案的復原點。</span><span class="sxs-lookup"><span data-stu-id="ae111-116">From the **Select recovery point** drop-down menu, select the recovery point that contains the files you want.</span></span> <span data-ttu-id="ae111-117">根據預設，已選取最近的復原點。</span><span class="sxs-lookup"><span data-stu-id="ae111-117">By default, the latest recovery point is already selected.</span></span>

4. <span data-ttu-id="ae111-118">按一下 [下載可執行檔] \(若為 Windows Azure VM) 或 [下載指令碼] \(若為 Linux Azure VM) 下載您要用來從復原點複製檔案的軟體。</span><span class="sxs-lookup"><span data-stu-id="ae111-118">Click **Download Executable** (for Windows Azure VM) or **Download Script** (for Linux Azure VM) to download the software that you'll use to copy files from the recovery point.</span></span>

  <span data-ttu-id="ae111-119">可執行檔/指令碼會在本機電腦和指定復原點之間建立連線。</span><span class="sxs-lookup"><span data-stu-id="ae111-119">The executable/script creates a connection between the local computer and the specified recovery point.</span></span>

5. <span data-ttu-id="ae111-120">您需要有密碼才能執行下載的指令碼/可執行檔。</span><span class="sxs-lookup"><span data-stu-id="ae111-120">You need a password to run the downloaded script/executable.</span></span> <span data-ttu-id="ae111-121">您可以使用所產生密碼旁邊的 [複製] 按鈕，從入口網站複製密碼。</span><span class="sxs-lookup"><span data-stu-id="ae111-121">You can copy the password from the portal using the copy button beside the generated password</span></span>

    ![產生的密碼](./media/backup-azure-restore-files-from-vm/generated-pswd.png)

6. <span data-ttu-id="ae111-123">在您要復原檔案的電腦上，執行可執行檔/指令碼。</span><span class="sxs-lookup"><span data-stu-id="ae111-123">On the computer where you want to recover the files, run the executable/script.</span></span> <span data-ttu-id="ae111-124">您必須以系統管理員認證來執行它。</span><span class="sxs-lookup"><span data-stu-id="ae111-124">You must run it with Administrator credentials.</span></span> <span data-ttu-id="ae111-125">如果您在具有限制存取的電腦上執行指令碼，請確定可存取︰</span><span class="sxs-lookup"><span data-stu-id="ae111-125">If you run the script on a computer with restricted access, ensure there is access to:</span></span>

    - <span data-ttu-id="ae111-126">download.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="ae111-126">download.microsoft.com</span></span>
    - <span data-ttu-id="ae111-127">用於 Azure VM 備份的 Azure 端點</span><span class="sxs-lookup"><span data-stu-id="ae111-127">Azure endpoints used for Azure VM backups</span></span>
    - <span data-ttu-id="ae111-128">輸出連接埠 3260</span><span class="sxs-lookup"><span data-stu-id="ae111-128">outbound port 3260</span></span>

   <span data-ttu-id="ae111-129">若為 Linux，指令碼需要 'open-iscsi' 和 'lshw' 元件來連接到復原點。</span><span class="sxs-lookup"><span data-stu-id="ae111-129">For Linux, the script requires 'open-iscsi' and 'lshw' components to connect to the recovery point.</span></span> <span data-ttu-id="ae111-130">如果這些不存在其所執行的電腦上，它會要求安裝相關元件的權限，並在同意下加以安裝。</span><span class="sxs-lookup"><span data-stu-id="ae111-130">If those do not exist on the machine where it is run, it asks for permission to install the relevant components and installs them upon consent.</span></span>
   
   <span data-ttu-id="ae111-131">出現提示時，輸入從入口網站複製的密碼。</span><span class="sxs-lookup"><span data-stu-id="ae111-131">Enter the password copied from the portal when prompted.</span></span> <span data-ttu-id="ae111-132">輸入有效的密碼後，指令碼會連接到復原點。</span><span class="sxs-lookup"><span data-stu-id="ae111-132">Once the valid password is entered the scripts connects to the recovery point.</span></span>
      
    ![[檔案復原] 刀鋒視窗](./media/backup-azure-restore-files-from-vm/executable-output.png)
    
   
   <span data-ttu-id="ae111-134">您可以在任何具有與備份 VM 相的 (或相容) 作業系統的電腦上執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="ae111-134">You can run the script on any machine that has the same (or compatible) operating system as the backed-up VM.</span></span> <span data-ttu-id="ae111-135">請參閱[相容作業系統資料表](backup-azure-restore-files-from-vm.md#compatible-os)以查看相容的作業系統。</span><span class="sxs-lookup"><span data-stu-id="ae111-135">See the [Compatible OS table](backup-azure-restore-files-from-vm.md#compatible-os) for compatible operating systems.</span></span> <span data-ttu-id="ae111-136">如果受保護的 Azure 虛擬機器使用 Windows 儲存空間 (若為 Windows Azure VM) 或 LVM/RAID 陣列 (若為 Linux VM)，則您無法在相同的虛擬機器上執行可執行檔/指令碼。</span><span class="sxs-lookup"><span data-stu-id="ae111-136">If the protected Azure virtual machine uses Windows Storage Spaces (for Windows Azure VMs) or LVM/RAID Arrays(for Linux VMs), then you can't run the executable/script on the same virtual machine.</span></span> <span data-ttu-id="ae111-137">相反地，在任何其他具有相容作業系統上的電腦執行它。</span><span class="sxs-lookup"><span data-stu-id="ae111-137">Instead, run it on any other machine with a compatible operating system.</span></span>

### <a name="compatible-os"></a><span data-ttu-id="ae111-138">相容的作業系統</span><span class="sxs-lookup"><span data-stu-id="ae111-138">Compatible OS</span></span>

#### <a name="for-windows"></a><span data-ttu-id="ae111-139">若為 Windows</span><span class="sxs-lookup"><span data-stu-id="ae111-139">For Windows</span></span>

<span data-ttu-id="ae111-140">下表顯示伺服器和電腦作業系統之間的相容性。</span><span class="sxs-lookup"><span data-stu-id="ae111-140">The following table shows the compatibility between server and computer operating systems.</span></span> <span data-ttu-id="ae111-141">當復原檔案時，您無法還原不相容作業系統之間的檔案。</span><span class="sxs-lookup"><span data-stu-id="ae111-141">When recovering files, you can't restore files between incompatible operating systems.</span></span>

|<span data-ttu-id="ae111-142">伺服器作業系統</span><span class="sxs-lookup"><span data-stu-id="ae111-142">Server OS</span></span> | <span data-ttu-id="ae111-143">相容的用戶端作業系統</span><span class="sxs-lookup"><span data-stu-id="ae111-143">Compatible client OS</span></span>  |
| --------------- | ---- |
| <span data-ttu-id="ae111-144">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="ae111-144">Windows Server 2012 R2</span></span> | <span data-ttu-id="ae111-145">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="ae111-145">Windows 8.1</span></span> |
| <span data-ttu-id="ae111-146">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="ae111-146">Windows Server 2012</span></span>    | <span data-ttu-id="ae111-147">Windows 8</span><span class="sxs-lookup"><span data-stu-id="ae111-147">Windows 8</span></span>  |
| <span data-ttu-id="ae111-148">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="ae111-148">Windows Server 2008 R2</span></span> | <span data-ttu-id="ae111-149">Windows 7</span><span class="sxs-lookup"><span data-stu-id="ae111-149">Windows 7</span></span>   |

#### <a name="for-linux"></a><span data-ttu-id="ae111-150">若為 Linux</span><span class="sxs-lookup"><span data-stu-id="ae111-150">For Linux</span></span>

<span data-ttu-id="ae111-151">在 Linux 中，基本要求是指令碼在其中執行之電腦的作業系統應該支援備份 Linux VM 中出現之檔案的檔案系統。</span><span class="sxs-lookup"><span data-stu-id="ae111-151">In Linux, the fundamental requirement is that the OS of the machine where the script is run should support the filesystem of the files present in the backed-up Linux VM.</span></span> <span data-ttu-id="ae111-152">當選取電腦以執行指令碼時，請確定它有相容的作業系統和下表中所述的版本。</span><span class="sxs-lookup"><span data-stu-id="ae111-152">While selecting a machine to run the script, please ensure it has the compatible OS and the versions as mentioned in the table below.</span></span>

|<span data-ttu-id="ae111-153">Linux 作業系統</span><span class="sxs-lookup"><span data-stu-id="ae111-153">Linux OS</span></span> | <span data-ttu-id="ae111-154">版本</span><span class="sxs-lookup"><span data-stu-id="ae111-154">Versions</span></span>  |
| --------------- | ---- |
| <span data-ttu-id="ae111-155">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="ae111-155">Ubuntu</span></span> | <span data-ttu-id="ae111-156">12.04 和更新版本</span><span class="sxs-lookup"><span data-stu-id="ae111-156">12.04 and above</span></span> |
| <span data-ttu-id="ae111-157">CentOS</span><span class="sxs-lookup"><span data-stu-id="ae111-157">CentOS</span></span> | <span data-ttu-id="ae111-158">6.5 和更新版本</span><span class="sxs-lookup"><span data-stu-id="ae111-158">6.5 and above</span></span>  |
| <span data-ttu-id="ae111-159">RHEL</span><span class="sxs-lookup"><span data-stu-id="ae111-159">RHEL</span></span> | <span data-ttu-id="ae111-160">6.7 和更新版本</span><span class="sxs-lookup"><span data-stu-id="ae111-160">6.7 and above</span></span> |
| <span data-ttu-id="ae111-161">Debian</span><span class="sxs-lookup"><span data-stu-id="ae111-161">Debian</span></span> | <span data-ttu-id="ae111-162">7 和更新版本</span><span class="sxs-lookup"><span data-stu-id="ae111-162">7 and above</span></span> |
| <span data-ttu-id="ae111-163">Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="ae111-163">Oracle Linux</span></span> | <span data-ttu-id="ae111-164">6.4 和更新版本</span><span class="sxs-lookup"><span data-stu-id="ae111-164">6.4 and above</span></span> |

<span data-ttu-id="ae111-165">指令碼也需要 Python 和 Bash 元件來執行，並安全地連接到復原點。</span><span class="sxs-lookup"><span data-stu-id="ae111-165">The script also requires python and bash components to execute and connect securely to the recovery point.</span></span>

|<span data-ttu-id="ae111-166">元件</span><span class="sxs-lookup"><span data-stu-id="ae111-166">Component</span></span> | <span data-ttu-id="ae111-167">版本</span><span class="sxs-lookup"><span data-stu-id="ae111-167">Version</span></span>  |
| --------------- | ---- |
| <span data-ttu-id="ae111-168">Bash</span><span class="sxs-lookup"><span data-stu-id="ae111-168">bash</span></span> | <span data-ttu-id="ae111-169">4 和更新版本</span><span class="sxs-lookup"><span data-stu-id="ae111-169">4 and above</span></span> |
| <span data-ttu-id="ae111-170">Python</span><span class="sxs-lookup"><span data-stu-id="ae111-170">python</span></span> | <span data-ttu-id="ae111-171">2.6.6 和更新版本</span><span class="sxs-lookup"><span data-stu-id="ae111-171">2.6.6 and above</span></span>  |


### <a name="identifying-volumes"></a><span data-ttu-id="ae111-172">識別磁碟區</span><span class="sxs-lookup"><span data-stu-id="ae111-172">Identifying Volumes</span></span>

#### <a name="for-windows"></a><span data-ttu-id="ae111-173">若為 Windows</span><span class="sxs-lookup"><span data-stu-id="ae111-173">For Windows</span></span>

<span data-ttu-id="ae111-174">當您執行可執行檔時，作業系統會掛接新磁碟區，並指派磁碟機代號。</span><span class="sxs-lookup"><span data-stu-id="ae111-174">When you run the exectuable, the operating system mounts the new volumes and assigns drive letters.</span></span> <span data-ttu-id="ae111-175">您可以使用 Windows 檔案總管或檔案總管來瀏覽這些磁碟機。</span><span class="sxs-lookup"><span data-stu-id="ae111-175">You can use Windows Explorer or File Explorer to browse those drives.</span></span> <span data-ttu-id="ae111-176">指派給磁碟區的磁碟機代號可能與原始虛擬機器為不同的代號，不過，系統會保留磁碟區名稱。</span><span class="sxs-lookup"><span data-stu-id="ae111-176">The drive letters assigned to the volumes may not be the same letters as the original virtual machine, however, the volume name is preserved.</span></span> <span data-ttu-id="ae111-177">例如，如果原始虛擬機器上的磁碟區是 “資料磁碟機 (E:\)”，則該磁碟區可以在本機電腦上附加做為 “資料磁碟機 ('任何可用的磁碟機代號':\)。</span><span class="sxs-lookup"><span data-stu-id="ae111-177">For example, if the volume on the original virtual machine was “Data Disk (E:\)”, that volume can be attached as “Data Disk ('Any drive letter available':\) on the local computer.</span></span> <span data-ttu-id="ae111-178">瀏覽指令碼輸出中所提及的所有磁碟區，直到找出您的檔案/資料夾。</span><span class="sxs-lookup"><span data-stu-id="ae111-178">Browse through all volumes mentioned in the script output until you find your files/folder.</span></span>  
       
   ![[檔案復原] 刀鋒視窗](./media/backup-azure-restore-files-from-vm/volumes-attached.png)
           
#### <a name="for-linux"></a><span data-ttu-id="ae111-180">若為 Linux</span><span class="sxs-lookup"><span data-stu-id="ae111-180">For Linux</span></span>

<span data-ttu-id="ae111-181">在 Linux 中，復原點的磁碟區會掛接到執行指令碼的資料夾。</span><span class="sxs-lookup"><span data-stu-id="ae111-181">In Linux, the volumes of the recovery point are mounted to the folder where the script is run.</span></span> <span data-ttu-id="ae111-182">連結的磁碟、磁碟區和對應的掛接路徑會相應顯示。</span><span class="sxs-lookup"><span data-stu-id="ae111-182">The attached disks, volumes and the corresponding mount paths are shown accordingly.</span></span> <span data-ttu-id="ae111-183">具有根層級存取權的使用者都看得到這些掛接路徑。</span><span class="sxs-lookup"><span data-stu-id="ae111-183">These mount paths are visible to users having root level access.</span></span> <span data-ttu-id="ae111-184">在指令碼輸出中瀏覽所述的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="ae111-184">Browse through the volumes mentioned in the script output.</span></span>

  ![Linux [檔案復原] 刀鋒視窗](./media/backup-azure-restore-files-from-vm/linux-mount-paths.png)
  

## <a name="closing-the-connection"></a><span data-ttu-id="ae111-186">關閉連線</span><span class="sxs-lookup"><span data-stu-id="ae111-186">Closing the connection</span></span>

<span data-ttu-id="ae111-187">在識別檔案並將它們複製到本機儲存體位置之後，移除 (或卸載) 其他磁碟機。</span><span class="sxs-lookup"><span data-stu-id="ae111-187">After identifying the files and copying them to a local storage location, remove (or unmount) the additional drives.</span></span> <span data-ttu-id="ae111-188">若要卸載磁碟機，在 Azure 入口網站的 [檔案復原] 刀鋒視窗中，按一下 [取消掛接磁碟]。</span><span class="sxs-lookup"><span data-stu-id="ae111-188">To unmount the drives, on the **File Recovery** blade in the Azure portal, click **Unmount Disks**.</span></span>

![取消掛接磁碟](./media/backup-azure-restore-files-from-vm/unmount-disks3.png)

<span data-ttu-id="ae111-190">一旦卸載磁碟後，您會收到一則訊息，告知您已順利完成。</span><span class="sxs-lookup"><span data-stu-id="ae111-190">Once the disks have been unmounted, you receive a message letting you know it was successful.</span></span> <span data-ttu-id="ae111-191">連線可能需要幾分鐘重新整理，以讓您可以移除磁碟。</span><span class="sxs-lookup"><span data-stu-id="ae111-191">It may take a few minutes for the connection to refresh so that you can remove the disks.</span></span>

<span data-ttu-id="ae111-192">在 Linux 中，復原點的連線嚴重損毀之後，作業系統並不會自動移除對應的掛接路徑。</span><span class="sxs-lookup"><span data-stu-id="ae111-192">In Linux, after the connection to the recovery point is severed, the OS doesn't remove the corresponding mount paths automatically.</span></span> <span data-ttu-id="ae111-193">這些做為「字串」磁碟區存在且它們會顯示，但當您存取/寫入檔案時會擲回錯誤。</span><span class="sxs-lookup"><span data-stu-id="ae111-193">These exist as "orphan" volumes and they are visible but throw an error when you access/write the files.</span></span> <span data-ttu-id="ae111-194">可以手動移除它們。</span><span class="sxs-lookup"><span data-stu-id="ae111-194">They can be manually removed.</span></span> <span data-ttu-id="ae111-195">指令碼執行時，會從任何先前的復原點識別任何這類現有的磁碟區，並在同意下將它們清除。</span><span class="sxs-lookup"><span data-stu-id="ae111-195">The script, when run, identifies any such volumes existing from any previous recovery points and cleans them up upon consent.</span></span>

## <a name="special-configurations"></a><span data-ttu-id="ae111-196">特殊的組態</span><span class="sxs-lookup"><span data-stu-id="ae111-196">Special configurations</span></span>

### <a name="dynamic-disks"></a><span data-ttu-id="ae111-197">動態磁碟</span><span class="sxs-lookup"><span data-stu-id="ae111-197">Dynamic Disks</span></span>

<span data-ttu-id="ae111-198">如果備份的 Azure VM 具有跨越多個磁碟 (跨距與等量磁碟區) 及/或跨越動態磁碟上多個容錯磁碟區 (鏡像與 RAID 5 磁碟區) 的磁碟區，您將無法在相同的 VM 上執行可執行的指令碼。</span><span class="sxs-lookup"><span data-stu-id="ae111-198">If the Azure VM that was backed up has volumes that span multiple disks (spanned and striped volumes) and/or fault-tolerant volumes (mirrored and RAID-5 volumes) on dynamic disks, then you can't run the executable script on the same VM.</span></span> <span data-ttu-id="ae111-199">相反地，在任何其他具有相容作業系統上的電腦執行可執行的指令碼。</span><span class="sxs-lookup"><span data-stu-id="ae111-199">Instead, run the executable script on any other machine with a compatible operating system.</span></span>

### <a name="windows-storage-spaces"></a><span data-ttu-id="ae111-200">Windows 儲存空間</span><span class="sxs-lookup"><span data-stu-id="ae111-200">Windows Storage Spaces</span></span>

<span data-ttu-id="ae111-201">Windows 儲存空間是 Windows 儲存體中的一種技術，可讓您虛擬化儲存體。</span><span class="sxs-lookup"><span data-stu-id="ae111-201">Windows Storage Spaces is a technology in Windows storage that enables you to virtualize storage.</span></span> <span data-ttu-id="ae111-202">您可以利用 Windows 儲存空間將工業標準磁碟群組為儲存體集區，然後從這些儲存體集區中的可用空間建立虛擬磁碟，稱為儲存空間。</span><span class="sxs-lookup"><span data-stu-id="ae111-202">With Windows Storage Spaces you can group industry-standard disks into storage pools, and then create virtual disks, called storage spaces, from the available space in those storage pools.</span></span>

<span data-ttu-id="ae111-203">如果備份的 Azure VM 使用 Windows 儲存空間，則您無法在相同的虛擬機器上執行可執行的指令碼。</span><span class="sxs-lookup"><span data-stu-id="ae111-203">If the Azure VM that was backed up uses Windows Storage Spaces, then you can't run the executable script on the same VM.</span></span> <span data-ttu-id="ae111-204">相反地，在任何其他具有相容作業系統上的電腦執行可執行的指令碼。</span><span class="sxs-lookup"><span data-stu-id="ae111-204">Instead, run the executable script on any other machine with a compatible operating system.</span></span>

### <a name="lvmraid-arrays"></a><span data-ttu-id="ae111-205">LVM/RAID 陣列</span><span class="sxs-lookup"><span data-stu-id="ae111-205">LVM/RAID Arrays</span></span>

<span data-ttu-id="ae111-206">在 Linux 中，邏輯磁碟區管理員 (LVM) 和/或軟體 RAID 陣列會用來管理多個磁碟的邏輯磁碟區。</span><span class="sxs-lookup"><span data-stu-id="ae111-206">In Linux, Logical volume manager (LVM) and/or software RAID Arrays are used to manage logical volumes over multiple disks.</span></span> <span data-ttu-id="ae111-207">如果備份的 Linux VM 使用 LVM 和/或 RAID 陣列，您無法在相同的 VM 上執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="ae111-207">If the backed up Linux VM uses LVM and/or RAID Arrays, you can't run the script on the same VM.</span></span> <span data-ttu-id="ae111-208">改為在任何其他具有相容作業系統，且其可支援備份 VM 之檔案系統的電腦上執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="ae111-208">Instead run the script on any other machine with compatible OS and which supports filesystem of the backed up VM.</span></span>

<span data-ttu-id="ae111-209">指令碼輸出會顯示 LVM 和/或 RAID 陣列磁碟和具有如下所示的磁碟分割類型之磁碟區</span><span class="sxs-lookup"><span data-stu-id="ae111-209">The script output displays the LVM and/or RAID Arrays disks and the volumes with the partition type as shown below</span></span>

   ![Linux LVM 輸出刀鋒視窗](./media/backup-azure-restore-files-from-vm/linux-LVMOutput.png)
   
<span data-ttu-id="ae111-211">下列命令必須由使用者執行使這些磁碟分割上線。</span><span class="sxs-lookup"><span data-stu-id="ae111-211">The following commands need to be run by the user to bring these partitions online.</span></span> 

<span data-ttu-id="ae111-212">**若為 LVM 磁碟分割**</span><span class="sxs-lookup"><span data-stu-id="ae111-212">**For LVM Partitions**</span></span>

```
$ pvs <volume name as shown above in the script output> 
```
<span data-ttu-id="ae111-213">這會列出實體磁碟區下的磁碟區群組名稱。</span><span class="sxs-lookup"><span data-stu-id="ae111-213">This lists the volume group names under a physical volume.</span></span>

```
$ lvdisplay <volume-group-name from the pvs command’s results> 
```
<span data-ttu-id="ae111-214">這會列出所有邏輯磁碟區、名稱和其磁碟區群組中的路徑。</span><span class="sxs-lookup"><span data-stu-id="ae111-214">This lists all logical volumes, names and their paths in a volume group.</span></span>

```
$ mount <LV path> </mountpath>
```
<span data-ttu-id="ae111-215">若要掛接邏輯磁碟區至您所選擇的路徑。</span><span class="sxs-lookup"><span data-stu-id="ae111-215">To mount the logical volumes to the path of your choice.</span></span>


<span data-ttu-id="ae111-216">**若為 RAID 陣列**</span><span class="sxs-lookup"><span data-stu-id="ae111-216">**For RAID Arrays**</span></span>

```
$ mdadm –detail –scan
```
<span data-ttu-id="ae111-217">這會顯示有關所有 RAID 磁碟的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="ae111-217">This displays details about all raid disks.</span></span> <span data-ttu-id="ae111-218">相關的 RAID 磁碟將顯示為 `/dev/mdm/<RAID array name in the backed up VM>`</span><span class="sxs-lookup"><span data-stu-id="ae111-218">The relevant RAID disk will be displayed as `/dev/mdm/<RAID array name in the backed up VM>`</span></span>

<span data-ttu-id="ae111-219">如果 RAID 磁碟具有實體磁碟區，請使用掛接命令。</span><span class="sxs-lookup"><span data-stu-id="ae111-219">Use the mount command if the RAID disk has physical volumes.</span></span>
```
$ mount [RAID Disk Path] [/mounthpath]
```

<span data-ttu-id="ae111-220">如果此 RAID 磁碟有另一個在其中配置的 LVM，則針對具有磁碟區名稱為 RAID 磁碟名稱的 LVM 磁碟分割，遵循如上面所述的相同程序</span><span class="sxs-lookup"><span data-stu-id="ae111-220">If this RAID disk has another LVM configured in it then follow the same procedure as outlined above for LVM partitions with the volume name being the RAID Disk name</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="ae111-221">疑難排解</span><span class="sxs-lookup"><span data-stu-id="ae111-221">Troubleshooting</span></span>

<span data-ttu-id="ae111-222">如果您從虛擬機器復原檔案時遇到問題，請檢查下表中的其他資訊。</span><span class="sxs-lookup"><span data-stu-id="ae111-222">If you have problems while recovering files from the virtual machines, check the following table for additional information.</span></span>

| <span data-ttu-id="ae111-223">錯誤訊息 / 案例</span><span class="sxs-lookup"><span data-stu-id="ae111-223">Error Message / Scenario</span></span> | <span data-ttu-id="ae111-224">可能的原因</span><span class="sxs-lookup"><span data-stu-id="ae111-224">Probable Cause</span></span> | <span data-ttu-id="ae111-225">建議的動作</span><span class="sxs-lookup"><span data-stu-id="ae111-225">Recommended action</span></span> |
| ------------------------ | -------------- | ------------------ |
| <span data-ttu-id="ae111-226">Exe 輸出︰連線到目標的例外狀況</span><span class="sxs-lookup"><span data-stu-id="ae111-226">Exe output: *Exception connecting to the target*</span></span> |<span data-ttu-id="ae111-227">指令碼無法存取復原點</span><span class="sxs-lookup"><span data-stu-id="ae111-227">Script is not able to access the recovery point</span></span> | <span data-ttu-id="ae111-228">檢查電腦是否符合上述的存取需求</span><span class="sxs-lookup"><span data-stu-id="ae111-228">Check whether the machine fulfills the access requirements mentioned above</span></span>|  
|   <span data-ttu-id="ae111-229">Exe 輸出︰目標已透過 ISCSI 工作階段登入。</span><span class="sxs-lookup"><span data-stu-id="ae111-229">Exe output: *The target has already been logged in via an ISCSI session.*</span></span> | <span data-ttu-id="ae111-230">指令碼已在相同電腦上執行，並已附加磁碟機</span><span class="sxs-lookup"><span data-stu-id="ae111-230">The script was already executed on the same machine and the drives have been attached</span></span> | <span data-ttu-id="ae111-231">復原點磁碟區已連接。</span><span class="sxs-lookup"><span data-stu-id="ae111-231">The volumes of the recovery point have already been attached.</span></span> <span data-ttu-id="ae111-232">它們可能未使用原始 VM 的相同磁碟機代號裝載。</span><span class="sxs-lookup"><span data-stu-id="ae111-232">They may NOT be mounted with the same drive letters of the original VM.</span></span> <span data-ttu-id="ae111-233">在檔案總管中的檔案瀏覽所有可用的磁碟區</span><span class="sxs-lookup"><span data-stu-id="ae111-233">Browse through all the available volumes in the file explorer for your file</span></span> |
| <span data-ttu-id="ae111-234">Exe 輸出︰這個指令碼無效，因為磁碟已透過入口網站/超過 12 小時限制卸載。請從入口網站下載新的指令碼。</span><span class="sxs-lookup"><span data-stu-id="ae111-234">Exe output: *This script is invalid because the disks have been dismounted via portal/exceeded the 12-hr limit. Please download a new script from the portal.*</span></span> |  <span data-ttu-id="ae111-235">已從入口網站卸載磁碟或超過 12 小時的限制</span><span class="sxs-lookup"><span data-stu-id="ae111-235">The disks have been dismounted from the portal or the 12-hr limit exceeded</span></span> |    <span data-ttu-id="ae111-236">此特定 exe 目前無效，無法執行。</span><span class="sxs-lookup"><span data-stu-id="ae111-236">This particular exe is now invalid and can’t be run.</span></span> <span data-ttu-id="ae111-237">如果您想要存取該復原點時間的檔案，請瀏覽新 exe 的入口網站</span><span class="sxs-lookup"><span data-stu-id="ae111-237">If you want to access the files of that recovery point-in-time, visit the portal for a new exe</span></span>|
| <span data-ttu-id="ae111-238">在執行 exe 的電腦上︰按一下 [卸載] 按鈕之後不會卸載新的磁碟區</span><span class="sxs-lookup"><span data-stu-id="ae111-238">On the machine where the exe is run: The new volumes are not dismounted after the dismount button is clicked</span></span> |    <span data-ttu-id="ae111-239">電腦上的 ISCSI 啟動器沒有回應/重新整理其與目標之連接及維護快取</span><span class="sxs-lookup"><span data-stu-id="ae111-239">The ISCSI initiator on the machine is not responding/refreshing its connection to the target and maintaining the cache</span></span> |    <span data-ttu-id="ae111-240">按下 [卸載] 按鈕後等候幾分鐘。</span><span class="sxs-lookup"><span data-stu-id="ae111-240">Wait for some mins after the dismount button is pressed.</span></span> <span data-ttu-id="ae111-241">如果仍無法卸載新磁碟區，請瀏覽的所有磁碟區。</span><span class="sxs-lookup"><span data-stu-id="ae111-241">If the new volumes are still not dismounted, please browse through all the volumes.</span></span> <span data-ttu-id="ae111-242">這會強制啟動器重新整理連接，且會卸載磁碟區，並出現磁碟無法使用的錯誤訊息</span><span class="sxs-lookup"><span data-stu-id="ae111-242">This forces the initiator to refresh the connection and the volume is dismounted with an error message that the disk is not available</span></span>|
| <span data-ttu-id="ae111-243">Exe 輸出︰指令碼成功執行，但指令碼輸出上不會顯示「附加的新磁碟區」</span><span class="sxs-lookup"><span data-stu-id="ae111-243">Exe output: Script is run successfully but “New volumes attached” is not displayed on the script output</span></span> | <span data-ttu-id="ae111-244">這是暫時性的錯誤</span><span class="sxs-lookup"><span data-stu-id="ae111-244">This is a transient error</span></span>   | <span data-ttu-id="ae111-245">磁碟區可能已經附加。</span><span class="sxs-lookup"><span data-stu-id="ae111-245">The volumes would have been already attached.</span></span> <span data-ttu-id="ae111-246">開啟檔案總管以瀏覽。</span><span class="sxs-lookup"><span data-stu-id="ae111-246">Open Explorer to browse.</span></span> <span data-ttu-id="ae111-247">如果您每次都使用同一部電腦執行指令碼，請考慮重新啟動電腦，清單應該會顯示在後續的 exe 執行。</span><span class="sxs-lookup"><span data-stu-id="ae111-247">If you are using the same machine for running scripts every time, consider restarting the machine and the list should be displayed in the subsequent exe runs.</span></span> |
| <span data-ttu-id="ae111-248">Linux 特定︰無法檢視所需的磁碟區</span><span class="sxs-lookup"><span data-stu-id="ae111-248">Linux specific: Not able to view the desired volumes</span></span> | <span data-ttu-id="ae111-249">執行指令碼之電腦的作業系統可能無法辨識備份 VM 的基礎檔案系統</span><span class="sxs-lookup"><span data-stu-id="ae111-249">The OS of the machine where the script is run may not recognize the underlying filesystem of the backed up VM</span></span> | <span data-ttu-id="ae111-250">檢查復原點是否損毀一致還是檔案一致。</span><span class="sxs-lookup"><span data-stu-id="ae111-250">Check whether the recovery point is crash consistent or file-consistent.</span></span> <span data-ttu-id="ae111-251">如果檔案一致，在作業系統可辨識備份 VM 的檔案系統之其他電腦上執行指令碼</span><span class="sxs-lookup"><span data-stu-id="ae111-251">If file consistent, run the script on another machine whose OS recognizes the backed up VM's filesystem</span></span> |
| <span data-ttu-id="ae111-252">Windows 特定︰無法檢視所需的磁碟區</span><span class="sxs-lookup"><span data-stu-id="ae111-252">Windows specific: Not able to view the desired volumes</span></span> | <span data-ttu-id="ae111-253">已連接磁碟，但未設定磁碟區</span><span class="sxs-lookup"><span data-stu-id="ae111-253">The disks may have been attached but the volumes were not configured</span></span> | <span data-ttu-id="ae111-254">從 [磁碟管理] 畫面上，找出與復原點相關的其他磁碟。</span><span class="sxs-lookup"><span data-stu-id="ae111-254">From the disk management screen, identify the additional disks related to the recovery point.</span></span> <span data-ttu-id="ae111-255">如果有任何這些磁碟處於離線狀態，請透過在磁碟上按一下滑鼠右鍵並按一下 [上線]，來嘗試使狀態成為上線</span><span class="sxs-lookup"><span data-stu-id="ae111-255">If any of these disks are in offline state try making them online by right-clicking on the disk and click 'Online'</span></span>|
