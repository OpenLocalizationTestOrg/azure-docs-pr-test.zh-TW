---
title: "在 Azure 入口網站中使用 Linux 疑難排解 VM | Microsoft Docs"
description: "了解如何使用 Azure 入口網站將 OS 磁碟連接至復原 VM，以針對 Linux 虛擬機器問題進行疑難排解"
services: virtual-machines-linux
documentationCenter: 
authors: iainfoulds
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 11/14/2016
ms.author: iainfou
ms.openlocfilehash: c96ff625c3e83f6fc9057f1163c877e8e0aed5e3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-a-linux-vm-by-attaching-the-os-disk-to-a-recovery-vm-using-the-azure-portal"></a><span data-ttu-id="b52f7-103">使用 Azure 入口網站將 OS 磁碟連結至復原 VM，以針對 Linux VM 進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="b52f7-103">Troubleshoot a Linux VM by attaching the OS disk to a recovery VM using the Azure portal</span></span>
<span data-ttu-id="b52f7-104">如果 Linux 虛擬機器 (VM) 發生開機或磁碟錯誤，您可能需要對虛擬硬碟本身執行疑難排解步驟。</span><span class="sxs-lookup"><span data-stu-id="b52f7-104">If your Linux virtual machine (VM) encounters a boot or disk error, you may need to perform troubleshooting steps on the virtual hard disk itself.</span></span> <span data-ttu-id="b52f7-105">常見的例子是 `/etc/fstab` 中的項目無效，導致 VM 無法成功開機。</span><span class="sxs-lookup"><span data-stu-id="b52f7-105">A common example would be an invalid entry in `/etc/fstab` that prevents the VM from being able to boot successfully.</span></span> <span data-ttu-id="b52f7-106">本文詳細說明如何使用 Azure 入口網站將虛擬硬碟連接至另一個 Linux VM，以修正任何錯誤，然後重新建立原始 VM。</span><span class="sxs-lookup"><span data-stu-id="b52f7-106">This article details how to use the Azure portal to connect your virtual hard disk to another Linux VM to fix any errors, then re-create your original VM.</span></span>

## <a name="recovery-process-overview"></a><span data-ttu-id="b52f7-107">復原程序概觀</span><span class="sxs-lookup"><span data-stu-id="b52f7-107">Recovery process overview</span></span>
<span data-ttu-id="b52f7-108">疑難排解程序如下所示︰</span><span class="sxs-lookup"><span data-stu-id="b52f7-108">The troubleshooting process is as follows:</span></span>

1. <span data-ttu-id="b52f7-109">刪除遇到問題的 VM，保住虛擬硬碟。</span><span class="sxs-lookup"><span data-stu-id="b52f7-109">Delete the VM encountering issues, keeping the virtual hard disks.</span></span>
2. <span data-ttu-id="b52f7-110">將虛擬硬碟連結和掛接至另一個 Linux VM，以進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="b52f7-110">Attach and mount the virtual hard disk to another Linux VM for troubleshooting purposes.</span></span>
3. <span data-ttu-id="b52f7-111">連接至疑難排解 VM。</span><span class="sxs-lookup"><span data-stu-id="b52f7-111">Connect to the troubleshooting VM.</span></span> <span data-ttu-id="b52f7-112">編輯檔案或執行任何工具來修正原始虛擬硬碟的問題。</span><span class="sxs-lookup"><span data-stu-id="b52f7-112">Edit files or run any tools to fix issues on the original virtual hard disk.</span></span>
4. <span data-ttu-id="b52f7-113">從疑難排解 VM 卸載並中斷連結虛擬硬碟。</span><span class="sxs-lookup"><span data-stu-id="b52f7-113">Unmount and detach the virtual hard disk from the troubleshooting VM.</span></span>
5. <span data-ttu-id="b52f7-114">使用原始虛擬硬碟建立 VM。</span><span class="sxs-lookup"><span data-stu-id="b52f7-114">Create a VM using the original virtual hard disk.</span></span>


