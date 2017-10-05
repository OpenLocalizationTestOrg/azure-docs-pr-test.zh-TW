---
title: "在執行 Linux 的虛擬機器上設定 LVM | Microsoft Docs"
description: "了解如何在 Azure 中的 Linux 上設定 LVM"
services: virtual-machines-linux
documentationcenter: na
author: szarkos
manager: timlt
editor: tysonn
tag: azure-service-management,azure-resource-manager
ms.assetid: 7f533725-1484-479d-9472-6b3098d0aecc
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: 7926627aaa3f0da935131f491d927ab5cb4b35c9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="configure-lvm-on-a-linux-vm-in-azure"></a><span data-ttu-id="7465c-103">設定 Azure 中 Linux VM 的 LVM</span><span class="sxs-lookup"><span data-stu-id="7465c-103">Configure LVM on a Linux VM in Azure</span></span>
<span data-ttu-id="7465c-104">本文將討論如何在 Azure 虛擬機器中設定邏輯磁碟區管理員 (LVM)。</span><span class="sxs-lookup"><span data-stu-id="7465c-104">This document will discuss how to configure Logical Volume Manager (LVM) in your Azure virtual machine.</span></span> <span data-ttu-id="7465c-105">雖然可以在任何連接到虛擬機器的磁碟上設定 LVM，但根據預設，大部分的雲端映像不會在作業系統磁碟上設定 LVM。</span><span class="sxs-lookup"><span data-stu-id="7465c-105">While it is feasible to configure LVM on any disk attached to the virtual machine, by default most cloud images will not have LVM configured on the OS disk.</span></span> <span data-ttu-id="7465c-106">這是為了防止重複磁碟區群組相關的問題，因為作業系統磁碟可能曾經連接到相同散發套件及類型的 VM (例如在復原期間)。</span><span class="sxs-lookup"><span data-stu-id="7465c-106">This is to prevent problems with duplicate volume groups if the OS disk is ever attached to another VM of the same distribution and type, i.e. during a recovery scenario.</span></span> <span data-ttu-id="7465c-107">因此建議只在資料磁碟上使用 LVM。</span><span class="sxs-lookup"><span data-stu-id="7465c-107">Therefore it is recommended only to use LVM on the data disks.</span></span>

## <a name="linear-vs-striped-logical-volumes"></a><span data-ttu-id="7465c-108">線性與等量邏輯磁碟區</span><span class="sxs-lookup"><span data-stu-id="7465c-108">Linear vs. striped logical volumes</span></span>
<span data-ttu-id="7465c-109">LVM 可以用來將數個實體磁碟的結合成單一存放磁碟區。</span><span class="sxs-lookup"><span data-stu-id="7465c-109">LVM can be used to combine a number of physical disks into a single storage volume.</span></span> <span data-ttu-id="7465c-110">根據預設 LVM 通常會建立線性邏輯磁碟區，這表示實體儲存體是串連在一起。</span><span class="sxs-lookup"><span data-stu-id="7465c-110">By default LVM will usually create linear logical volumes, which means that the physical storage is concatenated together.</span></span> <span data-ttu-id="7465c-111">在此情況下，讀取/寫入作業通常只會傳送至單一磁碟。</span><span class="sxs-lookup"><span data-stu-id="7465c-111">In this case read/write operations will typically only be sent to a single disk.</span></span> <span data-ttu-id="7465c-112">相反地，我們也可以建立等量邏輯磁碟區，其中讀取和寫入會分散到磁碟區群組中的多個磁碟 (類似 RAID0)。</span><span class="sxs-lookup"><span data-stu-id="7465c-112">In contrast, we can also create striped logical volumes where reads and writes are distributed to multiple disks contained in the volume group (i.e. similar to RAID0).</span></span> <span data-ttu-id="7465c-113">基於效能考量，您可能會希望建立等量邏輯磁碟區，使讀取和寫入時會用到所有已連接的資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="7465c-113">For performance reasons it is likely you will want to stripe your logical volumes so that reads and writes utilize all your attached data disks.</span></span>

