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
ms.openlocfilehash: 1a62a0ed83d61272c032ac0377a54099ed118db4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="recover-files-from-azure-virtual-machine-backup"></a><span data-ttu-id="83312-104">從 Azure 虛擬機器備份復原檔案</span><span class="sxs-lookup"><span data-stu-id="83312-104">Recover files from Azure virtual machine backup</span></span>

<span data-ttu-id="83312-105">Azure 備份提供 hello 功能 toorestore [Azure Vm 和磁碟](./backup-azure-arm-restore-vms.md)從 Azure VM 的備份。</span><span class="sxs-lookup"><span data-stu-id="83312-105">Azure backup provides hello capability toorestore [Azure VMs and disks](./backup-azure-arm-restore-vms.md) from Azure VM backups.</span></span> <span data-ttu-id="83312-106">現在本文說明如何從 Azure VM 備份復原檔案和資料夾等項目。</span><span class="sxs-lookup"><span data-stu-id="83312-106">Now this article explains how you can recover items such as files and folders from an Azure VM backup.</span></span>

> [!Note]
> <span data-ttu-id="83312-107">這項功能適用於 Azure Vm 部署使用 hello 資源管理員模型和受保護的 tooa 復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="83312-107">This feature is available for Azure VMs deployed using hello Resource Manager model and protected tooa Recovery services vault.</span></span>
> <span data-ttu-id="83312-108">不支援從加密 VM 備份的檔案復原。</span><span class="sxs-lookup"><span data-stu-id="83312-108">File recovery from an encrypted VM backup is not supported.</span></span>
>

## <a name="mount-hello-volume-and-copy-files"></a><span data-ttu-id="83312-109">掛接 hello 磁碟區和複製檔案</span><span class="sxs-lookup"><span data-stu-id="83312-109">Mount hello volume and copy files</span></span>

1. <span data-ttu-id="83312-110">登入 hello [Azure 入口網站](http://portal.Azure.com)。</span><span class="sxs-lookup"><span data-stu-id="83312-110">Sign into hello [Azure portal](http://portal.Azure.com).</span></span> <span data-ttu-id="83312-111">尋找 hello 相關復原服務保存庫以及所需的 hello 備份項目。</span><span class="sxs-lookup"><span data-stu-id="83312-111">Find hello relevant Recovery services vault and hello required backup item.</span></span>

2. <span data-ttu-id="83312-112">在 hello 備份項目刀鋒視窗中，按一下 **檔案復原**</span><span class="sxs-lookup"><span data-stu-id="83312-112">On hello Backup Item blade, click **File Recovery**</span></span>

    ![開啟復原服務保存庫備份項目](./media/backup-azure-restore-files-from-vm/open-vault-item.png)

    <span data-ttu-id="83312-114">hello**檔案復原**刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="83312-114">hello **File Recovery** blade opens.</span></span>

    ![[檔案復原] 刀鋒視窗](./media/backup-azure-restore-files-from-vm/file-recovery-blade.png)

3. <span data-ttu-id="83312-116">從 hello**選取復原點**想下拉式功能表、 選取 hello 包含 hello 檔案的復原點。</span><span class="sxs-lookup"><span data-stu-id="83312-116">From hello **Select recovery point** drop-down menu, select hello recovery point that contains hello files you want.</span></span> <span data-ttu-id="83312-117">根據預設，已選取 hello 最新的復原點。</span><span class="sxs-lookup"><span data-stu-id="83312-117">By default, hello latest recovery point is already selected.</span></span>

4. <span data-ttu-id="83312-118">按一下**下載可執行檔**（適用於 Windows Azure VM) 或**下載指令碼**（適用於 Linux 的 Azure VM) toodownload hello 軟體，您將使用 toocopy 檔案從 hello 復原點。</span><span class="sxs-lookup"><span data-stu-id="83312-118">Click **Download Executable** (for Windows Azure VM) or **Download Script** (for Linux Azure VM) toodownload hello software that you'll use toocopy files from hello recovery point.</span></span>

  <span data-ttu-id="83312-119">hello/指令碼可執行檔之間建立連接 hello 本機電腦，並指定 hello 復原點。</span><span class="sxs-lookup"><span data-stu-id="83312-119">hello executable/script creates a connection between hello local computer and hello specified recovery point.</span></span>

5. <span data-ttu-id="83312-120">您需要密碼 toorun hello 下載指令碼/可執行檔。</span><span class="sxs-lookup"><span data-stu-id="83312-120">You need a password toorun hello downloaded script/executable.</span></span> <span data-ttu-id="83312-121">您可以從使用 hello 複製 按鈕旁邊 hello 產生密碼的 hello 入口網站複製 hello 密碼</span><span class="sxs-lookup"><span data-stu-id="83312-121">You can copy hello password from hello portal using hello copy button beside hello generated password</span></span>

    ![產生的密碼](./media/backup-azure-restore-files-from-vm/generated-pswd.png)