## <a name="determine-boot-issues"></a><span data-ttu-id="b52f7-115">判斷開機問題</span><span class="sxs-lookup"><span data-stu-id="b52f7-115">Determine boot issues</span></span>
<span data-ttu-id="b52f7-116">檢查開機診斷和 VM 螢幕擷取畫面來判斷 VM 為何無法正常開機。</span><span class="sxs-lookup"><span data-stu-id="b52f7-116">Examine the boot diagnostics and VM screenshot to determine why your VM is not able to boot correctly.</span></span> <span data-ttu-id="b52f7-117">常見的例子是 `/etc/fstab` 中的項目無效，或因為刪除或移動基礎虛擬硬碟。</span><span class="sxs-lookup"><span data-stu-id="b52f7-117">A common example would be an invalid entry in `/etc/fstab`, or an underlying virtual hard disk being deleted or moved.</span></span>

<span data-ttu-id="b52f7-118">在入口網站中選取您的 VM，然後向下捲動至 [支援 + 疑難排解] 區段。</span><span class="sxs-lookup"><span data-stu-id="b52f7-118">Select your VM in the portal and then scroll down to the **Support + Troubleshooting** section.</span></span> <span data-ttu-id="b52f7-119">按一下 [開機診斷] 以檢視從 VM 串流過來的主控台訊息。</span><span class="sxs-lookup"><span data-stu-id="b52f7-119">Click **Boot diagnostics** to view the console messages streamed from your VM.</span></span> <span data-ttu-id="b52f7-120">檢閱主控台記錄，以查看是否可以判斷 VM 為何會發生問題。</span><span class="sxs-lookup"><span data-stu-id="b52f7-120">Review the console logs to see if you can determine why the VM is encountering an issue.</span></span> <span data-ttu-id="b52f7-121">下列範例說明卡在維護模式，因而需要手動互動的 VM：</span><span class="sxs-lookup"><span data-stu-id="b52f7-121">The following example shows a VM stuck in maintenance mode that requires manual interaction:</span></span>

![檢視 VM 開機診斷主控台記錄](./media/troubleshoot-recovery-disks-portal/boot-diagnostics-error.png)

<span data-ttu-id="b52f7-123">您也可以按一下橫跨在開機診斷記錄頂端的**螢幕擷取畫面**，下載所擷取的 VM 螢幕擷取畫面。</span><span class="sxs-lookup"><span data-stu-id="b52f7-123">You can also click **Screenshot** across the top of the boot diagnostics log to download a capture of the VM screenshot.</span></span>


## <a name="view-existing-virtual-hard-disk-details"></a><span data-ttu-id="b52f7-124">檢視現有的虛擬硬碟詳細資料</span><span class="sxs-lookup"><span data-stu-id="b52f7-124">View existing virtual hard disk details</span></span>
<span data-ttu-id="b52f7-125">您需要先識別虛擬硬碟 (VHD) 的名稱，才能將虛擬硬碟連結至另一個 VM。</span><span class="sxs-lookup"><span data-stu-id="b52f7-125">Before you can attach your virtual hard disk to another VM, you need to identify the name of the virtual hard disk (VHD).</span></span> 

<span data-ttu-id="b52f7-126">從入口網站選取資源群組，然後選取儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="b52f7-126">Select your resource group from the portal, then select your storage account.</span></span> <span data-ttu-id="b52f7-127">按一下 [Blob]，如下列範例所示︰</span><span class="sxs-lookup"><span data-stu-id="b52f7-127">Click **Blobs**, as in the following example:</span></span>

![選取儲存體 Blob](./media/troubleshoot-recovery-disks-portal/storage-account-overview.png)