<span data-ttu-id="7465c-114">本文件將說明如何將數個資料磁碟結合成單一磁碟區群組，然後再建立等量邏輯磁碟區。</span><span class="sxs-lookup"><span data-stu-id="7465c-114">This document will describe how to combine several data disks into a single volume group, and then create a striped logical volume.</span></span> <span data-ttu-id="7465c-115">下列為一般性步驟，可適用於大部分的散發套件。</span><span class="sxs-lookup"><span data-stu-id="7465c-115">The steps below are somewhat generalized to work with most distributions.</span></span> <span data-ttu-id="7465c-116">在大部分情況下，Azure 上用於管理 LVM 的公用程式和工作流程，與其他環境中的基本上都相同。</span><span class="sxs-lookup"><span data-stu-id="7465c-116">In most cases the utilities and workflows for managing LVM on Azure are not fundamentally different than other environments.</span></span> <span data-ttu-id="7465c-117">像往常一樣，也請向您的 Linux 廠商洽詢搭配特定散發套件使用 LVM 的文件和最佳做法。</span><span class="sxs-lookup"><span data-stu-id="7465c-117">As usual, please also consult your Linux vendor for documentation and best practices for using LVM with your particular distribution.</span></span>

## <a name="attaching-data-disks"></a><span data-ttu-id="7465c-118">連接資料磁碟</span><span class="sxs-lookup"><span data-stu-id="7465c-118">Attaching data disks</span></span>
<span data-ttu-id="7465c-119">使用 LVM 時，通常一開始會用二個或更多的空資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="7465c-119">One will usually want to start with two or more empty data disks when using LVM.</span></span> <span data-ttu-id="7465c-120">根據 IO 需求，您可以選擇連接儲存在標準儲存體且一個磁碟最多具有 500 IO/ps 的磁碟，或進階儲存體且一個磁碟最多具有 5000 IO/ps 的磁碟。</span><span class="sxs-lookup"><span data-stu-id="7465c-120">Based on your IO needs, you can choose to attach disks that are stored in our Standard Storage, with up to 500 IO/ps per disk or our Premium storage with up to 5000 IO/ps per disk.</span></span> <span data-ttu-id="7465c-121">本文將不會詳細說明如何佈建資料磁碟以及將其連接至 Linux 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="7465c-121">This article will not go into detail on how to provision and attach data disks to a Linux virtual machine.</span></span> <span data-ttu-id="7465c-122">請參閱 Microsoft Azure 文章[連接磁碟](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)，取得如何在 Azure 上將空白資料磁碟連接至 Linux 虛擬機器的詳細指示。</span><span class="sxs-lookup"><span data-stu-id="7465c-122">Please see the Microsoft Azure article [attach a disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for detailed instructions on how to attach an empty data disk to a Linux virtual machine on Azure.</span></span>

## <a name="install-the-lvm-utilities"></a><span data-ttu-id="7465c-123">安裝 LVM 公用程式</span><span class="sxs-lookup"><span data-stu-id="7465c-123">Install the LVM utilities</span></span>
* <span data-ttu-id="7465c-124">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="7465c-124">**Ubuntu**</span></span>

    ```bash  
    sudo apt-get update
    sudo apt-get install lvm2
    ```

* <span data-ttu-id="7465c-125">**RHEL、CentOS 和 Oracle Linux**</span><span class="sxs-lookup"><span data-stu-id="7465c-125">**RHEL, CentOS & Oracle Linux**</span></span>

    ```bash   
    sudo yum install lvm2
    ```

* <span data-ttu-id="7465c-126">**SLES 12 和 openSUSE**</span><span class="sxs-lookup"><span data-stu-id="7465c-126">**SLES 12 and openSUSE**</span></span>

    ```bash   
    sudo zypper install lvm2
    ```

* <span data-ttu-id="7465c-127">**SLES 11**</span><span class="sxs-lookup"><span data-stu-id="7465c-127">**SLES 11**</span></span>

    ```bash   
    sudo zypper install lvm2
    ```

    <span data-ttu-id="7465c-128">在 SLES11 上，您也必須編輯 `/etc/sysconfig/lvm` 並將 `LVM_ACTIVATED_ON_DISCOVERED` 設為 "enable"：</span><span class="sxs-lookup"><span data-stu-id="7465c-128">On SLES11 you must also edit `/etc/sysconfig/lvm` and set `LVM_ACTIVATED_ON_DISCOVERED` to "enable":</span></span>

    ```sh   
    LVM_ACTIVATED_ON_DISCOVERED="enable" 
    ```

## <a name="configure-lvm"></a><span data-ttu-id="7465c-129">設定 LVM</span><span class="sxs-lookup"><span data-stu-id="7465c-129">Configure LVM</span></span>
<span data-ttu-id="7465c-130">本指南假設您已經連接三個資料磁碟，我們會以 `/dev/sdc`、`/dev/sdd` 和 `/dev/sde` 來代表。</span><span class="sxs-lookup"><span data-stu-id="7465c-130">In this guide we will assume you have attached three data disks, which we'll refer to as `/dev/sdc`, `/dev/sdd` and `/dev/sde`.</span></span> <span data-ttu-id="7465c-131">請注意，您 VM 中的路徑名稱不一定與上述的相同。</span><span class="sxs-lookup"><span data-stu-id="7465c-131">Note that these may not always be the same path names in your VM.</span></span> <span data-ttu-id="7465c-132">您可以執行 '`sudo fdisk -l`' 或類似的命令以列出可用的磁碟。</span><span class="sxs-lookup"><span data-stu-id="7465c-132">You can run '`sudo fdisk -l`' or similar command to list your available disks.</span></span>

1. <span data-ttu-id="7465c-133">準備實體磁碟區：</span><span class="sxs-lookup"><span data-stu-id="7465c-133">Prepare the physical volumes:</span></span>

    ```bash    
    sudo pvcreate /dev/sd[cde]
    Physical volume "/dev/sdc" successfully created
    Physical volume "/dev/sdd" successfully created
    Physical volume "/dev/sde" successfully created
    ```

2. <span data-ttu-id="7465c-134">建立磁碟區群組。</span><span class="sxs-lookup"><span data-stu-id="7465c-134">Create a volume group.</span></span> <span data-ttu-id="7465c-135">我們在此範例中呼叫磁碟區群組 `data-vg01`：</span><span class="sxs-lookup"><span data-stu-id="7465c-135">In this example we are calling the volume group `data-vg01`:</span></span>

    ```bash    
    sudo vgcreate data-vg01 /dev/sd[cde]
    Volume group "data-vg01" successfully created
    ```

3. <span data-ttu-id="7465c-136">建立一或多個邏輯磁碟區。</span><span class="sxs-lookup"><span data-stu-id="7465c-136">Create the logical volume(s).</span></span> <span data-ttu-id="7465c-137">以下命令會建立名為 `data-lv01` 的單一邏輯磁碟區，以橫跨整個磁碟區群組，但是請留意，在磁碟區群組中建立多個邏輯磁碟區也是可行的。</span><span class="sxs-lookup"><span data-stu-id="7465c-137">The command below we will create a single logical volume called `data-lv01` to span the entire volume group, but note that it is also feasible to create multiple logical volumes in the volume group.</span></span>

    ```bash   
    sudo lvcreate --extents 100%FREE --stripes 3 --name data-lv01 data-vg01
    Logical volume "data-lv01" created.
    ```

4. <span data-ttu-id="7465c-138">格式化邏輯磁碟區</span><span class="sxs-lookup"><span data-stu-id="7465c-138">Format the logical volume</span></span>

    ```bash  
    sudo mkfs -t ext4 /dev/data-vg01/data-lv01
    ```
   
   > [!NOTE]
   > <span data-ttu-id="7465c-139">SLES11 請使用 `-t ext3` 而不是 ext4。</span><span class="sxs-lookup"><span data-stu-id="7465c-139">With SLES11 use `-t ext3` instead of ext4.</span></span> <span data-ttu-id="7465c-140">SLES11 對於 ext4 檔案系統只支援唯讀權限。</span><span class="sxs-lookup"><span data-stu-id="7465c-140">SLES11 only supports read-only access to ext4 filesystems.</span></span>

## <a name="add-the-new-file-system-to-etcfstab"></a><span data-ttu-id="7465c-141">將新的檔案系統新增至 /etc/fstab</span><span class="sxs-lookup"><span data-stu-id="7465c-141">Add the new file system to /etc/fstab</span></span>
> [!IMPORTANT]
> <span data-ttu-id="7465c-142">不當編輯 `/etc/fstab` 檔案會導致系統無法開機。</span><span class="sxs-lookup"><span data-stu-id="7465c-142">Improperly editing the `/etc/fstab` file could result in an unbootable system.</span></span> <span data-ttu-id="7465c-143">如果不確定，請參閱散發套件的文件，以取得如何適當編輯此檔案的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="7465c-143">If unsure, please refer to the distribution's documentation for information on how to properly edit this file.</span></span> <span data-ttu-id="7465c-144">在編輯之前，也建議先備份 `/etc/fstab` 檔案。</span><span class="sxs-lookup"><span data-stu-id="7465c-144">It is also recommended that a backup of the `/etc/fstab` file is created before editing.</span></span>

1. <span data-ttu-id="7465c-145">建立新檔案系統所需的掛接點，例如：</span><span class="sxs-lookup"><span data-stu-id="7465c-145">Create the desired mount point for your new file system, for example:</span></span>

    ```bash  
    sudo mkdir /data
    ```

2. <span data-ttu-id="7465c-146">找出邏輯磁碟區的路徑</span><span class="sxs-lookup"><span data-stu-id="7465c-146">Locate the logical volume path</span></span>

    ```bash    
    lvdisplay
    --- Logical volume ---
    LV Path                /dev/data-vg01/data-lv01
    ....
    ```

3. <span data-ttu-id="7465c-147">在文字編輯器中開啟 `/etc/fstab`，並為新檔案系統新增項目，例如：</span><span class="sxs-lookup"><span data-stu-id="7465c-147">Open `/etc/fstab` in a text editor and add an entry for the new file system, for example:</span></span>

    ```bash    
    /dev/data-vg01/data-lv01  /data  ext4  defaults  0  2
    ```   
    <span data-ttu-id="7465c-148">然後，儲存並關閉 `/etc/fstab`。</span><span class="sxs-lookup"><span data-stu-id="7465c-148">Then, save and close `/etc/fstab`.</span></span>

4. <span data-ttu-id="7465c-149">測試 `/etc/fstab` 項目是否正確：</span><span class="sxs-lookup"><span data-stu-id="7465c-149">Test that the `/etc/fstab` entry is correct:</span></span>

    ```bash    
    sudo mount -a
    ```

    <span data-ttu-id="7465c-150">如果此命令會產生錯誤訊息，請檢查 `/etc/fstab` 檔案中的語法。</span><span class="sxs-lookup"><span data-stu-id="7465c-150">If this command results in an error message please check the syntax in the `/etc/fstab` file.</span></span>
   
    <span data-ttu-id="7465c-151">接下來，執行 `mount` 命令，以確保已掛接檔案系統：</span><span class="sxs-lookup"><span data-stu-id="7465c-151">Next run the `mount` command to ensure the file system is mounted:</span></span>

    ```bash    
    mount
    ......
    /dev/mapper/data--vg01-data--lv01 on /data type ext4 (rw)
    ```

5. <span data-ttu-id="7465c-152">(選擇性) 保全 `/etc/fstab`中的開機參數</span><span class="sxs-lookup"><span data-stu-id="7465c-152">(Optional) Failsafe boot parameters in `/etc/fstab`</span></span>
   
    <span data-ttu-id="7465c-153">許多散發套件包含 `nobootwait` 或 `nofail` 掛接參數，可加入至 `/etc/fstab` 檔案。</span><span class="sxs-lookup"><span data-stu-id="7465c-153">Many distributions include either the `nobootwait` or `nofail` mount parameters that may be added to the `/etc/fstab` file.</span></span> <span data-ttu-id="7465c-154">這些參數容許發生掛接特定檔案系統失敗，並容許 Linux 系統繼續開機，即使它無法正確地掛接 RAID 檔案系統。</span><span class="sxs-lookup"><span data-stu-id="7465c-154">These parameters allow for failures when mounting a particular file system and allow the Linux system to continue to boot even if it is unable to properly mount the RAID file system.</span></span> <span data-ttu-id="7465c-155">請查閱散發套件的文件，以取得這些參數的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="7465c-155">Please refer to your distribution's documentation for more information on these parameters.</span></span>
   
    <span data-ttu-id="7465c-156">範例 (Ubuntu)：</span><span class="sxs-lookup"><span data-stu-id="7465c-156">Example (Ubuntu):</span></span>

    ```bash 
    /dev/data-vg01/data-lv01  /data  ext4  defaults,nobootwait  0  2
    ```

## <a name="trimunmap-support"></a><span data-ttu-id="7465c-157">TRIM/UNMAP 支援</span><span class="sxs-lookup"><span data-stu-id="7465c-157">TRIM/UNMAP support</span></span>
<span data-ttu-id="7465c-158">有些 Linux 核心會支援 TRIM/UNMAP 作業以捨棄磁碟上未使用的區塊。</span><span class="sxs-lookup"><span data-stu-id="7465c-158">Some Linux kernels support TRIM/UNMAP operations to discard unused blocks on the disk.</span></span> <span data-ttu-id="7465c-159">這些作業主要是在標準儲存體中相當實用，可用來通知 Azure 已刪除的頁面已不再有效而可予以捨棄。</span><span class="sxs-lookup"><span data-stu-id="7465c-159">These operations are primarily useful in standard storage to inform Azure that deleted pages are no longer valid and can be discarded.</span></span> <span data-ttu-id="7465c-160">如果您建立大型檔案，然後再將它們刪除，捨棄頁面可以節省成本。</span><span class="sxs-lookup"><span data-stu-id="7465c-160">Discarding pages can save cost if you create large files and then delete them.</span></span>

<span data-ttu-id="7465c-161">有兩種方式可在 Linux VM 中啟用 TRIM 支援。</span><span class="sxs-lookup"><span data-stu-id="7465c-161">There are two ways to enable TRIM support in your Linux VM.</span></span> <span data-ttu-id="7465c-162">像往常一樣，請參閱您的散發套件以了解建議的方法︰</span><span class="sxs-lookup"><span data-stu-id="7465c-162">As usual, consult your distribution for the recommended approach:</span></span>

- <span data-ttu-id="7465c-163">在 `/etc/fstab` 中使用 `discard` 掛接選項，例如：</span><span class="sxs-lookup"><span data-stu-id="7465c-163">Use the `discard` mount option in `/etc/fstab`, for example:</span></span>

    ```bash 
    /dev/data-vg01/data-lv01  /data  ext4  defaults,discard  0  2
    ```

- <span data-ttu-id="7465c-164">在某些情況下，`discard` 選項可能會影響效能。</span><span class="sxs-lookup"><span data-stu-id="7465c-164">In some cases the `discard` option may have performance implications.</span></span> <span data-ttu-id="7465c-165">或者，您也可以從命令列手動執行 `fstrim` 命令，或將它新增到 crontab 來定期執行︰</span><span class="sxs-lookup"><span data-stu-id="7465c-165">Alternatively, you can run the `fstrim` command manually from the command line, or add it to your crontab to run regularly:</span></span>

    <span data-ttu-id="7465c-166">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="7465c-166">**Ubuntu**</span></span>

    ```bash 
    # sudo apt-get install util-linux
    # sudo fstrim /datadrive
    ```

    <span data-ttu-id="7465c-167">**RHEL/CentOS**</span><span class="sxs-lookup"><span data-stu-id="7465c-167">**RHEL/CentOS**</span></span>

    ```bash 
    # sudo yum install util-linux
    # sudo fstrim /datadrive
    ```
