---
title: "備份 Azure Linux VM | Microsoft Docs"
description: "使用 Azure 備份來備份並保護 Linux VM。"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/27/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 7c00392d5185a2f067f2ee2717529dcbde1e71f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-linux--virtual-machines-in-azure"></a><span data-ttu-id="5a0b5-103">備份 Azure 中的 Linux 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="5a0b5-103">Back up Linux  virtual machines in Azure</span></span>

<span data-ttu-id="5a0b5-104">您可以定期建立備份以保護您的資料。</span><span class="sxs-lookup"><span data-stu-id="5a0b5-104">You can protect your data by taking backups at regular intervals.</span></span> <span data-ttu-id="5a0b5-105">Azure 備份會建立復原點，並儲存在異地備援復原保存庫。</span><span class="sxs-lookup"><span data-stu-id="5a0b5-105">Azure Backup creates recovery points that are stored in geo-redundant recovery vaults.</span></span> <span data-ttu-id="5a0b5-106">當您從復原點還原時，您可以還原 hello 整個 VM 或特定的檔案。</span><span class="sxs-lookup"><span data-stu-id="5a0b5-106">When you restore from a recovery point, you can restore hello whole VM or just specific files.</span></span> <span data-ttu-id="5a0b5-107">本文說明如何 toorestore 單一檔案 tooa Linux VM 執行 nginx。</span><span class="sxs-lookup"><span data-stu-id="5a0b5-107">This article explains how toorestore a single file tooa Linux VM running nginx.</span></span> <span data-ttu-id="5a0b5-108">如果您還沒有 VM toouse，您可以建立一個使用 hello [Linux 快速入門](quick-create-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="5a0b5-108">If you don't already have a VM toouse, you can create one using hello [Linux quickstart](quick-create-cli.md).</span></span> <span data-ttu-id="5a0b5-109">在本教學課程中，您了解如何：</span><span class="sxs-lookup"><span data-stu-id="5a0b5-109">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="5a0b5-110">建立 VM 的備份</span><span class="sxs-lookup"><span data-stu-id="5a0b5-110">Create a backup of a VM</span></span>
> * <span data-ttu-id="5a0b5-111">排定每日備份</span><span class="sxs-lookup"><span data-stu-id="5a0b5-111">Schedule a daily backup</span></span>
> * <span data-ttu-id="5a0b5-112">從備份還原檔案</span><span class="sxs-lookup"><span data-stu-id="5a0b5-112">Restore a file from a backup</span></span>



## <a name="backup-overview"></a><span data-ttu-id="5a0b5-113">備份概觀</span><span class="sxs-lookup"><span data-stu-id="5a0b5-113">Backup overview</span></span>

<span data-ttu-id="5a0b5-114">當 hello Azure 備份服務啟動備份時，它就會觸發 hello 備用分機號碼 tootake 時間點快照集。</span><span class="sxs-lookup"><span data-stu-id="5a0b5-114">When hello Azure Backup service initiates a backup, it triggers hello backup extension tootake a point-in-time snapshot.</span></span> <span data-ttu-id="5a0b5-115">hello Azure 備份服務會使用 hello _VMSnapshotLinux_ Linux 中的擴充功能。</span><span class="sxs-lookup"><span data-stu-id="5a0b5-115">hello Azure Backup service uses hello _VMSnapshotLinux_ extension in Linux.</span></span> <span data-ttu-id="5a0b5-116">hello 延伸模組會安裝在第一個 VM 備份 hello hello VM 正在執行。</span><span class="sxs-lookup"><span data-stu-id="5a0b5-116">hello extension is installed during hello first VM backup if hello VM is running.</span></span> <span data-ttu-id="5a0b5-117">如果 hello 未執行 VM，hello Backup service 的快照 hello 基礎儲存體 （因為 VM 已停止的 hello 時，會不發生任何應用程式寫入）。</span><span class="sxs-lookup"><span data-stu-id="5a0b5-117">If hello VM is not running, hello Backup service takes a snapshot of hello underlying storage (since no application writes occur while hello VM is stopped).</span></span>

<span data-ttu-id="5a0b5-118">根據預設，Azure Backup 所需的檔案系統的一致備份 Linux VM，但它可以設定的 tootake[使用前指令碼和後置指令碼架構的應用程式一致備份](https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent)。</span><span class="sxs-lookup"><span data-stu-id="5a0b5-118">By default, Azure Backup takes a file system consistent backup for Linux VM but it can be configured tootake [application consistent backup using pre-script and post-script framework](https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent).</span></span> <span data-ttu-id="5a0b5-119">一旦 hello Azure 備份服務會擷取 hello 快照，hello 資料就是傳送的 toohello 保存庫。</span><span class="sxs-lookup"><span data-stu-id="5a0b5-119">Once hello Azure Backup service takes hello snapshot, hello data is transferred toohello vault.</span></span> <span data-ttu-id="5a0b5-120">toomaximize 效率 hello 服務識別，以及傳輸只 hello 的 hello 上一次備份之後變更資料的區塊。</span><span class="sxs-lookup"><span data-stu-id="5a0b5-120">toomaximize efficiency, hello service identifies and transfers only hello blocks of data that have changed since hello previous backup.</span></span>

<span data-ttu-id="5a0b5-121">Hello 資料傳輸完成時，會移除 hello 快照集，並建立復原點。</span><span class="sxs-lookup"><span data-stu-id="5a0b5-121">When hello data transfer is complete, hello snapshot is removed and a recovery point is created.</span></span>


## <a name="create-a-backup"></a><span data-ttu-id="5a0b5-122">建立備份</span><span class="sxs-lookup"><span data-stu-id="5a0b5-122">Create a backup</span></span>
<span data-ttu-id="5a0b5-123">建立簡單排定每日備份 tooa 復原服務保存庫。</span><span class="sxs-lookup"><span data-stu-id="5a0b5-123">Create a simple scheduled daily backup tooa Recovery Services Vault.</span></span> 

1. <span data-ttu-id="5a0b5-124">登入 toohello [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="5a0b5-124">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="5a0b5-125">在左側 hello hello 功能表中選取**虛擬機器**。</span><span class="sxs-lookup"><span data-stu-id="5a0b5-125">In hello menu on hello left, select **Virtual machines**.</span></span> 
3. <span data-ttu-id="5a0b5-126">從 hello 清單中，選取 VM tooback。</span><span class="sxs-lookup"><span data-stu-id="5a0b5-126">From hello list, select a VM tooback up.</span></span>
4. <span data-ttu-id="5a0b5-127">在 hello VM 刀鋒視窗中，在 hello**設定**區段中，按一下**備份**。</span><span class="sxs-lookup"><span data-stu-id="5a0b5-127">On hello VM blade, in hello **Settings** section, click **Backup**.</span></span> <span data-ttu-id="5a0b5-128">hello**啟用備份**刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="5a0b5-128">hello **Enable backup** blade opens.</span></span>
5. <span data-ttu-id="5a0b5-129">在**復原服務保存庫**，按一下 **建立新**並提供 hello hello 新的保存庫名稱。</span><span class="sxs-lookup"><span data-stu-id="5a0b5-129">In **Recovery Services vault**, click **Create new** and provide hello name for hello new vault.</span></span> <span data-ttu-id="5a0b5-130">新的保存庫中建立 hello 相同資源群組及做為 hello 虛擬機器的位置。</span><span class="sxs-lookup"><span data-stu-id="5a0b5-130">A new vault is created in hello same Resource Group and location as hello virtual machine.</span></span>
6. <span data-ttu-id="5a0b5-131">按一下 [備份原則]。</span><span class="sxs-lookup"><span data-stu-id="5a0b5-131">Click **Backup policy**.</span></span> <span data-ttu-id="5a0b5-132">此範例中，保留 hello 預設然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="5a0b5-132">For this example, keep hello defaults and click **OK**.</span></span>
7. <span data-ttu-id="5a0b5-133">在 hello**啟用備份**刀鋒視窗中，按一下 **啟用備份**。</span><span class="sxs-lookup"><span data-stu-id="5a0b5-133">On hello **Enable backup** blade, click **Enable Backup**.</span></span> <span data-ttu-id="5a0b5-134">這會建立根據 hello 預設排程每日備份。</span><span class="sxs-lookup"><span data-stu-id="5a0b5-134">This creates a daily backup based on hello default schedule.</span></span>
10. <span data-ttu-id="5a0b5-135">toocreate 初始的復原點，在 hello**備份**刀鋒視窗中按一下**備份現在**。</span><span class="sxs-lookup"><span data-stu-id="5a0b5-135">toocreate an initial recovery point, on hello **Backup** blade click **Backup now**.</span></span>
11. <span data-ttu-id="5a0b5-136">在 hello**立即備份**刀鋒視窗中，按一下 hello 行事曆圖示，請使用 hello 行事曆控制項 tooselect hello 最後一天，此復原點會保留下來，並按一下**備份**。</span><span class="sxs-lookup"><span data-stu-id="5a0b5-136">On hello **Backup Now** blade, click hello calendar icon, use hello calendar control tooselect hello last day this recovery point is retained, and click **Backup**.</span></span>
12. <span data-ttu-id="5a0b5-137">在 hello**備份**刀鋒視窗中的 VM，您會看到 hello 都已完成的復原點數目。</span><span class="sxs-lookup"><span data-stu-id="5a0b5-137">In hello **Backup** blade for your VM, you will see hello number of recovery points that are complete.</span></span>

    ![復原點](./media/tutorial-backup-vms/backup-complete.png)

<span data-ttu-id="5a0b5-139">hello 第一次備份大約需要 20 分鐘。</span><span class="sxs-lookup"><span data-stu-id="5a0b5-139">hello first backup takes about 20 minutes.</span></span> <span data-ttu-id="5a0b5-140">在您的備份完成之後，請繼續 toohello 本教學課程的下一個部分。</span><span class="sxs-lookup"><span data-stu-id="5a0b5-140">Proceed toohello next part of this tutorial after your backup is finished.</span></span>

## <a name="restore-a-file"></a><span data-ttu-id="5a0b5-141">還原檔案</span><span class="sxs-lookup"><span data-stu-id="5a0b5-141">Restore a file</span></span>

<span data-ttu-id="5a0b5-142">如果您不小心刪除或變更 tooa 檔案，您可以使用檔案復原 toorecover hello 檔案從您的備份保存庫。</span><span class="sxs-lookup"><span data-stu-id="5a0b5-142">If you accidentally delete or make changes tooa file, you can use File Recovery toorecover hello file from your backup vault.</span></span> <span data-ttu-id="5a0b5-143">檔案復原使用 hello VM 執行的指令碼為本機磁碟機 toomount hello 復原點。</span><span class="sxs-lookup"><span data-stu-id="5a0b5-143">File Recovery uses a script that runs on hello VM, toomount hello recovery point as local drive.</span></span> <span data-ttu-id="5a0b5-144">這些磁碟機仍會掛接為 12 小時，讓您可以從 hello 復原點複製檔案並將它們還原 toohello VM。</span><span class="sxs-lookup"><span data-stu-id="5a0b5-144">These drives will remain mounted for 12 hours so that you can copy files from hello recovery point and restore them toohello VM.</span></span>  

<span data-ttu-id="5a0b5-145">在此範例中，我們會示範如何 toorecover hello 預設 nginx 網頁 /var/www/html/index.nginx-debian.html。</span><span class="sxs-lookup"><span data-stu-id="5a0b5-145">In this example, we show how toorecover hello default nginx web page /var/www/html/index.nginx-debian.html.</span></span> <span data-ttu-id="5a0b5-146">在此範例中我們 VM 的 hello 公用 IP 位址是*13.69.75.209*。</span><span class="sxs-lookup"><span data-stu-id="5a0b5-146">hello public IP address of our VM in this example is *13.69.75.209*.</span></span> <span data-ttu-id="5a0b5-147">您可以找到 hello vm 使用的 IP 位址：</span><span class="sxs-lookup"><span data-stu-id="5a0b5-147">You can find hello IP address of your vm using:</span></span>

 ```bash 
 az vm show --resource-group myResourceGroup --name myVM -d --query [publicIps] --o tsv
 ```

 
1. <span data-ttu-id="5a0b5-148">在您的本機電腦上開啟瀏覽器並輸入中的 VM toosee hello 預設 nginx 網頁 hello 公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="5a0b5-148">On your local computer, open a browser and type in hello public IP address of your VM toosee hello default nginx web page.</span></span>

    ![預設的 nginx 網頁](./media/tutorial-backup-vms/nginx-working.png)

1. <span data-ttu-id="5a0b5-150">透過 SSH 連線到您的 VM。</span><span class="sxs-lookup"><span data-stu-id="5a0b5-150">SSH into your VM.</span></span>

    ```bash
    ssh 13.69.75.209
    ```
2. <span data-ttu-id="5a0b5-151">刪除 /var/www/html/index.nginx-debian.html。</span><span class="sxs-lookup"><span data-stu-id="5a0b5-151">Delete /var/www/html/index.nginx-debian.html.</span></span>

    ```bash
    sudo rm /var/www/html/index.nginx-debian.html
    ```
    
4. <span data-ttu-id="5a0b5-152">在您的本機電腦上重新整理 hello 瀏覽器所按下 CTRL + F5 toosee 預設 nginx 網頁就會消失。</span><span class="sxs-lookup"><span data-stu-id="5a0b5-152">On your local computer, refresh hello browser by hitting CTRL + F5 toosee that default nginx page is gone.</span></span>

    ![預設的 nginx 網頁](./media/tutorial-backup-vms/nginx-broken.png)
    
1. <span data-ttu-id="5a0b5-154">在您的本機電腦上登入 toohello [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="5a0b5-154">On your local computer, sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
6. <span data-ttu-id="5a0b5-155">在左側 hello hello 功能表中選取**虛擬機器**。</span><span class="sxs-lookup"><span data-stu-id="5a0b5-155">In hello menu on hello left, select **Virtual machines**.</span></span> 
7. <span data-ttu-id="5a0b5-156">從 hello 清單中，選取 hello VM。</span><span class="sxs-lookup"><span data-stu-id="5a0b5-156">From hello list, select hello VM.</span></span>
8. <span data-ttu-id="5a0b5-157">在 hello VM 刀鋒視窗中，在 hello**設定**區段中，按一下**備份**。</span><span class="sxs-lookup"><span data-stu-id="5a0b5-157">On hello VM blade, in hello **Settings** section, click **Backup**.</span></span> <span data-ttu-id="5a0b5-158">hello**備份**刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="5a0b5-158">hello **Backup** blade opens.</span></span> 
9. <span data-ttu-id="5a0b5-159">在 hello 在 hello hello 刀鋒視窗頂端的功能表中選取**檔案復原**。</span><span class="sxs-lookup"><span data-stu-id="5a0b5-159">In hello menu at hello top of hello blade, select **File Recovery**.</span></span> <span data-ttu-id="5a0b5-160">hello**檔案復原**刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="5a0b5-160">hello **File Recovery** blade opens.</span></span>
10. <span data-ttu-id="5a0b5-161">在**步驟 1： 選取的復原點**，從 hello 下拉式清單中選取的復原點。</span><span class="sxs-lookup"><span data-stu-id="5a0b5-161">In **Step 1: Select recovery point**, select a recovery point from hello drop-down.</span></span>
11. <span data-ttu-id="5a0b5-162">在**步驟 2： 下載指令碼 toobrowse 並復原檔案**，按一下 hello**下載可執行檔** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="5a0b5-162">In **Step 2: Download script toobrowse and recover files**, click hello **Download Executable** button.</span></span> <span data-ttu-id="5a0b5-163">儲存 hello 下載的檔案 tooyour 本機電腦。</span><span class="sxs-lookup"><span data-stu-id="5a0b5-163">Save hello downloaded file tooyour local computer.</span></span>
7. <span data-ttu-id="5a0b5-164">按一下**下載指令碼**toodownload hello 指令碼檔案儲存在本機。</span><span class="sxs-lookup"><span data-stu-id="5a0b5-164">Click **Download script** toodownload hello script file locally.</span></span>
8. <span data-ttu-id="5a0b5-165">開啟 Bash 提示字元並輸入 hello 遵循、 取代*Linux_myVM_05-05-2017.sh* hello 包含正確的路徑和檔名，您所下載的 hello 指令碼*azureuser*與 hello hello VM 的使用者名稱和*13.69.75.209* vm hello 公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="5a0b5-165">Open a Bash prompt and type hello following, replacing *Linux_myVM_05-05-2017.sh* with hello correct path and filename for hello script that you downloaded, *azureuser* with hello username for hello VM and *13.69.75.209* with hello public IP address for your VM.</span></span>
    
    ```bash
    scp Linux_myVM_05-05-2017.sh azureuser@13.69.75.209:
    ```
    
9. <span data-ttu-id="5a0b5-166">在您的本機電腦上開啟 SSH 連線 toohello VM。</span><span class="sxs-lookup"><span data-stu-id="5a0b5-166">On your local computer, open an SSH connection toohello VM.</span></span>

    ```bash
    ssh 13.69.75.209
    ```
    
10. <span data-ttu-id="5a0b5-167">您在 VM 上，將執行權限 toohello 指令檔。</span><span class="sxs-lookup"><span data-stu-id="5a0b5-167">On your VM, add execute permissions toohello script file.</span></span>

    ```bash
    chmod +x Linux_myVM_05-05-2017.sh
    ```
    
11. <span data-ttu-id="5a0b5-168">在您的 VM 執行 hello 指令碼 toomount hello 復原點為檔案系統。</span><span class="sxs-lookup"><span data-stu-id="5a0b5-168">On your VM, run hello script toomount hello recovery point as a filesystem.</span></span>

    ```bash
    ./Linux_myVM_05-05-2017.sh
    ```
    
12. <span data-ttu-id="5a0b5-169">hello hello 指令碼可提供從輸出 hello hello 掛接點路徑。</span><span class="sxs-lookup"><span data-stu-id="5a0b5-169">hello output from hello script gives you hello path for hello mount point.</span></span> <span data-ttu-id="5a0b5-170">hello 輸出看起來類似 toothis:</span><span class="sxs-lookup"><span data-stu-id="5a0b5-170">hello output looks similar toothis:</span></span>

    ```bash
    Microsoft Azure VM Backup - File Recovery
    ______________________________________________
                          
    Connecting toorecovery point using ISCSI service...
    
    Connection succeeded!
    
    Please wait while we attach volumes of hello recovery point toothis machine...
                         
    ************ Volumes of hello recovery point and their mount paths on this machine ************

    Sr.No.  |  Disk  |  Volume  |  MountPath 

    1)  | /dev/sdc  |  /dev/sdc1  |  /home/azureuser/myVM-20170505191055/Volume1

    ************ Open File Explorer toobrowse for files. ************

    After recovery, tooremove hello disks and close hello connection toohello recovery point, please click 'Unmount Disks' in step 3 of hello portal.

    Please enter 'q/Q' tooexit...
    ```

12. <span data-ttu-id="5a0b5-171">您在 VM 上，複製 hello nginx 預設 web 網頁 hello 掛接點後 toowhere 從已刪除 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="5a0b5-171">On your VM, copy hello nginx default web page from hello mount point back toowhere you deleted hello file.</span></span>

    ```bash
    sudo cp ~/myVM-20170505191055/Volume1/var/www/html/index.nginx-debian.html /var/www/html/
    ```
    
17. <span data-ttu-id="5a0b5-172">在您的本機電腦上開啟 hello 瀏覽器索引標籤，您連接 toohello hello VM 顯示 hello nginx 預設頁面的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="5a0b5-172">On your local computer, open hello browser tab where you are connected toohello IP address of hello VM showing hello nginx default page.</span></span> <span data-ttu-id="5a0b5-173">按 CTRL + F5 toorefresh hello 瀏覽器頁面。</span><span class="sxs-lookup"><span data-stu-id="5a0b5-173">Press CTRL + F5 toorefresh hello browser page.</span></span> <span data-ttu-id="5a0b5-174">您現在應該會看到該 hello 預設頁面又重新運作。</span><span class="sxs-lookup"><span data-stu-id="5a0b5-174">You should now see that hello default page is working again.</span></span>

    ![預設的 nginx 網頁](./media/tutorial-backup-vms/nginx-working.png)

18. <span data-ttu-id="5a0b5-176">在本機電腦，請返回 toohello 瀏覽器索引標籤的 hello Azure 入口網站，並在**步驟 3： 在復原之後卸載 hello 磁碟**按一下 hello**取消掛接磁碟**按鈕。</span><span class="sxs-lookup"><span data-stu-id="5a0b5-176">On your local computer, go back toohello browser tab for hello Azure portal and in **Step 3: Unmount hello disks after recovery** click hello **Unmount Disks** button.</span></span> <span data-ttu-id="5a0b5-177">如果您忘記 toodo 此步驟中，hello 連接 toohello 掛接點在 12 小時後已自動關閉。</span><span class="sxs-lookup"><span data-stu-id="5a0b5-177">If you forget toodo this step, hello connection toohello mountpoint is automatically close after 12 hours.</span></span> <span data-ttu-id="5a0b5-178">這些 12 小時之後，您需要 toodownload 新的指令碼 toocreate 新的掛接點。</span><span class="sxs-lookup"><span data-stu-id="5a0b5-178">After those 12 hours, you need toodownload a new script toocreate a new mountpoint.</span></span>


## <a name="next-steps"></a><span data-ttu-id="5a0b5-179">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5a0b5-179">Next steps</span></span>

<span data-ttu-id="5a0b5-180">在本教學課程中，您已了解如何：</span><span class="sxs-lookup"><span data-stu-id="5a0b5-180">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="5a0b5-181">建立 VM 的備份</span><span class="sxs-lookup"><span data-stu-id="5a0b5-181">Create a backup of a VM</span></span>
> * <span data-ttu-id="5a0b5-182">排定每日備份</span><span class="sxs-lookup"><span data-stu-id="5a0b5-182">Schedule a daily backup</span></span>
> * <span data-ttu-id="5a0b5-183">從備份還原檔案</span><span class="sxs-lookup"><span data-stu-id="5a0b5-183">Restore a file from a backup</span></span>

<span data-ttu-id="5a0b5-184">前進 toohello 下一個教學課程的 toolearn 有關監視虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="5a0b5-184">Advance toohello next tutorial toolearn about monitoring virtual machines.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="5a0b5-185">監視虛擬機器</span><span class="sxs-lookup"><span data-stu-id="5a0b5-185">Monitor virtual machines</span></span>](tutorial-monitoring.md)