<span data-ttu-id="b52f7-129">一般來說，您會有一個名為 **vhds** 的容器，以儲存虛擬硬碟。</span><span class="sxs-lookup"><span data-stu-id="b52f7-129">Typically you have a container named **vhds** that stores your virtual hard disks.</span></span> <span data-ttu-id="b52f7-130">選取該容器以檢視虛擬硬碟清單。</span><span class="sxs-lookup"><span data-stu-id="b52f7-130">Select the container to view a list of virtual hard disks.</span></span> <span data-ttu-id="b52f7-131">記下 VHD 的名稱 (其前置詞通常是 VM 的名稱)︰</span><span class="sxs-lookup"><span data-stu-id="b52f7-131">Note the name of your VHD (the prefix is usually the name of your VM):</span></span>

![識別儲存體容器中的 VHD](./media/troubleshoot-recovery-disks-portal/storage-container.png)

<span data-ttu-id="b52f7-133">從清單中選取您現有的虛擬硬碟，並複製 URL 以供下列步驟使用︰</span><span class="sxs-lookup"><span data-stu-id="b52f7-133">Select your existing virtual hard disk from the list and copy the URL for use in the following steps:</span></span>

![複製現有的虛擬硬碟 URL](./media/troubleshoot-recovery-disks-portal/copy-vhd-url.png)


## <a name="delete-existing-vm"></a><span data-ttu-id="b52f7-135">刪除現有的 VM</span><span class="sxs-lookup"><span data-stu-id="b52f7-135">Delete existing VM</span></span>
<span data-ttu-id="b52f7-136">虛擬硬碟和 VM 在 Azure 中是兩個不同的資源。</span><span class="sxs-lookup"><span data-stu-id="b52f7-136">Virtual hard disks and VMs are two distinct resources in Azure.</span></span> <span data-ttu-id="b52f7-137">虛擬硬碟中儲存作業系統本身、應用程式和設定。</span><span class="sxs-lookup"><span data-stu-id="b52f7-137">A virtual hard disk is where the operating system itself, applications, and configurations are stored.</span></span> <span data-ttu-id="b52f7-138">VM 本身只是定義大小或位置的中繼資料，還會參考資源，例如虛擬硬碟或虛擬網路介面卡 (NIC)。</span><span class="sxs-lookup"><span data-stu-id="b52f7-138">The VM itself is just metadata that defines the size or location, and references resources such as a virtual hard disk or virtual network interface card (NIC).</span></span> <span data-ttu-id="b52f7-139">每個虛擬硬碟連結至 VM 時會獲派租用。</span><span class="sxs-lookup"><span data-stu-id="b52f7-139">Each virtual hard disk has a lease assigned when attached to a VM.</span></span> <span data-ttu-id="b52f7-140">雖然即使 VM 正在執行時也可以連結和中斷連結資料磁碟，但除非刪除 VM 資源，否則無法中斷連結 OS 磁碟。</span><span class="sxs-lookup"><span data-stu-id="b52f7-140">Although data disks can be attached and detached even while the VM is running, the OS disk cannot be detached unless the VM resource is deleted.</span></span> <span data-ttu-id="b52f7-141">即使 VM 處於已停止和解除配置的狀態，租用仍會持續讓 OS 磁碟與 VM 產生關聯。</span><span class="sxs-lookup"><span data-stu-id="b52f7-141">The lease continues to associate the OS disk with a VM even when that VM is in a stopped and deallocated state.</span></span>

<span data-ttu-id="b52f7-142">復原 VM 的第一個步驟是刪除 VM 資源本身。</span><span class="sxs-lookup"><span data-stu-id="b52f7-142">The first step to recover your VM is to delete the VM resource itself.</span></span> <span data-ttu-id="b52f7-143">刪除 VM 時，虛擬硬碟會留在儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="b52f7-143">Deleting the VM leaves the virtual hard disks in your storage account.</span></span> <span data-ttu-id="b52f7-144">刪除 VM 之後，您需要將虛擬硬碟連結至另一個 VM，以進行疑難排解並解決錯誤。</span><span class="sxs-lookup"><span data-stu-id="b52f7-144">After the VM is deleted, you attach the virtual hard disk to another VM to troubleshoot and resolve the errors.</span></span>

