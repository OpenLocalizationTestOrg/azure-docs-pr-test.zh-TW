---
title: "透過 Azure CLI 1.0 使用 Linux 疑難排解 VM | Microsoft Docs"
description: "了解如何使用 Azure CLI 1.0 將 OS 磁碟連接至復原 VM，以針對 Linux VM 問題進行疑難排解"
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
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: d817358211f123c96d899c5cff88cc47aeb5c9c1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-a-linux-vm-by-attaching-the-os-disk-to-a-recovery-vm-using-the-azure-cli-10"></a><span data-ttu-id="51bd9-103">使用 Azure CLI 1.0 將 OS 磁碟連結至復原 VM，以針對 Linux VM 進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="51bd9-103">Troubleshoot a Linux VM by attaching the OS disk to a recovery VM using the Azure CLI 1.0</span></span>
<span data-ttu-id="51bd9-104">如果 Linux 虛擬機器 (VM) 發生開機或磁碟錯誤，您可能需要對虛擬硬碟本身執行疑難排解步驟。</span><span class="sxs-lookup"><span data-stu-id="51bd9-104">If your Linux virtual machine (VM) encounters a boot or disk error, you may need to perform troubleshooting steps on the virtual hard disk itself.</span></span> <span data-ttu-id="51bd9-105">常見的例子是 `/etc/fstab` 中的項目無效，導致 VM 無法成功開機。</span><span class="sxs-lookup"><span data-stu-id="51bd9-105">A common example would be an invalid entry in `/etc/fstab` that prevents the VM from being able to boot successfully.</span></span> <span data-ttu-id="51bd9-106">本文詳細說明如何使用 Azure CLI 1.0 將虛擬硬碟連接至另一個 Linux VM，以修正任何錯誤，然後重新建立原始 VM。</span><span class="sxs-lookup"><span data-stu-id="51bd9-106">This article details how to use the Azure CLI 1.0 to connect your virtual hard disk to another Linux VM to fix any errors, then re-create your original VM.</span></span>


## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="51bd9-107">用以完成工作的 CLI 版本</span><span class="sxs-lookup"><span data-stu-id="51bd9-107">CLI versions to complete the task</span></span>
<span data-ttu-id="51bd9-108">您可以使用下列其中一個 CLI 版本來完成工作︰</span><span class="sxs-lookup"><span data-stu-id="51bd9-108">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="51bd9-109">[Azure CLI 1.0](#recovery-process-overview) – 適用於傳統和資源管理部署模型的 CLI (本文章)</span><span class="sxs-lookup"><span data-stu-id="51bd9-109">[Azure CLI 1.0](#recovery-process-overview) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="51bd9-110">[Azure CLI 2.0](../windows/troubleshoot-recovery-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - 適用於資源管理部署模型的新一代 CLI</span><span class="sxs-lookup"><span data-stu-id="51bd9-110">[Azure CLI 2.0](../windows/troubleshoot-recovery-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>


## <a name="recovery-process-overview"></a><span data-ttu-id="51bd9-111">復原程序概觀</span><span class="sxs-lookup"><span data-stu-id="51bd9-111">Recovery process overview</span></span>
<span data-ttu-id="51bd9-112">疑難排解程序如下所示︰</span><span class="sxs-lookup"><span data-stu-id="51bd9-112">The troubleshooting process is as follows:</span></span>

1. <span data-ttu-id="51bd9-113">刪除遇到問題的 VM，保住虛擬硬碟。</span><span class="sxs-lookup"><span data-stu-id="51bd9-113">Delete the VM encountering issues, keeping the virtual hard disks.</span></span>
2. <span data-ttu-id="51bd9-114">將虛擬硬碟連結和掛接至另一個 Linux VM，以進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="51bd9-114">Attach and mount the virtual hard disk to another Linux VM for troubleshooting purposes.</span></span>
3. <span data-ttu-id="51bd9-115">連接至疑難排解 VM。</span><span class="sxs-lookup"><span data-stu-id="51bd9-115">Connect to the troubleshooting VM.</span></span> <span data-ttu-id="51bd9-116">編輯檔案或執行任何工具來修正原始虛擬硬碟的問題。</span><span class="sxs-lookup"><span data-stu-id="51bd9-116">Edit files or run any tools to fix issues on the original virtual hard disk.</span></span>
4. <span data-ttu-id="51bd9-117">從疑難排解 VM 卸載並中斷連結虛擬硬碟。</span><span class="sxs-lookup"><span data-stu-id="51bd9-117">Unmount and detach the virtual hard disk from the troubleshooting VM.</span></span>
5. <span data-ttu-id="51bd9-118">使用原始虛擬硬碟建立 VM。</span><span class="sxs-lookup"><span data-stu-id="51bd9-118">Create a VM using the original virtual hard disk.</span></span>

<span data-ttu-id="51bd9-119">確定您已安裝[最新的 Azure CLI 1.0](../../cli-install-nodejs.md)，並已登入且使用 Resource Manager 模式：</span><span class="sxs-lookup"><span data-stu-id="51bd9-119">Make sure that you have [the latest Azure CLI 1.0](../../cli-install-nodejs.md) installed and logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="51bd9-120">在下列範例中，請以您自己的值取代參數名稱。</span><span class="sxs-lookup"><span data-stu-id="51bd9-120">In the following examples, replace parameter names with your own values.</span></span> <span data-ttu-id="51bd9-121">範例參數名稱包含 `myResourceGroup`、`mystorageaccount` 和 `myVM`。</span><span class="sxs-lookup"><span data-stu-id="51bd9-121">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>


## <a name="determine-boot-issues"></a><span data-ttu-id="51bd9-122">判斷開機問題</span><span class="sxs-lookup"><span data-stu-id="51bd9-122">Determine boot issues</span></span>
<span data-ttu-id="51bd9-123">檢查序列輸出來判斷 VM 為何無法正常開機。</span><span class="sxs-lookup"><span data-stu-id="51bd9-123">Examine the serial output to determine why your VM is not able to boot correctly.</span></span> <span data-ttu-id="51bd9-124">常見的例子是 `/etc/fstab` 中的項目無效，或因為刪除或移動基礎虛擬硬碟。</span><span class="sxs-lookup"><span data-stu-id="51bd9-124">A common example is an invalid entry in `/etc/fstab`, or the underlying virtual hard disk being deleted or moved.</span></span>

<span data-ttu-id="51bd9-125">下列範例會從資源群組 `myResourceGroup` 中的 VM `myVM` 取得序列輸出：</span><span class="sxs-lookup"><span data-stu-id="51bd9-125">The following example gets the serial output from the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>

```azurecli
azure vm get-serial-output --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="51bd9-126">檢閱序列輸出來判斷 VM 為何無法開機。</span><span class="sxs-lookup"><span data-stu-id="51bd9-126">Review the serial output to determine why the VM is failing to boot.</span></span> <span data-ttu-id="51bd9-127">如果序列輸出未提供任何指示，您可能需要將虛擬硬碟連接至疑難排解 VM，然後檢閱 `/var/log` 中的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="51bd9-127">If the serial output isn't providing any indication, you may need to review log files in `/var/log` once you have the virtual hard disk connected to a troubleshooting VM.</span></span>


## <a name="view-existing-virtual-hard-disk-details"></a><span data-ttu-id="51bd9-128">檢視現有的虛擬硬碟詳細資料</span><span class="sxs-lookup"><span data-stu-id="51bd9-128">View existing virtual hard disk details</span></span>
<span data-ttu-id="51bd9-129">您需要先識別虛擬硬碟 (VHD) 的名稱，才能將虛擬硬碟連結至另一個 VM。</span><span class="sxs-lookup"><span data-stu-id="51bd9-129">Before you can attach your virtual hard disk to another VM, you need to identify the name of the virtual hard disk (VHD).</span></span> 

<span data-ttu-id="51bd9-130">下列範例會針對資源群組 `myResourceGroup` 中的 VM `myVM` 取得相關資訊：</span><span class="sxs-lookup"><span data-stu-id="51bd9-130">The following example gets information for the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>

```azurecli
azure vm show --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="51bd9-131">在先前命令的輸出中尋找 `Vhd URI`。</span><span class="sxs-lookup"><span data-stu-id="51bd9-131">Look for `Vhd URI` in the output from the preceding command.</span></span> <span data-ttu-id="51bd9-132">下列截短範例輸出的最後一行顯示 `Vhd URI`︰</span><span class="sxs-lookup"><span data-stu-id="51bd9-132">The following truncated example output shows the `Vhd URI` on the last line:</span></span>

```azurecli
info:    Executing command vm show
+ Looking up the VM "myVM"
+ Looking up the NIC "myNic"
+ Looking up the public ip "myPublicIP"
...
data:
data:      OS Disk:
data:        OSType                      :Linux
data:        Name                        :myVM
data:        Caching                     :ReadWrite
data:        CreateOption                :FromImage
data:        Vhd:
data:          Uri                       :https://mystorageaccount.blob.core.windows.net/vhds/myVM201610292712.vhd
```


## <a name="delete-existing-vm"></a><span data-ttu-id="51bd9-133">刪除現有的 VM</span><span class="sxs-lookup"><span data-stu-id="51bd9-133">Delete existing VM</span></span>
<span data-ttu-id="51bd9-134">虛擬硬碟和 VM 在 Azure 中是兩個不同的資源。</span><span class="sxs-lookup"><span data-stu-id="51bd9-134">Virtual hard disks and VMs are two distinct resources in Azure.</span></span> <span data-ttu-id="51bd9-135">虛擬硬碟中儲存作業系統本身、應用程式和設定。</span><span class="sxs-lookup"><span data-stu-id="51bd9-135">A virtual hard disk is where the operating system itself, applications, and configurations are stored.</span></span> <span data-ttu-id="51bd9-136">VM 本身只是定義大小或位置的中繼資料，還會參考資源，例如虛擬硬碟或虛擬網路介面卡 (NIC)。</span><span class="sxs-lookup"><span data-stu-id="51bd9-136">The VM itself is just metadata that defines the size or location, and references resources such as a virtual hard disk or virtual network interface card (NIC).</span></span> <span data-ttu-id="51bd9-137">每個虛擬硬碟連結至 VM 時會獲派租用。</span><span class="sxs-lookup"><span data-stu-id="51bd9-137">Each virtual hard disk has a lease assigned when attached to a VM.</span></span> <span data-ttu-id="51bd9-138">雖然即使 VM 正在執行時也可以連結和中斷連結資料磁碟，但除非刪除 VM 資源，否則無法中斷連結 OS 磁碟。</span><span class="sxs-lookup"><span data-stu-id="51bd9-138">Although data disks can be attached and detached even while the VM is running, the OS disk cannot be detached unless the VM resource is deleted.</span></span> <span data-ttu-id="51bd9-139">即使 VM 處於已停止和解除配置的狀態，租用仍會持續讓 OS 磁碟與 VM 產生關聯。</span><span class="sxs-lookup"><span data-stu-id="51bd9-139">The lease continues to associate the OS disk with a VM even when that VM is in a stopped and deallocated state.</span></span>

<span data-ttu-id="51bd9-140">復原 VM 的第一個步驟是刪除 VM 資源本身。</span><span class="sxs-lookup"><span data-stu-id="51bd9-140">The first step to recover your VM is to delete the VM resource itself.</span></span> <span data-ttu-id="51bd9-141">刪除 VM 時，虛擬硬碟會留在儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="51bd9-141">Deleting the VM leaves the virtual hard disks in your storage account.</span></span> <span data-ttu-id="51bd9-142">刪除 VM 之後，您需要將虛擬硬碟連結至另一個 VM，以進行疑難排解並解決錯誤。</span><span class="sxs-lookup"><span data-stu-id="51bd9-142">After the VM is deleted, you attach the virtual hard disk to another VM to troubleshoot and resolve the errors.</span></span>

<span data-ttu-id="51bd9-143">下列範例會從資源群組 `myResourceGroup` 中刪除 VM `myVM`：</span><span class="sxs-lookup"><span data-stu-id="51bd9-143">The following example deletes the VM named `myVM` from the resource group named `myResourceGroup`:</span></span>

```azurecli
azure vm delete --resource-group myResourceGroup --name myVM 
```

<span data-ttu-id="51bd9-144">請等到 VM 完成刪除之後，再將虛擬硬碟連結至另一個 VM。</span><span class="sxs-lookup"><span data-stu-id="51bd9-144">Wait until the VM has finished deleting before you attach the virtual hard disk to another VM.</span></span> <span data-ttu-id="51bd9-145">在虛擬硬碟上，將它與 VM 產生關聯的租用必須先釋放，您才能將虛擬硬碟連結至另一個 VM。</span><span class="sxs-lookup"><span data-stu-id="51bd9-145">The lease on the virtual hard disk that associates it with the VM needs to be released before you can attach the virtual hard disk to another VM.</span></span>


## <a name="attach-existing-virtual-hard-disk-to-another-vm"></a><span data-ttu-id="51bd9-146">將現有的虛擬硬碟連結至另一個 VM</span><span class="sxs-lookup"><span data-stu-id="51bd9-146">Attach existing virtual hard disk to another VM</span></span>
<span data-ttu-id="51bd9-147">在接下來幾個步驟中，您將使用另一個 VM 進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="51bd9-147">For the next few steps, you use another VM for troubleshooting purposes.</span></span> <span data-ttu-id="51bd9-148">您將現有的虛擬硬碟連結至這個疑難排解 VM，以瀏覽並編輯磁碟的內容。</span><span class="sxs-lookup"><span data-stu-id="51bd9-148">You attach the existing virtual hard disk to this troubleshooting VM to browse and edit the disk's content.</span></span> <span data-ttu-id="51bd9-149">舉例來說，此程序可讓您更正任何設定錯誤，或檢閱其他應用程式記錄檔或系統記錄檔。</span><span class="sxs-lookup"><span data-stu-id="51bd9-149">This process allows you to correct any configuration errors or review additional application or system log files, for example.</span></span> <span data-ttu-id="51bd9-150">選擇或建立另一個 VM 以進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="51bd9-150">Choose or create another VM to use for troubleshooting purposes.</span></span>

<span data-ttu-id="51bd9-151">當您連結現有的虛擬硬碟時，請指定在先前的 `azure vm show` 命令中取得的磁碟 URL。</span><span class="sxs-lookup"><span data-stu-id="51bd9-151">When you attach the existing virtual hard disk, specify the URL to the disk obtained in the preceding `azure vm show` command.</span></span> <span data-ttu-id="51bd9-152">下列範例會將現有的虛擬硬碟連結至資源群組 `myResourceGroup` 中的疑難排解 VM `myVMRecovery`：</span><span class="sxs-lookup"><span data-stu-id="51bd9-152">The following example attaches an existing virtual hard disk to the troubleshooting VM named `myVMRecovery` in the resource group named `myResourceGroup`:</span></span>

```azurecli
azure vm disk attach --resource-group myResourceGroup --name myVMRecovery \
    --vhd-url https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
```


## <a name="mount-the-attached-data-disk"></a><span data-ttu-id="51bd9-153">掛接已連結的資料磁碟</span><span class="sxs-lookup"><span data-stu-id="51bd9-153">Mount the attached data disk</span></span>

> [!NOTE]
> <span data-ttu-id="51bd9-154">下列範例詳細說明 Ubuntu VM 上所需的步驟。</span><span class="sxs-lookup"><span data-stu-id="51bd9-154">The following examples detail the steps required on an Ubuntu VM.</span></span> <span data-ttu-id="51bd9-155">如果您使用不同的 Linux 發行版本，例如 Red Hat Enterprise Linux 或 SUSE，則記錄檔位置和 `mount` 命令可能稍微不同。</span><span class="sxs-lookup"><span data-stu-id="51bd9-155">If you are using a different Linux distro, such as Red Hat Enterprise Linux or SUSE, the log file locations and `mount` commands may be a little different.</span></span> <span data-ttu-id="51bd9-156">請參閱您的特定發行版本的文件，以了解命令中相應的變更。</span><span class="sxs-lookup"><span data-stu-id="51bd9-156">Refer to the documentation for your specific distro for the appropriate changes in commands.</span></span>

1. <span data-ttu-id="51bd9-157">使用適當的認證以 SSH 登入疑難排解 VM。</span><span class="sxs-lookup"><span data-stu-id="51bd9-157">SSH to your troubleshooting VM using the appropriate credentials.</span></span> <span data-ttu-id="51bd9-158">如果此磁碟是第一個連結至疑難排解 VM 的資料磁碟，則磁碟很可能連結至 `/dev/sdc`。</span><span class="sxs-lookup"><span data-stu-id="51bd9-158">If this disk is the first data disk attached to your troubleshooting VM, the disk is likely connected to `/dev/sdc`.</span></span> <span data-ttu-id="51bd9-159">使用 `dmseg` 來檢視已連結的磁碟︰</span><span class="sxs-lookup"><span data-stu-id="51bd9-159">Use `dmseg` to view attached disks:</span></span>

    ```bash
    dmesg | grep SCSI
    ```

    <span data-ttu-id="51bd9-160">輸出類似於下列範例：</span><span class="sxs-lookup"><span data-stu-id="51bd9-160">The output is similar to the following example:</span></span>

    ```bash
    [    0.294784] SCSI subsystem initialized
    [    0.573458] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 252)
    [    7.110271] sd 2:0:0:0: [sda] Attached SCSI disk
    [    8.079653] sd 3:0:1:0: [sdb] Attached SCSI disk
    [ 1828.162306] sd 5:0:0:0: [sdc] Attached SCSI disk
    ```

    <span data-ttu-id="51bd9-161">在上述範例中，OS 磁碟位於 `/dev/sda`，而提供給每個 VM 的暫存磁碟位於 `/dev/sdb`。</span><span class="sxs-lookup"><span data-stu-id="51bd9-161">In the preceding example, the OS disk is at `/dev/sda` and the temporary disk provided for each VM is at `/dev/sdb`.</span></span> <span data-ttu-id="51bd9-162">如果您有多個資料磁碟，它們應該是位於 `/dev/sdd`、`/dev/sde`，依此類推。</span><span class="sxs-lookup"><span data-stu-id="51bd9-162">If you had multiple data disks, they should be at `/dev/sdd`, `/dev/sde`, and so on.</span></span>

2. <span data-ttu-id="51bd9-163">建立目錄來掛接現有的虛擬硬碟。</span><span class="sxs-lookup"><span data-stu-id="51bd9-163">Create a directory to mount your existing virtual hard disk.</span></span> <span data-ttu-id="51bd9-164">下列範例會建立名為 `troubleshootingdisk` 的目錄：</span><span class="sxs-lookup"><span data-stu-id="51bd9-164">The following example creates a directory named `troubleshootingdisk`:</span></span>

    ```bash
    sudo mkdir /mnt/troubleshootingdisk
    ```

3. <span data-ttu-id="51bd9-165">如果您在現有的虛擬硬碟上有多個磁碟分割，請掛接所需的磁碟分割。</span><span class="sxs-lookup"><span data-stu-id="51bd9-165">If you have multiple partitions on your existing virtual hard disk, mount the required partition.</span></span> <span data-ttu-id="51bd9-166">下列範例會將第一個主要磁碟分割掛接在 `/dev/sdc1`：</span><span class="sxs-lookup"><span data-stu-id="51bd9-166">The following example mounts the first primary partition at `/dev/sdc1`:</span></span>

    ```bash
    sudo mount /dev/sdc1 /mnt/troubleshootingdisk
    ```

    > [!NOTE]
    > <span data-ttu-id="51bd9-167">最佳做法是使用虛擬硬碟的通用唯一識別碼 (UUID)，將資料磁碟掛接在 Azure 中的 VM。</span><span class="sxs-lookup"><span data-stu-id="51bd9-167">Best practice is to mount data disks on VMs in Azure using the universally unique identifier (UUID) of the virtual hard disk.</span></span> <span data-ttu-id="51bd9-168">在這個簡短的疑難排解案例中，不需要使用 UUID 來掛接虛擬硬碟。</span><span class="sxs-lookup"><span data-stu-id="51bd9-168">For this short troubleshooting scenario, mounting the virtual hard disk using the UUID is not necessary.</span></span> <span data-ttu-id="51bd9-169">但在正常使用情況下，如果編輯 `/etc/fstab` 來使用裝置名稱掛接虛擬硬碟，而不是使用 UUID，可能會造成 VM 無法開機。</span><span class="sxs-lookup"><span data-stu-id="51bd9-169">However, under normal use, editing `/etc/fstab` to mount virtual hard disks using device name rather than UUID may cause the VM to fail to boot.</span></span>


## <a name="fix-issues-on-original-virtual-hard-disk"></a><span data-ttu-id="51bd9-170">修正原始虛擬硬碟的問題</span><span class="sxs-lookup"><span data-stu-id="51bd9-170">Fix issues on original virtual hard disk</span></span>
<span data-ttu-id="51bd9-171">已掛接現有的虛擬硬碟掛，您現在可以視需要執行任何維護和疑難排解步驟。</span><span class="sxs-lookup"><span data-stu-id="51bd9-171">With the existing virtual hard disk mounted, you can now perform any maintenance and troubleshooting steps as needed.</span></span> <span data-ttu-id="51bd9-172">解決問題之後，請繼續進行下列步驟。</span><span class="sxs-lookup"><span data-stu-id="51bd9-172">Once you have addressed the issues, continue with the following steps.</span></span>


## <a name="unmount-and-detach-original-virtual-hard-disk"></a><span data-ttu-id="51bd9-173">卸載並中斷連結原始虛擬硬碟</span><span class="sxs-lookup"><span data-stu-id="51bd9-173">Unmount and detach original virtual hard disk</span></span>
<span data-ttu-id="51bd9-174">一旦解決錯誤，您就要從疑難排解 VM 卸載中斷連結並現有的虛擬硬碟。</span><span class="sxs-lookup"><span data-stu-id="51bd9-174">Once your errors are resolved, you unmount and detach the existing virtual hard disk from your troubleshooting VM.</span></span> <span data-ttu-id="51bd9-175">直到將虛擬硬碟連結至疑難排解 VM 的租用釋放，您才能將虛擬硬碟用於其他任何 VM。</span><span class="sxs-lookup"><span data-stu-id="51bd9-175">You cannot use your virtual hard disk with any other VM until the lease attaching the virtual hard disk to the troubleshooting VM is released.</span></span>

1. <span data-ttu-id="51bd9-176">從疑難排解 VM 的 SSH 工作階段，卸載現有的虛擬硬碟。</span><span class="sxs-lookup"><span data-stu-id="51bd9-176">From the SSH session to your troubleshooting VM, unmount the existing virtual hard disk.</span></span> <span data-ttu-id="51bd9-177">首先離開掛接點的上層目錄︰</span><span class="sxs-lookup"><span data-stu-id="51bd9-177">Change out of the parent directory for your mount point first:</span></span>

    ```bash
    cd /
    ```

    <span data-ttu-id="51bd9-178">現在卸載現有的虛擬硬碟。</span><span class="sxs-lookup"><span data-stu-id="51bd9-178">Now unmount the existing virtual hard disk.</span></span> <span data-ttu-id="51bd9-179">下列範例會卸載位於 `/dev/sdc1` 的裝置：</span><span class="sxs-lookup"><span data-stu-id="51bd9-179">The following example unmounts the device at `/dev/sdc1`:</span></span>

    ```bash
    sudo umount /dev/sdc1
    ```

2. <span data-ttu-id="51bd9-180">現在從 VM 中斷連結虛擬硬碟。</span><span class="sxs-lookup"><span data-stu-id="51bd9-180">Now detach the virtual hard disk from the VM.</span></span> <span data-ttu-id="51bd9-181">結束疑難排解 VM 的 SSH 工作階段。</span><span class="sxs-lookup"><span data-stu-id="51bd9-181">Exit the SSH session to your troubleshooting VM.</span></span> <span data-ttu-id="51bd9-182">在 Azure CLI 中，先列出連結至疑難排解 VM 的資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="51bd9-182">In the Azure CLI, first list the attached data disks to your troubleshooting VM.</span></span> <span data-ttu-id="51bd9-183">下列範例會列出連結至資源群組 `myResourceGroup` 中 VM `myVMRecovery` 的資料磁碟：</span><span class="sxs-lookup"><span data-stu-id="51bd9-183">The following example lists the data disks attached to the VM named `myVMRecovery` in the resource group named `myResourceGroup`:</span></span>

    ```azurecli
    azure vm disk list --resource-group myResourceGroup --vm-name myVMRecovery
    ```

    <span data-ttu-id="51bd9-184">請注意現有虛擬硬碟的 `Lun` 值。</span><span class="sxs-lookup"><span data-stu-id="51bd9-184">Note the `Lun` value for your existing virtual hard disk.</span></span> <span data-ttu-id="51bd9-185">下列範例命令輸出顯示連結在 LUN 0 的現有虛擬磁碟︰</span><span class="sxs-lookup"><span data-stu-id="51bd9-185">The following example command output shows the existing virtual disk attached at LUN 0:</span></span>

    ```azurecli
    info:    Executing command vm disk list
    + Looking up the VM "myVMRecovery"
    data:    Name              Lun  DiskSizeGB  Caching  URI
    data:    ------            ---  ----------  -------  ------------------------------------------------------------------------
    data:    myVM              0                None     https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
    info:    vm disk list command OK
    ```

    <span data-ttu-id="51bd9-186">使用適用的 `Lun` 值從 VM 卸載資料磁碟︰</span><span class="sxs-lookup"><span data-stu-id="51bd9-186">Detach the data disk from your VM using the applicable `Lun` value:</span></span>

    ```azurecli
    azure vm disk detach --resource-group myResourceGroup --vm-name myVMRecovery \
        --lun 0
    ```


## <a name="create-vm-from-original-hard-disk"></a><span data-ttu-id="51bd9-187">從原始硬碟建立 VM</span><span class="sxs-lookup"><span data-stu-id="51bd9-187">Create VM from original hard disk</span></span>
<span data-ttu-id="51bd9-188">若要從原始虛擬硬碟建立 VM，請使用[這個 Azure Resource Manager 範本](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd)。</span><span class="sxs-lookup"><span data-stu-id="51bd9-188">To create a VM from your original virtual hard disk, use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd).</span></span> <span data-ttu-id="51bd9-189">實際的 JSON 範本位於下列連結︰</span><span class="sxs-lookup"><span data-stu-id="51bd9-189">The actual JSON template is at the following link:</span></span>

