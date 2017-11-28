---
title: "Linux VM 疑難排解以 hello Azure CLI 2.0 的 aaaUse |Microsoft 文件"
description: "了解如何連接 hello OS 磁碟 tooa 復原 VM 使用發出 Linux VM 的 tootroubleshoot hello Azure CLI 2.0"
services: virtual-machines-linux
documentationCenter: 
authors: iainfoulds
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/16/2017
ms.author: iainfou
ms.openlocfilehash: 776d61b61280f46e3699157addcdb1e7dfb6818e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-linux-vm-by-attaching-hello-os-disk-tooa-recovery-vm-with-hello-azure-cli-20"></a><span data-ttu-id="f1819-103">藉由附加 hello OS 磁碟 tooa 復原 VM 以 hello Azure CLI 2.0 疑難排解 Linux VM</span><span class="sxs-lookup"><span data-stu-id="f1819-103">Troubleshoot a Linux VM by attaching hello OS disk tooa recovery VM with hello Azure CLI 2.0</span></span>
<span data-ttu-id="f1819-104">如果您的 Linux 虛擬機器 (VM) 會發生開機或磁碟錯誤，您可能需要 tooperform 疑難排解 hello 虛擬硬碟上本身的步驟。</span><span class="sxs-lookup"><span data-stu-id="f1819-104">If your Linux virtual machine (VM) encounters a boot or disk error, you may need tooperform troubleshooting steps on hello virtual hard disk itself.</span></span> <span data-ttu-id="f1819-105">常見範例是無效的項目中`/etc/fstab`，防止 hello VM 可以 tooboot 成功。</span><span class="sxs-lookup"><span data-stu-id="f1819-105">A common example would be an invalid entry in `/etc/fstab` that prevents hello VM from being able tooboot successfully.</span></span> <span data-ttu-id="f1819-106">本文詳細說明如何 toouse hello Azure CLI 2.0 tooconnect 虛擬硬碟磁碟 tooanother Linux VM toofix 任何錯誤，然後重新建立原始 VM。</span><span class="sxs-lookup"><span data-stu-id="f1819-106">This article details how toouse hello Azure CLI 2.0 tooconnect your virtual hard disk tooanother Linux VM toofix any errors, then re-create your original VM.</span></span> <span data-ttu-id="f1819-107">您也可以執行下列步驟以 hello [Azure CLI 1.0](troubleshoot-recovery-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="f1819-107">You can also perform these steps with hello [Azure CLI 1.0](troubleshoot-recovery-disks-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="recovery-process-overview"></a><span data-ttu-id="f1819-108">復原程序概觀</span><span class="sxs-lookup"><span data-stu-id="f1819-108">Recovery process overview</span></span>
<span data-ttu-id="f1819-109">hello 疑難排解程序如下所示：</span><span class="sxs-lookup"><span data-stu-id="f1819-109">hello troubleshooting process is as follows:</span></span>

1. <span data-ttu-id="f1819-110">刪除 hello VM 遇到問題，保留 hello 虛擬硬碟。</span><span class="sxs-lookup"><span data-stu-id="f1819-110">Delete hello VM encountering issues, keeping hello virtual hard disks.</span></span>
2. <span data-ttu-id="f1819-111">附加和掛接 hello Linux VM 的虛擬硬碟 tooanother 供疑難排解之用。</span><span class="sxs-lookup"><span data-stu-id="f1819-111">Attach and mount hello virtual hard disk tooanother Linux VM for troubleshooting purposes.</span></span>
3. <span data-ttu-id="f1819-112">連接 toohello 疑難排解 VM。</span><span class="sxs-lookup"><span data-stu-id="f1819-112">Connect toohello troubleshooting VM.</span></span> <span data-ttu-id="f1819-113">編輯檔案，或在 hello 原始虛擬硬碟上執行任何工具 toofix 問題。</span><span class="sxs-lookup"><span data-stu-id="f1819-113">Edit files or run any tools toofix issues on hello original virtual hard disk.</span></span>
4. <span data-ttu-id="f1819-114">取消掛接並卸離 hello 虛擬硬碟從 hello 疑難排解 VM。</span><span class="sxs-lookup"><span data-stu-id="f1819-114">Unmount and detach hello virtual hard disk from hello troubleshooting VM.</span></span>
5. <span data-ttu-id="f1819-115">使用建立 VM hello 原始虛擬硬碟。</span><span class="sxs-lookup"><span data-stu-id="f1819-115">Create a VM using hello original virtual hard disk.</span></span>

<span data-ttu-id="f1819-116">tooperform 這些疑難排解步驟，您需要最新的 hello [Azure CLI 2.0](/cli/azure/install-az-cli2)安裝並登入 tooan Azure 帳戶使用[az 登入](/cli/azure/#login)。</span><span class="sxs-lookup"><span data-stu-id="f1819-116">tooperform these troubleshooting steps, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="f1819-117">在 hello 下列範例中，會取代您自己的值的參數名稱。</span><span class="sxs-lookup"><span data-stu-id="f1819-117">In hello following examples, replace parameter names with your own values.</span></span> <span data-ttu-id="f1819-118">範例參數名稱包含 `myResourceGroup`、`mystorageaccount` 和 `myVM`。</span><span class="sxs-lookup"><span data-stu-id="f1819-118">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>


## <a name="determine-boot-issues"></a><span data-ttu-id="f1819-119">判斷開機問題</span><span class="sxs-lookup"><span data-stu-id="f1819-119">Determine boot issues</span></span>
<span data-ttu-id="f1819-120">請檢查您的 VM 為何不能 tooboot 正確 hello 序列輸出 toodetermine。</span><span class="sxs-lookup"><span data-stu-id="f1819-120">Examine hello serial output toodetermine why your VM is not able tooboot correctly.</span></span> <span data-ttu-id="f1819-121">常見範例是無效的項目中`/etc/fstab`，或 hello 基礎虛擬硬碟正在刪除或移動。</span><span class="sxs-lookup"><span data-stu-id="f1819-121">A common example is an invalid entry in `/etc/fstab`, or hello underlying virtual hard disk being deleted or moved.</span></span>

<span data-ttu-id="f1819-122">取得與 hello 開機記錄[az vm 開機診斷 get 開機-記錄](/cli/azure/vm/boot-diagnostics#get-boot-log)。</span><span class="sxs-lookup"><span data-stu-id="f1819-122">Get hello boot logs with [az vm boot-diagnostics get-boot-log](/cli/azure/vm/boot-diagnostics#get-boot-log).</span></span> <span data-ttu-id="f1819-123">hello 下列範例會取得 hello 序列輸出從名為 VM hello `myVM` hello 資源群組中名為`myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="f1819-123">hello following example gets hello serial output from hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
az vm boot-diagnostics get-boot-log --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="f1819-124">檢閱 hello 序列輸出的 toodetermine hello VM 失敗 tooboot 的原因。</span><span class="sxs-lookup"><span data-stu-id="f1819-124">Review hello serial output toodetermine why hello VM is failing tooboot.</span></span> <span data-ttu-id="f1819-125">如果 hello 序列輸出不提供任何資訊指出，您可能需要 tooreview 記錄檔中的`/var/log`一旦您擁有 hello 虛擬硬碟連接 tooa 疑難排解 VM。</span><span class="sxs-lookup"><span data-stu-id="f1819-125">If hello serial output isn't providing any indication, you may need tooreview log files in `/var/log` once you have hello virtual hard disk connected tooa troubleshooting VM.</span></span>


## <a name="view-existing-virtual-hard-disk-details"></a><span data-ttu-id="f1819-126">檢視現有的虛擬硬碟詳細資料</span><span class="sxs-lookup"><span data-stu-id="f1819-126">View existing virtual hard disk details</span></span>
<span data-ttu-id="f1819-127">您可以將附加您的虛擬硬碟 (VHD) tooanother VM 之前，您會需要 tooidentify hello hello 作業系統磁碟的 URI。</span><span class="sxs-lookup"><span data-stu-id="f1819-127">Before you can attach your virtual hard disk (VHD) tooanother VM, you need tooidentify hello URI of hello OS disk.</span></span> 

<span data-ttu-id="f1819-128">使用 [az vm show](/cli/azure/vm#show) 檢視 VM 的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="f1819-128">View information about your VM with [az vm show](/cli/azure/vm#show).</span></span> <span data-ttu-id="f1819-129">使用 hello`--query`旗標 tooextract hello URI toohello 作業系統磁碟。</span><span class="sxs-lookup"><span data-stu-id="f1819-129">Use hello `--query` flag tooextract hello URI toohello OS disk.</span></span> <span data-ttu-id="f1819-130">hello 下列範例會取得名為 VM hello 的磁碟資訊`myVM`hello 資源群組中名為`myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="f1819-130">hello following example gets disk information for hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
az vm show --resource-group myResourceGroup --name myVM \
    --query [storageProfile.osDisk.vhd.uri] --output tsv
```

<span data-ttu-id="f1819-131">hello URI 太類似**https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd**。</span><span class="sxs-lookup"><span data-stu-id="f1819-131">hello URI is similar too**https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd**.</span></span>

## <a name="delete-existing-vm"></a><span data-ttu-id="f1819-132">刪除現有的 VM</span><span class="sxs-lookup"><span data-stu-id="f1819-132">Delete existing VM</span></span>
<span data-ttu-id="f1819-133">虛擬硬碟和 VM 在 Azure 中是兩個不同的資源。</span><span class="sxs-lookup"><span data-stu-id="f1819-133">Virtual hard disks and VMs are two distinct resources in Azure.</span></span> <span data-ttu-id="f1819-134">虛擬硬碟是存放 hello 作業系統本身、 應用程式和組態的位置。</span><span class="sxs-lookup"><span data-stu-id="f1819-134">A virtual hard disk is where hello operating system itself, applications, and configurations are stored.</span></span> <span data-ttu-id="f1819-135">hello VM 本身是定義 hello 大小或位置，並參考資源，例如虛擬硬碟或虛擬網路介面卡 (NIC) 的只是中繼資料。</span><span class="sxs-lookup"><span data-stu-id="f1819-135">hello VM itself is just metadata that defines hello size or location, and references resources such as a virtual hard disk or virtual network interface card (NIC).</span></span> <span data-ttu-id="f1819-136">每個虛擬硬碟已連接時，指派租用 tooa VM。</span><span class="sxs-lookup"><span data-stu-id="f1819-136">Each virtual hard disk has a lease assigned when attached tooa VM.</span></span> <span data-ttu-id="f1819-137">雖然可以附加和卸離 hello VM 正在執行時，即使資料磁碟，除非刪除 hello VM 資源無法中斷 hello 作業系統磁碟。</span><span class="sxs-lookup"><span data-stu-id="f1819-137">Although data disks can be attached and detached even while hello VM is running, hello OS disk cannot be detached unless hello VM resource is deleted.</span></span> <span data-ttu-id="f1819-138">hello 租用會繼續 tooassociate hello OS 磁碟 vm，即使該 VM 是處於已停止和取消配置狀態。</span><span class="sxs-lookup"><span data-stu-id="f1819-138">hello lease continues tooassociate hello OS disk with a VM even when that VM is in a stopped and deallocated state.</span></span>

<span data-ttu-id="f1819-139">hello 第一個步驟 toorecover VM 是 toodelete hello VM 資源本身。</span><span class="sxs-lookup"><span data-stu-id="f1819-139">hello first step toorecover your VM is toodelete hello VM resource itself.</span></span> <span data-ttu-id="f1819-140">刪除 hello VM 離開您的儲存體帳戶中的 hello 虛擬硬碟。</span><span class="sxs-lookup"><span data-stu-id="f1819-140">Deleting hello VM leaves hello virtual hard disks in your storage account.</span></span> <span data-ttu-id="f1819-141">刪除 VM hello 之後, 您附加 hello 虛擬硬碟 tooanother VM tootroubleshoot，並解決 hello 錯誤。</span><span class="sxs-lookup"><span data-stu-id="f1819-141">After hello VM is deleted, you attach hello virtual hard disk tooanother VM tootroubleshoot and resolve hello errors.</span></span>

<span data-ttu-id="f1819-142">刪除 hello 與 VM [az vm 刪除](/cli/azure/vm#delete)。</span><span class="sxs-lookup"><span data-stu-id="f1819-142">Delete hello VM with [az vm delete](/cli/azure/vm#delete).</span></span> <span data-ttu-id="f1819-143">下列範例刪除 hello hello 名為 VM`myVM`從名為 hello 資源群組`myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="f1819-143">hello following example deletes hello VM named `myVM` from hello resource group named `myResourceGroup`:</span></span>

```azurecli
az vm delete --resource-group myResourceGroup --name myVM 
```

<span data-ttu-id="f1819-144">請等到完成刪除附加 hello 虛擬硬碟 tooanother VM 之前 hello VM。</span><span class="sxs-lookup"><span data-stu-id="f1819-144">Wait until hello VM has finished deleting before you attach hello virtual hard disk tooanother VM.</span></span> <span data-ttu-id="f1819-145">hello 租用 hello 虛擬硬碟關聯 hello VM 需要 toobe 附加 hello 虛擬硬碟 tooanother VM 之前釋出。</span><span class="sxs-lookup"><span data-stu-id="f1819-145">hello lease on hello virtual hard disk that associates it with hello VM needs toobe released before you can attach hello virtual hard disk tooanother VM.</span></span>


## <a name="attach-existing-virtual-hard-disk-tooanother-vm"></a><span data-ttu-id="f1819-146">附加現有的虛擬硬碟 tooanother VM</span><span class="sxs-lookup"><span data-stu-id="f1819-146">Attach existing virtual hard disk tooanother VM</span></span>
<span data-ttu-id="f1819-147">如 hello 接下來的幾個步驟，您可以使用另一個 VM 供疑難排解之用。</span><span class="sxs-lookup"><span data-stu-id="f1819-147">For hello next few steps, you use another VM for troubleshooting purposes.</span></span> <span data-ttu-id="f1819-148">附加 hello 疑難排解 VM toobrowse 現有虛擬硬碟 toothis 並編輯 hello 磁碟的內容。</span><span class="sxs-lookup"><span data-stu-id="f1819-148">You attach hello existing virtual hard disk toothis troubleshooting VM toobrowse and edit hello disk's content.</span></span> <span data-ttu-id="f1819-149">此程序可讓您 toocorrect 任何組態錯誤或檢閱其他應用程式或系統記錄檔，例如。</span><span class="sxs-lookup"><span data-stu-id="f1819-149">This process allows you toocorrect any configuration errors or review additional application or system log files, for example.</span></span> <span data-ttu-id="f1819-150">選擇或建立另一個 VM toouse 供疑難排解之用。</span><span class="sxs-lookup"><span data-stu-id="f1819-150">Choose or create another VM toouse for troubleshooting purposes.</span></span>

<span data-ttu-id="f1819-151">附加 hello 現有虛擬硬碟與[az vm unmanaged 磁碟附加](/cli/azure/vm/unmanaged-disk#attach)。</span><span class="sxs-lookup"><span data-stu-id="f1819-151">Attach hello existing virtual hard disk with [az vm unmanaged-disk attach](/cli/azure/vm/unmanaged-disk#attach).</span></span> <span data-ttu-id="f1819-152">當您附加 hello 現有虛擬硬碟時，指定在 hello 上述中取得的 hello URI toohello 磁碟`az vm show`命令。</span><span class="sxs-lookup"><span data-stu-id="f1819-152">When you attach hello existing virtual hard disk, specify hello URI toohello disk obtained in hello preceding `az vm show` command.</span></span> <span data-ttu-id="f1819-153">hello 下列範例會附加疑難排解名為 VM 的現有虛擬硬碟 toohello `myVMRecovery` hello 資源群組中名為`myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="f1819-153">hello following example attaches an existing virtual hard disk toohello troubleshooting VM named `myVMRecovery` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
az vm unmanaged-disk attach --resource-group myResourceGroup --vm-name myVMRecovery \
    --vhd-uri https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
```


## <a name="mount-hello-attached-data-disk"></a><span data-ttu-id="f1819-154">掛接 hello 連接的資料磁碟</span><span class="sxs-lookup"><span data-stu-id="f1819-154">Mount hello attached data disk</span></span>

> [!NOTE]
> <span data-ttu-id="f1819-155">hello 下列範例詳細說明 hello Ubuntu 虛擬機器上所需的步驟。</span><span class="sxs-lookup"><span data-stu-id="f1819-155">hello following examples detail hello steps required on an Ubuntu VM.</span></span> <span data-ttu-id="f1819-156">如果您使用不同的 Linux distro，例如 Red Hat Enterprise Linux 或 SUSE，hello 記錄檔位置和`mount`命令可能會稍有不同。</span><span class="sxs-lookup"><span data-stu-id="f1819-156">If you are using a different Linux distro, such as Red Hat Enterprise Linux or SUSE, hello log file locations and `mount` commands may be a little different.</span></span> <span data-ttu-id="f1819-157">如需您特定 distro hello 命令中的適當變更，請參閱 toohello 文件。</span><span class="sxs-lookup"><span data-stu-id="f1819-157">Refer toohello documentation for your specific distro for hello appropriate changes in commands.</span></span>

1. <span data-ttu-id="f1819-158">SSH tooyour 疑難排解 VM 使用 hello 適當的認證。</span><span class="sxs-lookup"><span data-stu-id="f1819-158">SSH tooyour troubleshooting VM using hello appropriate credentials.</span></span> <span data-ttu-id="f1819-159">如果這個磁碟是 hello 第一個資料磁碟附加 tooyour 疑難排解 VM，hello 磁碟的連接可能太`/dev/sdc`。</span><span class="sxs-lookup"><span data-stu-id="f1819-159">If this disk is hello first data disk attached tooyour troubleshooting VM, hello disk is likely connected too`/dev/sdc`.</span></span> <span data-ttu-id="f1819-160">使用`dmseg`tooview 連接的磁碟：</span><span class="sxs-lookup"><span data-stu-id="f1819-160">Use `dmseg` tooview attached disks:</span></span>

    ```bash
    dmesg | grep SCSI
    ```

    <span data-ttu-id="f1819-161">hello 輸出是 toohello 類似下列範例程式碼：</span><span class="sxs-lookup"><span data-stu-id="f1819-161">hello output is similar toohello following example:</span></span>

    ```bash
    [    0.294784] SCSI subsystem initialized
    [    0.573458] Block layer SCSI generic (bsg) driver version 0.4 loaded (major 252)
    [    7.110271] sd 2:0:0:0: [sda] Attached SCSI disk
    [    8.079653] sd 3:0:1:0: [sdb] Attached SCSI disk
    [ 1828.162306] sd 5:0:0:0: [sdc] Attached SCSI disk
    ```

    <span data-ttu-id="f1819-162">在上述範例中的 hello，hello OS 磁碟位於`/dev/sda`和 hello 暫存磁碟提供給每個 VM 位於`/dev/sdb`。</span><span class="sxs-lookup"><span data-stu-id="f1819-162">In hello preceding example, hello OS disk is at `/dev/sda` and hello temporary disk provided for each VM is at `/dev/sdb`.</span></span> <span data-ttu-id="f1819-163">如果您有多個資料磁碟，它們應該是位於 `/dev/sdd`、`/dev/sde`，依此類推。</span><span class="sxs-lookup"><span data-stu-id="f1819-163">If you had multiple data disks, they should be at `/dev/sdd`, `/dev/sde`, and so on.</span></span>

2. <span data-ttu-id="f1819-164">建立目錄 toomount 您現有的虛擬硬碟。</span><span class="sxs-lookup"><span data-stu-id="f1819-164">Create a directory toomount your existing virtual hard disk.</span></span> <span data-ttu-id="f1819-165">hello 下列範例會建立一個名為目錄`troubleshootingdisk`:</span><span class="sxs-lookup"><span data-stu-id="f1819-165">hello following example creates a directory named `troubleshootingdisk`:</span></span>

    ```bash
    sudo mkdir /mnt/troubleshootingdisk
    ```

3. <span data-ttu-id="f1819-166">如果您在現有的虛擬硬碟上有多個資料分割，裝載所需的 hello 磁碟分割。</span><span class="sxs-lookup"><span data-stu-id="f1819-166">If you have multiple partitions on your existing virtual hard disk, mount hello required partition.</span></span> <span data-ttu-id="f1819-167">hello 下列範例會 hello 第一個主要磁碟分割在`/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="f1819-167">hello following example mounts hello first primary partition at `/dev/sdc1`:</span></span>

    ```bash
    sudo mount /dev/sdc1 /mnt/troubleshootingdisk
    ```

    > [!NOTE]
    > <span data-ttu-id="f1819-168">最佳作法是 toomount 資料磁碟上的 Vm 在 Azure 中使用 hello hello 虛擬硬碟的通用唯一識別碼 (UUID)。</span><span class="sxs-lookup"><span data-stu-id="f1819-168">Best practice is toomount data disks on VMs in Azure using hello universally unique identifier (UUID) of hello virtual hard disk.</span></span> <span data-ttu-id="f1819-169">針對這個簡短的疑難排解案例，不需要掛接 hello 虛擬硬碟使用 hello UUID。</span><span class="sxs-lookup"><span data-stu-id="f1819-169">For this short troubleshooting scenario, mounting hello virtual hard disk using hello UUID is not necessary.</span></span> <span data-ttu-id="f1819-170">但是，在正常使用，編輯`/etc/fstab`toomount 虛擬硬碟使用的裝置名稱，而非可能會造成 UUID hello VM toofail tooboot。</span><span class="sxs-lookup"><span data-stu-id="f1819-170">However, under normal use, editing `/etc/fstab` toomount virtual hard disks using device name rather than UUID may cause hello VM toofail tooboot.</span></span>


## <a name="fix-issues-on-original-virtual-hard-disk"></a><span data-ttu-id="f1819-171">修正原始虛擬硬碟的問題</span><span class="sxs-lookup"><span data-stu-id="f1819-171">Fix issues on original virtual hard disk</span></span>
<span data-ttu-id="f1819-172">與 hello 現有虛擬硬碟掛接，您現在可以執行任何維護和疑難排解步驟，視需要。</span><span class="sxs-lookup"><span data-stu-id="f1819-172">With hello existing virtual hard disk mounted, you can now perform any maintenance and troubleshooting steps as needed.</span></span> <span data-ttu-id="f1819-173">一旦解決 hello 問題之後，繼續進行步驟 hello。</span><span class="sxs-lookup"><span data-stu-id="f1819-173">Once you have addressed hello issues, continue with hello following steps.</span></span>


## <a name="unmount-and-detach-original-virtual-hard-disk"></a><span data-ttu-id="f1819-174">卸載並中斷連結原始虛擬硬碟</span><span class="sxs-lookup"><span data-stu-id="f1819-174">Unmount and detach original virtual hard disk</span></span>
<span data-ttu-id="f1819-175">一旦解決的錯誤，您會卸載，並中斷您疑難排解的 VM 中的 hello 現有虛擬硬碟。</span><span class="sxs-lookup"><span data-stu-id="f1819-175">Once your errors are resolved, you unmount and detach hello existing virtual hard disk from your troubleshooting VM.</span></span> <span data-ttu-id="f1819-176">您無法使用虛擬硬碟與任何其他 VM，直到釋放附加 hello 疑難排解 VM 的虛擬硬碟 toohello hello 租用。</span><span class="sxs-lookup"><span data-stu-id="f1819-176">You cannot use your virtual hard disk with any other VM until hello lease attaching hello virtual hard disk toohello troubleshooting VM is released.</span></span>

1. <span data-ttu-id="f1819-177">從 hello SSH 工作階段 tooyour 疑難排解 VM，卸載 hello 現有虛擬硬碟。</span><span class="sxs-lookup"><span data-stu-id="f1819-177">From hello SSH session tooyour troubleshooting VM, unmount hello existing virtual hard disk.</span></span> <span data-ttu-id="f1819-178">第一次變更超出您掛接點的 hello 父目錄：</span><span class="sxs-lookup"><span data-stu-id="f1819-178">Change out of hello parent directory for your mount point first:</span></span>

    ```bash
    cd /
    ```

    <span data-ttu-id="f1819-179">現在取消掛接 hello 現有虛擬硬碟。</span><span class="sxs-lookup"><span data-stu-id="f1819-179">Now unmount hello existing virtual hard disk.</span></span> <span data-ttu-id="f1819-180">hello 下例取消掛接在 hello 裝置`/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="f1819-180">hello following example unmounts hello device at `/dev/sdc1`:</span></span>

    ```bash
    sudo umount /dev/sdc1
    ```

2. <span data-ttu-id="f1819-181">現在您可以卸離 hello 虛擬硬碟從 hello VM。</span><span class="sxs-lookup"><span data-stu-id="f1819-181">Now detach hello virtual hard disk from hello VM.</span></span> <span data-ttu-id="f1819-182">結束 hello SSH 工作階段 tooyour 疑難排解 VM。</span><span class="sxs-lookup"><span data-stu-id="f1819-182">Exit hello SSH session tooyour troubleshooting VM.</span></span> <span data-ttu-id="f1819-183">清單 hello 附加資料磁碟 tooyour 疑難排解與 VM [az vm unmanaged 磁碟清單](/cli/azure/vm/unmanaged-disk#list)。</span><span class="sxs-lookup"><span data-stu-id="f1819-183">List hello attached data disks tooyour troubleshooting VM with [az vm unmanaged-disk list](/cli/azure/vm/unmanaged-disk#list).</span></span> <span data-ttu-id="f1819-184">hello 下列範例列出 hello 資料磁碟附加 toohello 名為 VM `myVMRecovery` hello 資源群組中名為`myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="f1819-184">hello following example lists hello data disks attached toohello VM named `myVMRecovery` in hello resource group named `myResourceGroup`:</span></span>

    ```azurecli
    azure vm unmanaged-disk list --resource-group myResourceGroup --vm-name myVMRecovery \
        --query '[].{Disk:vhd.uri}' --output table
    ```

    <span data-ttu-id="f1819-185">請注意 hello 您現有的虛擬硬碟的名稱。</span><span class="sxs-lookup"><span data-stu-id="f1819-185">Note hello name for your existing virtual hard disk.</span></span> <span data-ttu-id="f1819-186">Hello 與磁碟名稱，例如 hello URI **https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd**是**myVHD**。</span><span class="sxs-lookup"><span data-stu-id="f1819-186">For example, hello name of a disk with hello URI of **https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd** is **myVHD**.</span></span> 

    <span data-ttu-id="f1819-187">卸離 hello 來自 VM 的資料磁碟[az vm unmanaged 磁碟卸離](/cli/azure/vm/unmanaged-disk#detach)。</span><span class="sxs-lookup"><span data-stu-id="f1819-187">Detach hello data disk from your VM [az vm unmanaged-disk detach](/cli/azure/vm/unmanaged-disk#detach).</span></span> <span data-ttu-id="f1819-188">hello 下列範例會卸離名為 「 hello 磁碟`myVHD`hello 名為 VM 從`myVMRecovery`在 hello`myResourceGroup`資源群組：</span><span class="sxs-lookup"><span data-stu-id="f1819-188">hello following example detaches hello disk named `myVHD` from hello VM named `myVMRecovery` in hello `myResourceGroup` resource group:</span></span>

    ```azurecli
    az vm unmanaged-disk detach --resource-group myResourceGroup --vm-name myVMRecovery \
        --name myVHD
    ```


## <a name="create-vm-from-original-hard-disk"></a><span data-ttu-id="f1819-189">從原始硬碟建立 VM</span><span class="sxs-lookup"><span data-stu-id="f1819-189">Create VM from original hard disk</span></span>
<span data-ttu-id="f1819-190">toocreate 原始虛擬硬碟，從 VM 使用[此 Azure Resource Manager 範本](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd)。</span><span class="sxs-lookup"><span data-stu-id="f1819-190">toocreate a VM from your original virtual hard disk, use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd).</span></span> <span data-ttu-id="f1819-191">hello 實際的 JSON 範本位於 hello 下列連結：</span><span class="sxs-lookup"><span data-stu-id="f1819-191">hello actual JSON template is at hello following link:</span></span>

- <span data-ttu-id="f1819-192">https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="f1819-192">https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json</span></span>

<span data-ttu-id="f1819-193">hello 範本部署 VM，使用從 hello hello VHD URI 稍早的命令。</span><span class="sxs-lookup"><span data-stu-id="f1819-193">hello template deploys a VM using hello VHD URI from hello earlier command.</span></span> <span data-ttu-id="f1819-194">部署與 hello 範本[az 群組部署建立](/cli/azure/group/deployment#create)。</span><span class="sxs-lookup"><span data-stu-id="f1819-194">Deploy hello template with [az group deployment create](/cli/azure/group/deployment#create).</span></span> <span data-ttu-id="f1819-195">提供 hello URI tooyour 原始 VHD，然後指定 hello 作業系統類型、 VM 大小和 VM 名稱，如下所示：</span><span class="sxs-lookup"><span data-stu-id="f1819-195">Provide hello URI tooyour original VHD and then specify hello OS type, VM size, and VM name as follows:</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup --name myDeployment \
  --parameters '{"osDiskVhdUri": {"value": "https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd"},
    "osType": {"value": "Linux"},
    "vmSize": {"value": "Standard_DS1_v2"},
    "vmName": {"value": "myDeployedVM"}}' \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd/azuredeploy.json
```

## <a name="re-enable-boot-diagnostics"></a><span data-ttu-id="f1819-196">重新啟用開機診斷</span><span class="sxs-lookup"><span data-stu-id="f1819-196">Re-enable boot diagnostics</span></span>
<span data-ttu-id="f1819-197">當您從 hello 現有虛擬硬碟建立 VM 時，開機診斷可能不會自動啟用。</span><span class="sxs-lookup"><span data-stu-id="f1819-197">When you create your VM from hello existing virtual hard disk, boot diagnostics may not automatically be enabled.</span></span> <span data-ttu-id="f1819-198">使用 [az vm boot-diagnostics enable](/cli/azure/vm/boot-diagnostics#enable) 啟用開機診斷。</span><span class="sxs-lookup"><span data-stu-id="f1819-198">Enable boot diagnostics with [az vm boot-diagnostics enable](/cli/azure/vm/boot-diagnostics#enable).</span></span> <span data-ttu-id="f1819-199">hello 下列範例會啟用 hello hello 名為 VM 上的診斷延伸模組`myDeployedVM`hello 資源群組中名為`myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="f1819-199">hello following example enables hello diagnostic extension on hello VM named `myDeployedVM` in hello resource group named `myResourceGroup`:</span></span>

```azurecli
az vm boot-diagnostics enable --resource-group myResourceGroup --name myDeployedVM
```

## <a name="next-steps"></a><span data-ttu-id="f1819-200">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f1819-200">Next steps</span></span>
<span data-ttu-id="f1819-201">如果您有連接 tooyour VM 的問題，請參閱[疑難排解 SSH 連線 tooan Azure VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="f1819-201">If you are having issues connecting tooyour VM, see [Troubleshoot SSH connections tooan Azure VM](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="f1819-202">如果存取 VM 上執行的應用程式時發生問題，請參閱[針對 Linux VM 上的應用程式連線問題進行疑難排解](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="f1819-202">For issues with accessing applications running on your VM, see [Troubleshoot application connectivity issues on a Linux VM](../windows/troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