<span data-ttu-id="b52f7-145">在入口網站中選取 VM，然後按一下 [刪除]：</span><span class="sxs-lookup"><span data-stu-id="b52f7-145">Select your VM in the portal, then click **Delete**:</span></span>

![顯示開機錯誤的 VM 開機診斷螢幕擷取畫面](./media/troubleshoot-recovery-disks-portal/stop-delete-vm.png)

<span data-ttu-id="b52f7-147">請等到 VM 完成刪除之後，再將虛擬硬碟連結至另一個 VM。</span><span class="sxs-lookup"><span data-stu-id="b52f7-147">Wait until the VM has finished deleting before you attach the virtual hard disk to another VM.</span></span> <span data-ttu-id="b52f7-148">在虛擬硬碟上，將它與 VM 產生關聯的租用必須先釋放，您才能將虛擬硬碟連結至另一個 VM。</span><span class="sxs-lookup"><span data-stu-id="b52f7-148">The lease on the virtual hard disk that associates it with the VM needs to be released before you can attach the virtual hard disk to another VM.</span></span>


## <a name="attach-existing-virtual-hard-disk-to-another-vm"></a><span data-ttu-id="b52f7-149">將現有的虛擬硬碟連結至另一個 VM</span><span class="sxs-lookup"><span data-stu-id="b52f7-149">Attach existing virtual hard disk to another VM</span></span>
<span data-ttu-id="b52f7-150">在接下來幾個步驟中，您將使用另一個 VM 進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="b52f7-150">For the next few steps, you use another VM for troubleshooting purposes.</span></span> <span data-ttu-id="b52f7-151">您要將現有的虛擬硬碟連結至這個疑難排解 VM，以便能夠瀏覽並編輯磁碟的內容。</span><span class="sxs-lookup"><span data-stu-id="b52f7-151">You attach the existing virtual hard disk to this troubleshooting VM to be able to browse and edit the disk's content.</span></span> <span data-ttu-id="b52f7-152">舉例來說，此程序可讓您更正任何設定錯誤，或檢閱其他應用程式記錄檔或系統記錄檔。</span><span class="sxs-lookup"><span data-stu-id="b52f7-152">This process allows you to correct any configuration errors or review additional application or system log files, for example.</span></span> <span data-ttu-id="b52f7-153">選擇或建立另一個 VM 以進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="b52f7-153">Choose or create another VM to use for troubleshooting purposes.</span></span>

1. <span data-ttu-id="b52f7-154">從入口網站選取資源群組，然後選取疑難排解 VM。</span><span class="sxs-lookup"><span data-stu-id="b52f7-154">Select your resource group from the portal, then select your troubleshooting VM.</span></span> <span data-ttu-id="b52f7-155">選取 [磁碟]，然後按一下 [連結現有項目]：</span><span class="sxs-lookup"><span data-stu-id="b52f7-155">Select **Disks** and then click **Attach existing**:</span></span>

    ![在入口網站中連結現有磁碟](./media/troubleshoot-recovery-disks-portal/attach-existing-disk.png)

2. <span data-ttu-id="b52f7-157">若要選取您現有的虛擬硬碟，請按一下 [VHD 檔案]：</span><span class="sxs-lookup"><span data-stu-id="b52f7-157">To select your existing virtual hard disk, click **VHD File**:</span></span>

    ![瀏覽現有 VHD](./media/troubleshoot-recovery-disks-portal/select-vhd-location.png)

3. <span data-ttu-id="b52f7-159">選取儲存體帳戶和容器，然後按一下您現有的 VHD。</span><span class="sxs-lookup"><span data-stu-id="b52f7-159">Select your storage account and container, then click your existing VHD.</span></span> <span data-ttu-id="b52f7-160">按一下 [選取] 按鈕，以確認您的選擇︰</span><span class="sxs-lookup"><span data-stu-id="b52f7-160">Click the **Select** button to confirm your choice:</span></span>

    ![選取現有 VHD](./media/troubleshoot-recovery-disks-portal/select-vhd.png)