- <span data-ttu-id="51bd9-190">https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="51bd9-190">https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json</span></span>

<span data-ttu-id="51bd9-191">此範本會使用來自先前命令的 VHD URL，將 VM 部署至現有的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="51bd9-191">The template deploys a VM into an existing virtual network, using the VHD URL from the earlier command.</span></span> <span data-ttu-id="51bd9-192">下列範例會將範本部署至名為 `myResourceGroup` 的資源群組：</span><span class="sxs-lookup"><span data-stu-id="51bd9-192">The following example deploys the template to the resource group named `myResourceGroup`:</span></span>

```azurecli
azure group deployment create --resource-group myResourceGroup --name myDeployment \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json
```

<span data-ttu-id="51bd9-193">回答範本的提示，例如 VM 名稱 (下列範例中的 `myDeployedVM`)、OS 類型 (`Linux`) 和 VM 大小 (`Standard_DS1_v2`)。</span><span class="sxs-lookup"><span data-stu-id="51bd9-193">Answer the prompts for the template such as VM name (`myDeployedVM` the following example), OS type (`Linux`), and VM size (`Standard_DS1_v2`).</span></span> <span data-ttu-id="51bd9-194">`osDiskVhdUri` 同於先前將現有的虛擬硬碟連結至疑難排解 VM 時所使用的值。</span><span class="sxs-lookup"><span data-stu-id="51bd9-194">The `osDiskVhdUri` is the same as previously used when attaching the existing virtual hard disk to the troubleshooting VM.</span></span> <span data-ttu-id="51bd9-195">命令輸出和提示的範例如下所示︰</span><span class="sxs-lookup"><span data-stu-id="51bd9-195">An example of the command output and prompts is as follows:</span></span>