6. <span data-ttu-id="83312-123">Hello 在電腦上您要 toorecover hello 檔案，執行 hello 可執行檔指令碼。</span><span class="sxs-lookup"><span data-stu-id="83312-123">On hello computer where you want toorecover hello files, run hello executable/script.</span></span> <span data-ttu-id="83312-124">您必須以系統管理員認證來執行它。</span><span class="sxs-lookup"><span data-stu-id="83312-124">You must run it with Administrator credentials.</span></span> <span data-ttu-id="83312-125">如果您具有限制存取的電腦上執行 hello 指令碼，請確定沒有存取權：</span><span class="sxs-lookup"><span data-stu-id="83312-125">If you run hello script on a computer with restricted access, ensure there is access to:</span></span>

    - <span data-ttu-id="83312-126">download.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="83312-126">download.microsoft.com</span></span>
    - <span data-ttu-id="83312-127">用於 Azure VM 備份的 Azure 端點</span><span class="sxs-lookup"><span data-stu-id="83312-127">Azure endpoints used for Azure VM backups</span></span>
    - <span data-ttu-id="83312-128">輸出連接埠 3260</span><span class="sxs-lookup"><span data-stu-id="83312-128">outbound port 3260</span></span>

   <span data-ttu-id="83312-129">適用於 Linux，hello 指令碼需要 ' 開啟 iscsi' 和 'lshw' 元件 tooconnect toohello 復原點。</span><span class="sxs-lookup"><span data-stu-id="83312-129">For Linux, hello script requires 'open-iscsi' and 'lshw' components tooconnect toohello recovery point.</span></span> <span data-ttu-id="83312-130">如果那些 hello 執行所在的電腦上不存在，它會要求權限 tooinstall hello 相關元件，並將它們安裝在同意時。</span><span class="sxs-lookup"><span data-stu-id="83312-130">If those do not exist on hello machine where it is run, it asks for permission tooinstall hello relevant components and installs them upon consent.</span></span>
   
   <span data-ttu-id="83312-131">輸入從 hello 入口網站，當系統提示您複製的 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="83312-131">Enter hello password copied from hello portal when prompted.</span></span> <span data-ttu-id="83312-132">一旦 hello 有效的密碼輸入 hello 指令碼會連接 toohello 復原點。</span><span class="sxs-lookup"><span data-stu-id="83312-132">Once hello valid password is entered hello scripts connects toohello recovery point.</span></span>
      
    ![[檔案復原] 刀鋒視窗](./media/backup-azure-restore-files-from-vm/executable-output.png)
    
   
   <span data-ttu-id="83312-134">您可以在任何具有 hello 相同 （或相容） 的作業系統，因為 hello 備份 VM 的電腦上執行 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="83312-134">You can run hello script on any machine that has hello same (or compatible) operating system as hello backed-up VM.</span></span> <span data-ttu-id="83312-135">請參閱 hello[相容 OS 資料表](backup-azure-restore-files-from-vm.md#compatible-os)相容的作業系統。</span><span class="sxs-lookup"><span data-stu-id="83312-135">See hello [Compatible OS table](backup-azure-restore-files-from-vm.md#compatible-os) for compatible operating systems.</span></span> <span data-ttu-id="83312-136">如果 hello 保護 Azure 虛擬機器會使用 Windows 儲存空間 （適用於 Windows Azure Vm) 或 LVM/RAID Arrays(for Linux VMs)，則您無法在執行 hello 可執行檔指令碼 hello 相同的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="83312-136">If hello protected Azure virtual machine uses Windows Storage Spaces (for Windows Azure VMs) or LVM/RAID Arrays(for Linux VMs), then you can't run hello executable/script on hello same virtual machine.</span></span> <span data-ttu-id="83312-137">相反地，在任何其他具有相容作業系統上的電腦執行它。</span><span class="sxs-lookup"><span data-stu-id="83312-137">Instead, run it on any other machine with a compatible operating system.</span></span>

### <a name="compatible-os"></a><span data-ttu-id="83312-138">相容的作業系統</span><span class="sxs-lookup"><span data-stu-id="83312-138">Compatible OS</span></span>

#### <a name="for-windows"></a><span data-ttu-id="83312-139">若為 Windows</span><span class="sxs-lookup"><span data-stu-id="83312-139">For Windows</span></span>

<span data-ttu-id="83312-140">下列表格顯示 hello 相容性伺服器和電腦的作業系統之間的 hello。</span><span class="sxs-lookup"><span data-stu-id="83312-140">hello following table shows hello compatibility between server and computer operating systems.</span></span> <span data-ttu-id="83312-141">當復原檔案時，您無法還原不相容作業系統之間的檔案。</span><span class="sxs-lookup"><span data-stu-id="83312-141">When recovering files, you can't restore files between incompatible operating systems.</span></span>

|<span data-ttu-id="83312-142">伺服器作業系統</span><span class="sxs-lookup"><span data-stu-id="83312-142">Server OS</span></span> | <span data-ttu-id="83312-143">相容的用戶端作業系統</span><span class="sxs-lookup"><span data-stu-id="83312-143">Compatible client OS</span></span>  |
| --------------- | ---- |
| <span data-ttu-id="83312-144">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="83312-144">Windows Server 2012 R2</span></span> | <span data-ttu-id="83312-145">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="83312-145">Windows 8.1</span></span> |
| <span data-ttu-id="83312-146">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="83312-146">Windows Server 2012</span></span>    | <span data-ttu-id="83312-147">Windows 8</span><span class="sxs-lookup"><span data-stu-id="83312-147">Windows 8</span></span>  |
| <span data-ttu-id="83312-148">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="83312-148">Windows Server 2008 R2</span></span> | <span data-ttu-id="83312-149">Windows 7</span><span class="sxs-lookup"><span data-stu-id="83312-149">Windows 7</span></span>   |

#### <a name="for-linux"></a><span data-ttu-id="83312-150">若為 Linux</span><span class="sxs-lookup"><span data-stu-id="83312-150">For Linux</span></span>

<span data-ttu-id="83312-151">在 Linux hello 基本的需求是 hello 機器 hello 指令碼在何處執行該 hello OS 應該支援 hello filesystem hello 的檔案存在於 hello 備份 Linux VM。</span><span class="sxs-lookup"><span data-stu-id="83312-151">In Linux, hello fundamental requirement is that hello OS of hello machine where hello script is run should support hello filesystem of hello files present in hello backed-up Linux VM.</span></span> <span data-ttu-id="83312-152">當選取的機器 toorun hello 指令碼時，請確定它有 hello 相容的作業系統與 hello 版本 hello 表中所述。</span><span class="sxs-lookup"><span data-stu-id="83312-152">While selecting a machine toorun hello script, please ensure it has hello compatible OS and hello versions as mentioned in hello table below.</span></span>

|<span data-ttu-id="83312-153">Linux 作業系統</span><span class="sxs-lookup"><span data-stu-id="83312-153">Linux OS</span></span> | <span data-ttu-id="83312-154">版本</span><span class="sxs-lookup"><span data-stu-id="83312-154">Versions</span></span>  |
| --------------- | ---- |
| <span data-ttu-id="83312-155">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="83312-155">Ubuntu</span></span> | <span data-ttu-id="83312-156">12.04 和更新版本</span><span class="sxs-lookup"><span data-stu-id="83312-156">12.04 and above</span></span> |
| <span data-ttu-id="83312-157">CentOS</span><span class="sxs-lookup"><span data-stu-id="83312-157">CentOS</span></span> | <span data-ttu-id="83312-158">6.5 和更新版本</span><span class="sxs-lookup"><span data-stu-id="83312-158">6.5 and above</span></span>  |
| <span data-ttu-id="83312-159">RHEL</span><span class="sxs-lookup"><span data-stu-id="83312-159">RHEL</span></span> | <span data-ttu-id="83312-160">6.7 和更新版本</span><span class="sxs-lookup"><span data-stu-id="83312-160">6.7 and above</span></span> |
| <span data-ttu-id="83312-161">Debian</span><span class="sxs-lookup"><span data-stu-id="83312-161">Debian</span></span> | <span data-ttu-id="83312-162">7 和更新版本</span><span class="sxs-lookup"><span data-stu-id="83312-162">7 and above</span></span> |
| <span data-ttu-id="83312-163">Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="83312-163">Oracle Linux</span></span> | <span data-ttu-id="83312-164">6.4 和更新版本</span><span class="sxs-lookup"><span data-stu-id="83312-164">6.4 and above</span></span> |

<span data-ttu-id="83312-165">hello 指令碼也需要 python 和撞元件 tooexecute 並安全地連線 toohello 復原點。</span><span class="sxs-lookup"><span data-stu-id="83312-165">hello script also requires python and bash components tooexecute and connect securely toohello recovery point.</span></span>

|<span data-ttu-id="83312-166">元件</span><span class="sxs-lookup"><span data-stu-id="83312-166">Component</span></span> | <span data-ttu-id="83312-167">版本</span><span class="sxs-lookup"><span data-stu-id="83312-167">Version</span></span>  |
| --------------- | ---- |
| <span data-ttu-id="83312-168">Bash</span><span class="sxs-lookup"><span data-stu-id="83312-168">bash</span></span> | <span data-ttu-id="83312-169">4 和更新版本</span><span class="sxs-lookup"><span data-stu-id="83312-169">4 and above</span></span> |
| <span data-ttu-id="83312-170">Python</span><span class="sxs-lookup"><span data-stu-id="83312-170">python</span></span> | <span data-ttu-id="83312-171">2.6.6 和更新版本</span><span class="sxs-lookup"><span data-stu-id="83312-171">2.6.6 and above</span></span>  |


### <a name="identifying-volumes"></a><span data-ttu-id="83312-172">識別磁碟區</span><span class="sxs-lookup"><span data-stu-id="83312-172">Identifying Volumes</span></span>

#### <a name="for-windows"></a><span data-ttu-id="83312-173">若為 Windows</span><span class="sxs-lookup"><span data-stu-id="83312-173">For Windows</span></span>

<span data-ttu-id="83312-174">當您執行 hello 可執行時，hello 作業系統掛接 hello 新磁碟區，並指派磁碟機代號。</span><span class="sxs-lookup"><span data-stu-id="83312-174">When you run hello exectuable, hello operating system mounts hello new volumes and assigns drive letters.</span></span> <span data-ttu-id="83312-175">您可以使用 Windows 檔案總管或檔案總管 toobrowse 這些磁碟機。</span><span class="sxs-lookup"><span data-stu-id="83312-175">You can use Windows Explorer or File Explorer toobrowse those drives.</span></span> <span data-ttu-id="83312-176">hello 分派 toohello 磁碟區的磁碟機代號可能無法保留相同的字母為 hello 原始虛擬機器，不過，hello 磁碟區名稱的 hello。</span><span class="sxs-lookup"><span data-stu-id="83312-176">hello drive letters assigned toohello volumes may not be hello same letters as hello original virtual machine, however, hello volume name is preserved.</span></span> <span data-ttu-id="83312-177">比方說，如果 hello hello 原始虛擬機器上的磁碟區是 「 資料磁碟 (e:\)"，磁碟區，可以附加為 「 資料磁碟 ('任何可用的磁碟機代號':\) hello 本機電腦上。</span><span class="sxs-lookup"><span data-stu-id="83312-177">For example, if hello volume on hello original virtual machine was “Data Disk (E:\)”, that volume can be attached as “Data Disk ('Any drive letter available':\) on hello local computer.</span></span> <span data-ttu-id="83312-178">瀏覽 hello 指令碼輸出中所述，直到您找到您的檔案/資料夾的所有磁碟區。</span><span class="sxs-lookup"><span data-stu-id="83312-178">Browse through all volumes mentioned in hello script output until you find your files/folder.</span></span>  
       
   ![[檔案復原] 刀鋒視窗](./media/backup-azure-restore-files-from-vm/volumes-attached.png)
           
#### <a name="for-linux"></a><span data-ttu-id="83312-180">若為 Linux</span><span class="sxs-lookup"><span data-stu-id="83312-180">For Linux</span></span>

<span data-ttu-id="83312-181">在 Linux 中 hello hello 復原點磁碟區會掛接的 toohello 資料夾 hello 指令碼執行的位置。</span><span class="sxs-lookup"><span data-stu-id="83312-181">In Linux, hello volumes of hello recovery point are mounted toohello folder where hello script is run.</span></span> <span data-ttu-id="83312-182">hello 附加磁碟、 磁碟區和 hello 相對應的掛接路徑會跟著顯示。</span><span class="sxs-lookup"><span data-stu-id="83312-182">hello attached disks, volumes and hello corresponding mount paths are shown accordingly.</span></span> <span data-ttu-id="83312-183">這些裝載路徑會顯示 toousers 具有根層級存取。</span><span class="sxs-lookup"><span data-stu-id="83312-183">These mount paths are visible toousers having root level access.</span></span> <span data-ttu-id="83312-184">瀏覽 hello hello 指令碼輸出中所述的磁碟區。</span><span class="sxs-lookup"><span data-stu-id="83312-184">Browse through hello volumes mentioned in hello script output.</span></span>

  ![Linux [檔案復原] 刀鋒視窗](./media/backup-azure-restore-files-from-vm/linux-mount-paths.png)
  

## <a name="closing-hello-connection"></a><span data-ttu-id="83312-186">關閉 hello 連接</span><span class="sxs-lookup"><span data-stu-id="83312-186">Closing hello connection</span></span>

<span data-ttu-id="83312-187">識別 hello 檔案，並將它們複製 tooa 本機儲存體位置之後, 移除 （或取消掛接） hello 其他磁碟機。</span><span class="sxs-lookup"><span data-stu-id="83312-187">After identifying hello files and copying them tooa local storage location, remove (or unmount) hello additional drives.</span></span> <span data-ttu-id="83312-188">toounmount hello 上的磁碟機，hello**檔案復原**刀鋒視窗 hello Azure 入口網站中的按一下**取消掛接磁碟**。</span><span class="sxs-lookup"><span data-stu-id="83312-188">toounmount hello drives, on hello **File Recovery** blade in hello Azure portal, click **Unmount Disks**.</span></span>

![取消掛接磁碟](./media/backup-azure-restore-files-from-vm/unmount-disks3.png)

<span data-ttu-id="83312-190">一旦 hello 磁碟已卸載，您會收到訊息，讓您知道已順利完成。</span><span class="sxs-lookup"><span data-stu-id="83312-190">Once hello disks have been unmounted, you receive a message letting you know it was successful.</span></span> <span data-ttu-id="83312-191">如此您就可以移除 hello 磁碟可能需要幾分鐘，讓 hello 連接 toorefresh。</span><span class="sxs-lookup"><span data-stu-id="83312-191">It may take a few minutes for hello connection toorefresh so that you can remove hello disks.</span></span>

<span data-ttu-id="83312-192">在 Linux 中切斷 hello 連接 toohello 復原點之後，hello OS 不 hello 對應的掛接路徑自動移除。</span><span class="sxs-lookup"><span data-stu-id="83312-192">In Linux, after hello connection toohello recovery point is severed, hello OS doesn't remove hello corresponding mount paths automatically.</span></span> <span data-ttu-id="83312-193">這些為 「 字串 」 磁碟區存在，且會顯示，但當您存取/寫入 hello 檔案時，擲回錯誤。</span><span class="sxs-lookup"><span data-stu-id="83312-193">These exist as "orphan" volumes and they are visible but throw an error when you access/write hello files.</span></span> <span data-ttu-id="83312-194">可以手動移除它們。</span><span class="sxs-lookup"><span data-stu-id="83312-194">They can be manually removed.</span></span> <span data-ttu-id="83312-195">hello 指令碼執行時，會識別任何先前的復原點從現有的這類磁碟區，並在同意時將它們清除。</span><span class="sxs-lookup"><span data-stu-id="83312-195">hello script, when run, identifies any such volumes existing from any previous recovery points and cleans them up upon consent.</span></span>

## <a name="special-configurations"></a><span data-ttu-id="83312-196">特殊的組態</span><span class="sxs-lookup"><span data-stu-id="83312-196">Special configurations</span></span>

### <a name="dynamic-disks"></a><span data-ttu-id="83312-197">動態磁碟</span><span class="sxs-lookup"><span data-stu-id="83312-197">Dynamic Disks</span></span>

<span data-ttu-id="83312-198">如果您無法執行 hello 可執行指令碼在 hello 已備份的 Azure VM 有跨越多個磁碟 （跨距與等量磁碟區） 和 （或） 容錯磁碟區 （鏡像與 RAID 5 磁碟區） 動態磁碟上的磁碟區 hello 相同的 VM。</span><span class="sxs-lookup"><span data-stu-id="83312-198">If hello Azure VM that was backed up has volumes that span multiple disks (spanned and striped volumes) and/or fault-tolerant volumes (mirrored and RAID-5 volumes) on dynamic disks, then you can't run hello executable script on hello same VM.</span></span> <span data-ttu-id="83312-199">相反地，在任何其他電腦相容的作業系統上執行 hello 可執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="83312-199">Instead, run hello executable script on any other machine with a compatible operating system.</span></span>

### <a name="windows-storage-spaces"></a><span data-ttu-id="83312-200">Windows 儲存空間</span><span class="sxs-lookup"><span data-stu-id="83312-200">Windows Storage Spaces</span></span>

<span data-ttu-id="83312-201">Windows 儲存空間是一種技術可讓您 toovirtualize 存放裝置的 Windows 儲存體中。</span><span class="sxs-lookup"><span data-stu-id="83312-201">Windows Storage Spaces is a technology in Windows storage that enables you toovirtualize storage.</span></span> <span data-ttu-id="83312-202">與 Windows 儲存空間中，您可以工業標準磁碟群組成儲存集區，然後再建立稱為儲存空間，從這些儲存集區中的 hello 可用空間的虛擬磁碟。</span><span class="sxs-lookup"><span data-stu-id="83312-202">With Windows Storage Spaces you can group industry-standard disks into storage pools, and then create virtual disks, called storage spaces, from hello available space in those storage pools.</span></span>

<span data-ttu-id="83312-203">如果 hello Azure VM 備份會使用 Windows 儲存空間，則您無法執行 hello 可執行指令碼在 hello 相同的 VM。</span><span class="sxs-lookup"><span data-stu-id="83312-203">If hello Azure VM that was backed up uses Windows Storage Spaces, then you can't run hello executable script on hello same VM.</span></span> <span data-ttu-id="83312-204">相反地，在任何其他電腦相容的作業系統上執行 hello 可執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="83312-204">Instead, run hello executable script on any other machine with a compatible operating system.</span></span>

### <a name="lvmraid-arrays"></a><span data-ttu-id="83312-205">LVM/RAID 陣列</span><span class="sxs-lookup"><span data-stu-id="83312-205">LVM/RAID Arrays</span></span>

<span data-ttu-id="83312-206">在 Linux、 邏輯磁碟區管理員 (LVM) 及/或軟體 RAID 陣列會是透過多個磁碟使用的 toomanage 邏輯磁碟區。</span><span class="sxs-lookup"><span data-stu-id="83312-206">In Linux, Logical volume manager (LVM) and/or software RAID Arrays are used toomanage logical volumes over multiple disks.</span></span> <span data-ttu-id="83312-207">如果備份 Linux VM 的 hello 使用 LVM 及/或 RAID 陣列，您無法執行 hello 指令碼在 hello 相同的 VM。</span><span class="sxs-lookup"><span data-stu-id="83312-207">If hello backed up Linux VM uses LVM and/or RAID Arrays, you can't run hello script on hello same VM.</span></span> <span data-ttu-id="83312-208">改為執行任何其他電腦相容的作業系統上的 hello 指令碼，並可支援 hello VM 備份的檔案系統。</span><span class="sxs-lookup"><span data-stu-id="83312-208">Instead run hello script on any other machine with compatible OS and which supports filesystem of hello backed up VM.</span></span>

<span data-ttu-id="83312-209">hello 指令碼輸出會顯示 hello LVM 和/或 RAID 陣列磁碟與 hello hello 分割區類型，如下所示的磁碟區</span><span class="sxs-lookup"><span data-stu-id="83312-209">hello script output displays hello LVM and/or RAID Arrays disks and hello volumes with hello partition type as shown below</span></span>

   ![Linux LVM 輸出刀鋒視窗](./media/backup-azure-restore-files-from-vm/linux-LVMOutput.png)
   
<span data-ttu-id="83312-211">遵循 hello 需要 toobe 執行命令的 hello 使用者 toobring 這些資料分割線上。</span><span class="sxs-lookup"><span data-stu-id="83312-211">hello following commands need toobe run by hello user toobring these partitions online.</span></span> 

<span data-ttu-id="83312-212">**若為 LVM 磁碟分割**</span><span class="sxs-lookup"><span data-stu-id="83312-212">**For LVM Partitions**</span></span>

```
$ pvs <volume name as shown above in hello script output> 
```
<span data-ttu-id="83312-213">這樣就會列出 hello 磁碟區群組名稱下的實體磁區。</span><span class="sxs-lookup"><span data-stu-id="83312-213">This lists hello volume group names under a physical volume.</span></span>

```
$ lvdisplay <volume-group-name from hello pvs command’s results> 
```
<span data-ttu-id="83312-214">這會列出所有邏輯磁碟區、名稱和其磁碟區群組中的路徑。</span><span class="sxs-lookup"><span data-stu-id="83312-214">This lists all logical volumes, names and their paths in a volume group.</span></span>

```
$ mount <LV path> </mountpath>
```
<span data-ttu-id="83312-215">toomount hello 邏輯磁碟區 toohello 路徑您選擇。</span><span class="sxs-lookup"><span data-stu-id="83312-215">toomount hello logical volumes toohello path of your choice.</span></span>


<span data-ttu-id="83312-216">**若為 RAID 陣列**</span><span class="sxs-lookup"><span data-stu-id="83312-216">**For RAID Arrays**</span></span>

```
$ mdadm –detail –scan
```
<span data-ttu-id="83312-217">這會顯示有關所有 RAID 磁碟的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="83312-217">This displays details about all raid disks.</span></span> <span data-ttu-id="83312-218">hello 相關的 RAID 磁碟將會顯示為`/dev/mdm/<RAID array name in hello backed up VM>`</span><span class="sxs-lookup"><span data-stu-id="83312-218">hello relevant RAID disk will be displayed as `/dev/mdm/<RAID array name in hello backed up VM>`</span></span>

<span data-ttu-id="83312-219">如果 hello RAID 磁碟有實體磁碟區，請使用 hello mount 命令。</span><span class="sxs-lookup"><span data-stu-id="83312-219">Use hello mount command if hello RAID disk has physical volumes.</span></span>
```
$ mount [RAID Disk Path] [/mounthpath]
```

<span data-ttu-id="83312-220">如上面所述的 LVM 磁碟分割與 hello hello RAID 磁碟名稱的磁碟區名稱，再依照此 RAID 磁碟是否設定中的另一個 LVM hello 相同的程序</span><span class="sxs-lookup"><span data-stu-id="83312-220">If this RAID disk has another LVM configured in it then follow hello same procedure as outlined above for LVM partitions with hello volume name being hello RAID Disk name</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="83312-221">疑難排解</span><span class="sxs-lookup"><span data-stu-id="83312-221">Troubleshooting</span></span>

<span data-ttu-id="83312-222">如果您從 hello 虛擬機器復原檔案時遇到問題，請檢查 hello 下表，如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="83312-222">If you have problems while recovering files from hello virtual machines, check hello following table for additional information.</span></span>

| <span data-ttu-id="83312-223">錯誤訊息 / 案例</span><span class="sxs-lookup"><span data-stu-id="83312-223">Error Message / Scenario</span></span> | <span data-ttu-id="83312-224">可能的原因</span><span class="sxs-lookup"><span data-stu-id="83312-224">Probable Cause</span></span> | <span data-ttu-id="83312-225">建議的動作</span><span class="sxs-lookup"><span data-stu-id="83312-225">Recommended action</span></span> |
| ------------------------ | -------------- | ------------------ |
| <span data-ttu-id="83312-226">Exe 輸出：*連接 toohello 目標的例外狀況*</span><span class="sxs-lookup"><span data-stu-id="83312-226">Exe output: *Exception connecting toohello target*</span></span> |<span data-ttu-id="83312-227">指令碼不能 tooaccess hello 復原點</span><span class="sxs-lookup"><span data-stu-id="83312-227">Script is not able tooaccess hello recovery point</span></span> | <span data-ttu-id="83312-228">檢查是否 hello 機器符合上面所述的 hello 存取需求</span><span class="sxs-lookup"><span data-stu-id="83312-228">Check whether hello machine fulfills hello access requirements mentioned above</span></span>|  
|   <span data-ttu-id="83312-229">Exe 輸出： *hello 目標已記錄在透過 ISCSI 工作階段。*</span><span class="sxs-lookup"><span data-stu-id="83312-229">Exe output: *hello target has already been logged in via an ISCSI session.*</span></span> |   <span data-ttu-id="83312-230">hello 已經附加相同的電腦和 hello 磁碟機上已執行 hello 指令碼</span><span class="sxs-lookup"><span data-stu-id="83312-230">hello script was already executed on hello same machine and hello drives have been attached</span></span> |   <span data-ttu-id="83312-231">hello hello 復原點磁碟區已連接。</span><span class="sxs-lookup"><span data-stu-id="83312-231">hello volumes of hello recovery point have already been attached.</span></span> <span data-ttu-id="83312-232">可能未裝載以相同的磁碟機代號的 hello hello 原始 VM。</span><span class="sxs-lookup"><span data-stu-id="83312-232">They may NOT be mounted with hello same drive letters of hello original VM.</span></span> <span data-ttu-id="83312-233">瀏覽所有 hello 可用的磁碟區在 hello 檔案總管 中的檔案</span><span class="sxs-lookup"><span data-stu-id="83312-233">Browse through all hello available volumes in hello file explorer for your file</span></span> |
| <span data-ttu-id="83312-234">Exe 輸出：*此指令碼無效，因為透過入口網站/超過 hello 12 hr 限制已解下 hello 磁碟。請從 hello 入口網站下載新的指令碼。*</span><span class="sxs-lookup"><span data-stu-id="83312-234">Exe output: *This script is invalid because hello disks have been dismounted via portal/exceeded hello 12-hr limit. Please download a new script from hello portal.*</span></span> |    <span data-ttu-id="83312-235">從 hello 入口網站或超過 hello 12 hr 限制已解下磁碟 hello</span><span class="sxs-lookup"><span data-stu-id="83312-235">hello disks have been dismounted from hello portal or hello 12-hr limit exceeded</span></span> |  <span data-ttu-id="83312-236">此特定 exe 目前無效，無法執行。</span><span class="sxs-lookup"><span data-stu-id="83312-236">This particular exe is now invalid and can’t be run.</span></span> <span data-ttu-id="83312-237">如果您想 tooaccess hello 該復原點時間的檔案，請瀏覽新的 exe 的 hello 入口網站</span><span class="sxs-lookup"><span data-stu-id="83312-237">If you want tooaccess hello files of that recovery point-in-time, visit hello portal for a new exe</span></span>|
| <span data-ttu-id="83312-238">Hello hello exe 執行所在的電腦上： hello 新磁碟區未卸載之後 hello 卸載按鈕</span><span class="sxs-lookup"><span data-stu-id="83312-238">On hello machine where hello exe is run: hello new volumes are not dismounted after hello dismount button is clicked</span></span> |    <span data-ttu-id="83312-239">hello hello 機器上的 ISCSI 啟動器無法回應/重新整理其連線 toohello 目標及維護 hello 快取</span><span class="sxs-lookup"><span data-stu-id="83312-239">hello ISCSI initiator on hello machine is not responding/refreshing its connection toohello target and maintaining hello cache</span></span> |    <span data-ttu-id="83312-240">等候一些分鐘之後按下 hello 卸載按鈕。</span><span class="sxs-lookup"><span data-stu-id="83312-240">Wait for some mins after hello dismount button is pressed.</span></span> <span data-ttu-id="83312-241">如果仍然無法卸載 hello 新磁碟區，請瀏覽 hello 的所有磁碟區。</span><span class="sxs-lookup"><span data-stu-id="83312-241">If hello new volumes are still not dismounted, please browse through all hello volumes.</span></span> <span data-ttu-id="83312-242">不提供這個 hello 磁碟的強制執行 hello 啟動器 toorefresh hello 連接和 hello 磁碟區卸載並出現錯誤訊息</span><span class="sxs-lookup"><span data-stu-id="83312-242">This forces hello initiator toorefresh hello connection and hello volume is dismounted with an error message that hello disk is not available</span></span>|
| <span data-ttu-id="83312-243">Exe 輸出： 指令碼執行成功，但 「 附加的新磁碟區 」 不會顯示在 hello 指令碼輸出</span><span class="sxs-lookup"><span data-stu-id="83312-243">Exe output: Script is run successfully but “New volumes attached” is not displayed on hello script output</span></span> |   <span data-ttu-id="83312-244">這是暫時性的錯誤</span><span class="sxs-lookup"><span data-stu-id="83312-244">This is a transient error</span></span>   | <span data-ttu-id="83312-245">hello 磁碟區就已附加之後。</span><span class="sxs-lookup"><span data-stu-id="83312-245">hello volumes would have been already attached.</span></span> <span data-ttu-id="83312-246">開啟檔案總管 toobrowse。</span><span class="sxs-lookup"><span data-stu-id="83312-246">Open Explorer toobrowse.</span></span> <span data-ttu-id="83312-247">如果您使用相同電腦的 hello 每次執行指令碼，請考慮重新啟動機器 hello 和 hello 清單應該會顯示在 hello 後續 exe 執行。</span><span class="sxs-lookup"><span data-stu-id="83312-247">If you are using hello same machine for running scripts every time, consider restarting hello machine and hello list should be displayed in hello subsequent exe runs.</span></span> |
| <span data-ttu-id="83312-248">Linux 特定： 無法 tooview hello 所需的磁碟區</span><span class="sxs-lookup"><span data-stu-id="83312-248">Linux specific: Not able tooview hello desired volumes</span></span> | <span data-ttu-id="83312-249">hello OS 的 hello 機器 hello 指令碼執行的位置可能無法辨識 hello 的 hello 備份 VM 的基礎檔案系統</span><span class="sxs-lookup"><span data-stu-id="83312-249">hello OS of hello machine where hello script is run may not recognize hello underlying filesystem of hello backed up VM</span></span> | <span data-ttu-id="83312-250">檢查是否 hello 復原點已損毀一致或檔案一致。</span><span class="sxs-lookup"><span data-stu-id="83312-250">Check whether hello recovery point is crash consistent or file-consistent.</span></span> <span data-ttu-id="83312-251">如果檔案一致，請執行 hello 指令碼，在其作業系統辨識 hello 的另一部電腦上備份 VM 的檔案系統</span><span class="sxs-lookup"><span data-stu-id="83312-251">If file consistent, run hello script on another machine whose OS recognizes hello backed up VM's filesystem</span></span> |
| <span data-ttu-id="83312-252">Windows 特定： 無法 tooview hello 所需的磁碟區</span><span class="sxs-lookup"><span data-stu-id="83312-252">Windows specific: Not able tooview hello desired volumes</span></span> | <span data-ttu-id="83312-253">hello 磁碟可能已附加，但未設定 hello 磁碟區</span><span class="sxs-lookup"><span data-stu-id="83312-253">hello disks may have been attached but hello volumes were not configured</span></span> | <span data-ttu-id="83312-254">從 hello 磁碟管理 畫面中，找出 hello 額外的磁碟相關的 toohello 復原點。</span><span class="sxs-lookup"><span data-stu-id="83312-254">From hello disk management screen, identify hello additional disks related toohello recovery point.</span></span> <span data-ttu-id="83312-255">如果任何這些磁碟處於離線狀態嘗試進行上線 hello 磁碟上按一下滑鼠右鍵，然後按一下 「 線上 」 狀態</span><span class="sxs-lookup"><span data-stu-id="83312-255">If any of these disks are in offline state try making them online by right-clicking on hello disk and click 'Online'</span></span>|