4. <span data-ttu-id="b52f7-162">在已選取 VHD 之後，按一下 [確定] 以連結現有虛擬硬碟︰</span><span class="sxs-lookup"><span data-stu-id="b52f7-162">With your VHD now selected, click **OK** to attach the existing virtual hard disk:</span></span>

    ![確認連結現有虛擬硬碟](./media/troubleshoot-recovery-disks-portal/attach-disk-confirm.png)

5. <span data-ttu-id="b52f7-164">幾秒鐘後，VM 的 [磁碟] 窗格便會將您現有的已連接虛擬硬碟列示為資料磁碟︰</span><span class="sxs-lookup"><span data-stu-id="b52f7-164">After a few seconds, the **Disks** pane for your VM lists your existing virtual hard disk connected as a data disk:</span></span>

    ![現有虛擬硬碟已連結為資料磁碟](./media/troubleshoot-recovery-disks-portal/attached-disk.png)


## <a name="mount-the-attached-data-disk"></a><span data-ttu-id="b52f7-166">掛接已連結的資料磁碟</span><span class="sxs-lookup"><span data-stu-id="b52f7-166">Mount the attached data disk</span></span>

> [!NOTE]
> <span data-ttu-id="b52f7-167">下列範例詳細說明 Ubuntu VM 上所需的步驟。</span><span class="sxs-lookup"><span data-stu-id="b52f7-167">The following examples detail the steps required on an Ubuntu VM.</span></span> <span data-ttu-id="b52f7-168">如果您使用不同的 Linux 發行版本，例如 Red Hat Enterprise Linux 或 SUSE，則記錄檔位置和 `mount` 命令可能稍微不同。</span><span class="sxs-lookup"><span data-stu-id="b52f7-168">If you are using a different Linux distro, such as Red Hat Enterprise Linux or SUSE, the log file locations and `mount` commands may be a little different.</span></span> <span data-ttu-id="b52f7-169">請參閱您的特定發行版本的文件，以了解命令中相應的變更。</span><span class="sxs-lookup"><span data-stu-id="b52f7-169">Refer to the documentation for your specific distro for the appropriate changes in commands.</span></span>

1. <span data-ttu-id="b52f7-170">使用適當的認證以 SSH 登入疑難排解 VM。</span><span class="sxs-lookup"><span data-stu-id="b52f7-170">SSH to your troubleshooting VM using the appropriate credentials.</span></span> <span data-ttu-id="b52f7-171">如果此磁碟是第一個連結至疑難排解 VM 的資料磁碟，則很可能會連接至 `/dev/sdc`。</span><span class="sxs-lookup"><span data-stu-id="b52f7-171">If this disk is the first data disk attached to your troubleshooting VM, it is likely connected to `/dev/sdc`.</span></span> <span data-ttu-id="b52f7-172">使用 `dmseg` 來列出已連結的磁碟︰</span><span class="sxs-lookup"><span data-stu-id="b52f7-172">Use `dmseg` to list attached disks:</span></span>

    ```bash
    dmesg | grep SCSI
    ```
    <span data-ttu-id="b52f7-173">輸出類似於下列範例：</span><span class="sxs-lookup"><span data-stu-id="b52f7-173">The output is similar to the following example:</span></span>

    ```bash
    [    0.294784] SCSI subsystem initialized
    [    0.573458] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 252)
    [    7.110271] sd 2:0:0:0: [sda] Attached SCSI disk
    [    8.079653] sd 3:0:1:0: [sdb] Attached SCSI disk
    [ 1828.162306] sd 5:0:0:0: [sdc] Attached SCSI disk
    ```

    <span data-ttu-id="b52f7-174">在上述範例中，OS 磁碟位於 `/dev/sda`，而提供給每個 VM 的暫存磁碟位於 `/dev/sdb`。</span><span class="sxs-lookup"><span data-stu-id="b52f7-174">In the preceding example, the OS disk is at `/dev/sda` and the temporary disk provided for each VM is at `/dev/sdb`.</span></span> <span data-ttu-id="b52f7-175">如果您有多個資料磁碟，它們應該是位於 `/dev/sdd`、`/dev/sde`，依此類推。</span><span class="sxs-lookup"><span data-stu-id="b52f7-175">If you had multiple data disks, they should be at `/dev/sdd`, `/dev/sde`, and so on.</span></span>