```azurecli
info:    Executing command group deployment create
info:    Supply values for the following parameters
vmName:  myDeployedVM
osType:  Linux
osDiskVhdUri:  https://mystorageaccount.blob.core.windows.net/vhds/myVM201610292712.vhd
vmSize:  Standard_DS1_v2
existingVirtualNetworkName:  myVnet
existingVirtualNetworkResourceGroup:  myResourceGroup
subnetName:  mySubnet
dnsNameForPublicIP:  mypublicipdeployed
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "mydeployment"
+ Waiting for deployment to complete
+
```


## <a name="re-enable-boot-diagnostics"></a><span data-ttu-id="51bd9-196">重新啟用開機診斷</span><span class="sxs-lookup"><span data-stu-id="51bd9-196">Re-enable boot diagnostics</span></span>

<span data-ttu-id="51bd9-197">當您從現有的虛擬硬碟建立 VM 時，可能不會自動啟用開機診斷。</span><span class="sxs-lookup"><span data-stu-id="51bd9-197">When you create your VM from the existing virtual hard disk, boot diagnostics may not automatically be enabled.</span></span> <span data-ttu-id="51bd9-198">下列範例會在資源群組 `myResourceGroup` 中的 VM `myDeployedVM` 上啟用診斷擴充：</span><span class="sxs-lookup"><span data-stu-id="51bd9-198">The following example enables the diagnostic extension on the VM named `myDeployedVM` in the resource group named `myResourceGroup`:</span></span>

```azurecli
azure vm enable-diag --resource-group myResourceGroup --name myDeployedVM
```

## <a name="next-steps"></a><span data-ttu-id="51bd9-199">後續步驟</span><span class="sxs-lookup"><span data-stu-id="51bd9-199">Next steps</span></span>
<span data-ttu-id="51bd9-200">如果連接至 VM 時發生問題，請參閱[針對 Azure VM 的 SSH 連接進行疑難排解](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="51bd9-200">If you are having issues connecting to your VM, see [Troubleshoot SSH connections to an Azure VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="51bd9-201">如果存取 VM 上執行的應用程式時發生問題，請參閱[針對 Linux VM 上的應用程式連線問題進行疑難排解](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="51bd9-201">For issues with accessing applications running on your VM, see [Troubleshoot application connectivity issues on a Linux VM](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>