2. <span data-ttu-id="b52f7-176">建立目錄來掛接現有的虛擬硬碟。</span><span class="sxs-lookup"><span data-stu-id="b52f7-176">Create a directory to mount your existing virtual hard disk.</span></span> <span data-ttu-id="b52f7-177">下列範例會建立名為 `troubleshootingdisk` 的目錄：</span><span class="sxs-lookup"><span data-stu-id="b52f7-177">The following example creates a directory named `troubleshootingdisk`:</span></span>

    ```bash
    sudo mkdir /mnt/troubleshootingdisk
    ```

3. <span data-ttu-id="b52f7-178">如果您在現有的虛擬硬碟上有多個磁碟分割，請掛接所需的磁碟分割。</span><span class="sxs-lookup"><span data-stu-id="b52f7-178">If you have multiple partitions on your existing virtual hard disk, mount the required partition.</span></span> <span data-ttu-id="b52f7-179">下列範例會將第一個主要磁碟分割掛接在 `/dev/sdc1`：</span><span class="sxs-lookup"><span data-stu-id="b52f7-179">The following example mounts the first primary partition at `/dev/sdc1`:</span></span>

    ```bash
    sudo mount /dev/sdc1 /mnt/troubleshootingdisk
    ```

    > [!NOTE]
    > <span data-ttu-id="b52f7-180">最佳做法是使用虛擬硬碟的通用唯一識別碼 (UUID)，將資料磁碟掛接在 Azure 中的 VM。</span><span class="sxs-lookup"><span data-stu-id="b52f7-180">Best practice is to mount data disks on VMs in Azure using the universally unique identifier (UUID) of the virtual hard disk.</span></span> <span data-ttu-id="b52f7-181">在這個簡短的疑難排解案例中，不需要使用 UUID 來掛接虛擬硬碟。</span><span class="sxs-lookup"><span data-stu-id="b52f7-181">For this short troubleshooting scenario, mounting the virtual hard disk using the UUID is not necessary.</span></span> <span data-ttu-id="b52f7-182">但在正常使用情況下，如果編輯 `/etc/fstab` 來使用裝置名稱掛接虛擬硬碟，而不是使用 UUID，可能會造成 VM 無法開機。</span><span class="sxs-lookup"><span data-stu-id="b52f7-182">However, under normal use, editing `/etc/fstab` to mount virtual hard disks using device name rather than UUID may cause the VM to fail to boot.</span></span>


## <a name="fix-issues-on-original-virtual-hard-disk"></a><span data-ttu-id="b52f7-183">修正原始虛擬硬碟的問題</span><span class="sxs-lookup"><span data-stu-id="b52f7-183">Fix issues on original virtual hard disk</span></span>
<span data-ttu-id="b52f7-184">已掛接現有的虛擬硬碟掛，您現在可以視需要執行任何維護和疑難排解步驟。</span><span class="sxs-lookup"><span data-stu-id="b52f7-184">With the existing virtual hard disk mounted, you can now perform any maintenance and troubleshooting steps as needed.</span></span> <span data-ttu-id="b52f7-185">解決問題之後，請繼續進行下列步驟。</span><span class="sxs-lookup"><span data-stu-id="b52f7-185">Once you have addressed the issues, continue with the following steps.</span></span>

## <a name="unmount-and-detach-original-virtual-hard-disk"></a><span data-ttu-id="b52f7-186">卸載並中斷連結原始虛擬硬碟</span><span class="sxs-lookup"><span data-stu-id="b52f7-186">Unmount and detach original virtual hard disk</span></span>
<span data-ttu-id="b52f7-187">錯誤解決之後，請將現有虛擬硬碟與疑難排解 VM 的連結中斷。</span><span class="sxs-lookup"><span data-stu-id="b52f7-187">Once your errors are resolved, detach the existing virtual hard disk from your troubleshooting VM.</span></span> <span data-ttu-id="b52f7-188">直到將虛擬硬碟連結至疑難排解 VM 的租用釋放，您才能將虛擬硬碟用於其他任何 VM。</span><span class="sxs-lookup"><span data-stu-id="b52f7-188">You cannot use your virtual hard disk with any other VM until the lease attaching the virtual hard disk to the troubleshooting VM is released.</span></span>

1. <span data-ttu-id="b52f7-189">從疑難排解 VM 的 SSH 工作階段，卸載現有的虛擬硬碟。</span><span class="sxs-lookup"><span data-stu-id="b52f7-189">From the SSH session to your troubleshooting VM, unmount the existing virtual hard disk.</span></span> <span data-ttu-id="b52f7-190">首先離開掛接點的上層目錄︰</span><span class="sxs-lookup"><span data-stu-id="b52f7-190">Change out of the parent directory for your mount point first:</span></span>

    ```bash
    cd /
    ```

    <span data-ttu-id="b52f7-191">現在卸載現有的虛擬硬碟。</span><span class="sxs-lookup"><span data-stu-id="b52f7-191">Now unmount the existing virtual hard disk.</span></span> <span data-ttu-id="b52f7-192">下列範例會卸載位於 `/dev/sdc1` 的裝置：</span><span class="sxs-lookup"><span data-stu-id="b52f7-192">The following example unmounts the device at `/dev/sdc1`:</span></span>

    ```bash
    sudo umount /dev/sdc1
    ```

2. <span data-ttu-id="b52f7-193">現在從 VM 中斷連結虛擬硬碟。</span><span class="sxs-lookup"><span data-stu-id="b52f7-193">Now detach the virtual hard disk from the VM.</span></span> <span data-ttu-id="b52f7-194">在入口網站中選取 VM，然後按一下 [磁碟]。</span><span class="sxs-lookup"><span data-stu-id="b52f7-194">Select your VM in the portal and click **Disks**.</span></span> <span data-ttu-id="b52f7-195">選取您現有的虛擬硬碟，然後按一下 [中斷連結]：</span><span class="sxs-lookup"><span data-stu-id="b52f7-195">Select your existing virtual hard disk and then click **Detach**:</span></span>

    ![將現有虛擬硬碟中斷連結](./media/troubleshoot-recovery-disks-portal/detach-disk.png)

    <span data-ttu-id="b52f7-197">請稍候，等待 VM 成功將資料磁碟中斷連結再繼續。</span><span class="sxs-lookup"><span data-stu-id="b52f7-197">Wait until the VM has successfully detached the data disk before continuing.</span></span>

## <a name="create-vm-from-original-hard-disk"></a><span data-ttu-id="b52f7-198">從原始硬碟建立 VM</span><span class="sxs-lookup"><span data-stu-id="b52f7-198">Create VM from original hard disk</span></span>
<span data-ttu-id="b52f7-199">若要從原始虛擬硬碟建立 VM，請使用[這個 Azure Resource Manager 範本](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet)。</span><span class="sxs-lookup"><span data-stu-id="b52f7-199">To create a VM from your original virtual hard disk, use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet).</span></span> <span data-ttu-id="b52f7-200">此範本會使用來自先前命令的 VHD URL，將 VM 部署至現有的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="b52f7-200">The template deploys a VM into an existing virtual network, using the VHD URL from the earlier command.</span></span> <span data-ttu-id="b52f7-201">按一下 [部署至 Azure] 按鈕，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="b52f7-201">Click the **Deploy to Azure** button as follows:</span></span>

![從來自 GitHub 的範本部署 VM](./media/troubleshoot-recovery-disks-portal/deploy-template-from-github.png)

<span data-ttu-id="b52f7-203">範本會載入到 Azure 入口網站以供部署。</span><span class="sxs-lookup"><span data-stu-id="b52f7-203">The template is loaded into the Azure portal for deployment.</span></span> <span data-ttu-id="b52f7-204">輸入新 VM 和現有 Azure 資源的名稱，並貼上您現有虛擬硬碟的 URL。</span><span class="sxs-lookup"><span data-stu-id="b52f7-204">Enter the names for your new VM and existing Azure resources, and paste the URL to your existing virtual hard disk.</span></span> <span data-ttu-id="b52f7-205">若要開始部署，請按一下 [購買]：</span><span class="sxs-lookup"><span data-stu-id="b52f7-205">To begin the deployment, click **Purchase**:</span></span>

![從範本部署 VM](./media/troubleshoot-recovery-disks-portal/deploy-from-image.png)


## <a name="re-enable-boot-diagnostics"></a><span data-ttu-id="b52f7-207">重新啟用開機診斷</span><span class="sxs-lookup"><span data-stu-id="b52f7-207">Re-enable boot diagnostics</span></span>
<span data-ttu-id="b52f7-208">當您從現有的虛擬硬碟建立 VM 時，可能不會自動啟用開機診斷。</span><span class="sxs-lookup"><span data-stu-id="b52f7-208">When you create your VM from the existing virtual hard disk, boot diagnostics may not automatically be enabled.</span></span> <span data-ttu-id="b52f7-209">若要檢查開機診斷狀態並在需要時開啟，請在入口網站中選取 VM。</span><span class="sxs-lookup"><span data-stu-id="b52f7-209">To check the status of boot diagnostics and turn on if needed, select your VM in the portal.</span></span> <span data-ttu-id="b52f7-210">在 [監視] 底下，按一下 [診斷設定]。</span><span class="sxs-lookup"><span data-stu-id="b52f7-210">Under **Monitoring**, click **Diagnostics settings**.</span></span> <span data-ttu-id="b52f7-211">請確定狀態是 [開啟]，而且已選取 [開機診斷] 旁邊的核取記號。</span><span class="sxs-lookup"><span data-stu-id="b52f7-211">Ensure the status is **On**, and the check mark next to **Boot diagnostics** is selected.</span></span> <span data-ttu-id="b52f7-212">如果有進行任何變更，請按一下 [儲存]：</span><span class="sxs-lookup"><span data-stu-id="b52f7-212">If you make any changes, click **Save**:</span></span>

![更新開機診斷設定](./media/troubleshoot-recovery-disks-portal/reenable-boot-diagnostics.png)

## <a name="next-steps"></a><span data-ttu-id="b52f7-214">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b52f7-214">Next steps</span></span>
<span data-ttu-id="b52f7-215">如果連接至 VM 時發生問題，請參閱[針對 Azure VM 的 SSH 連接進行疑難排解](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="b52f7-215">If you are having issues connecting to your VM, see [Troubleshoot SSH connections to an Azure VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="b52f7-216">如果存取 VM 上執行的應用程式時發生問題，請參閱[針對 Linux VM 上的應用程式連線問題進行疑難排解](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="b52f7-216">For issues with accessing applications running on your VM, see [Troubleshoot application connectivity issues on a Linux VM](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="b52f7-217">如需使用 Resource Manager 的詳細資訊，請參閱 [Azure Resource Manager 概觀](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="b52f7-217">For more information about using Resource Manager, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>