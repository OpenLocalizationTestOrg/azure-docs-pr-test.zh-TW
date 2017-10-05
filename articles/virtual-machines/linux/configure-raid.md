---
title: "在執行 Linux 的虛擬機器上設定軟體 RAID | Microsoft Docs"
description: "了解如何使用 mdadm，在 Azure 的 Linux 上設定 RAID。"
services: virtual-machines-linux
documentationcenter: na
author: rickstercdn
manager: timlt
editor: tysonn
tag: azure-service-management,azure-resource-manager
ms.assetid: f3cb2786-bda6-4d2c-9aaf-2db80f490feb
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: rclaus
ms.openlocfilehash: 12f540a700fbf85e579e8aadc9f6def039299ff7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="configure-software-raid-on-linux"></a><span data-ttu-id="3b5df-103">在 Linux 上設定軟體 RAID</span><span class="sxs-lookup"><span data-stu-id="3b5df-103">Configure Software RAID on Linux</span></span>
<span data-ttu-id="3b5df-104">在 Azure 的 Linux 虛擬機器上使用軟體 RAID，以單一 RAID 裝置的形式顯示多個連接的資料磁碟，這種案例很常遇到。</span><span class="sxs-lookup"><span data-stu-id="3b5df-104">It's a common scenario to use software RAID on Linux virtual machines in Azure to present multiple attached data disks as a single RAID device.</span></span> <span data-ttu-id="3b5df-105">相較於只使用單一磁碟，這通常可用來提高效能並允許增加輸送量。</span><span class="sxs-lookup"><span data-stu-id="3b5df-105">Typically this can be used to improve performance and allow for improved throughput compared to using just a single disk.</span></span>

## <a name="attaching-data-disks"></a><span data-ttu-id="3b5df-106">連接資料磁碟</span><span class="sxs-lookup"><span data-stu-id="3b5df-106">Attaching data disks</span></span>
<span data-ttu-id="3b5df-107">設定 RAID 裝置需要兩個以上的空白資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="3b5df-107">Two or more empty data disks are needed to configure a RAID device.</span></span>  <span data-ttu-id="3b5df-108">建立 RAID 裝置的主要原因是要提升磁碟 IO 效能。</span><span class="sxs-lookup"><span data-stu-id="3b5df-108">The primary reason for creating a RAID device is to improve performance of your disk IO.</span></span>  <span data-ttu-id="3b5df-109">根據 IO 需求，您可以選擇連接儲存在標準儲存體且一個磁碟最多具有 500 IO/ps 的磁碟，或進階儲存體且一個磁碟最多具有 5000 IO/ps 的磁碟。</span><span class="sxs-lookup"><span data-stu-id="3b5df-109">Based on your IO needs, you can choose to attach disks that are stored in our Standard Storage, with up to 500 IO/ps per disk or our Premium storage with up to 5000 IO/ps per disk.</span></span> <span data-ttu-id="3b5df-110">本文不會詳細說明如何佈建資料磁碟以及將其連接至 Linux 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="3b5df-110">This article does not go into detail on how to provision and attach data disks to a Linux virtual machine.</span></span>  <span data-ttu-id="3b5df-111">請參閱 Microsoft Azure 文章[連接磁碟](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)，取得如何在 Azure 上將空白資料磁碟連接至 Linux 虛擬機器的詳細指示。</span><span class="sxs-lookup"><span data-stu-id="3b5df-111">See the Microsoft Azure article [attach a disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for detailed instructions on how to attach an empty data disk to a Linux virtual machine on Azure.</span></span>

## <a name="install-the-mdadm-utility"></a><span data-ttu-id="3b5df-112">安裝 mdadm 公用程式</span><span class="sxs-lookup"><span data-stu-id="3b5df-112">Install the mdadm utility</span></span>
* <span data-ttu-id="3b5df-113">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="3b5df-113">**Ubuntu**</span></span>
```bash
sudo apt-get update
sudo apt-get install mdadm
```

* <span data-ttu-id="3b5df-114">**CentOS & Oracle Linux**</span><span class="sxs-lookup"><span data-stu-id="3b5df-114">**CentOS & Oracle Linux**</span></span>
```bash
sudo yum install mdadm
```

* <span data-ttu-id="3b5df-115">**SLES 和 openSUSE**</span><span class="sxs-lookup"><span data-stu-id="3b5df-115">**SLES and openSUSE**</span></span>
```bash  
zypper install mdadm
```

## <a name="create-the-disk-partitions"></a><span data-ttu-id="3b5df-116">建立磁碟分割</span><span class="sxs-lookup"><span data-stu-id="3b5df-116">Create the disk partitions</span></span>
<span data-ttu-id="3b5df-117">在本範例中，我們會在 /dev/sdc 上建立單一磁碟分割。</span><span class="sxs-lookup"><span data-stu-id="3b5df-117">In this example, we create a single disk partition on /dev/sdc.</span></span> <span data-ttu-id="3b5df-118">新磁碟分割的名稱會是 /dev/sdc1。</span><span class="sxs-lookup"><span data-stu-id="3b5df-118">The new disk partition will be called /dev/sdc1.</span></span>

1. <span data-ttu-id="3b5df-119">啟動 `fdisk` 開始建立磁碟分割</span><span class="sxs-lookup"><span data-stu-id="3b5df-119">Start `fdisk` to begin creating partitions</span></span>

    ```bash
    sudo fdisk /dev/sdc
    Device contains neither a valid DOS partition table, nor Sun, SGI or OSF disklabel
    Building a new DOS disklabel with disk identifier 0xa34cb70c.
    Changes will remain in memory only, until you decide to write them.
    After that, of course, the previous content won't be recoverable.

    WARNING: DOS-compatible mode is deprecated. It's strongly recommended to
                    switch off the mode (command 'c') and change display units to
                    sectors (command 'u').
    ```

2. <span data-ttu-id="3b5df-120">按下 'n' 個提示字元來建立在 **n**新增磁碟分割：</span><span class="sxs-lookup"><span data-stu-id="3b5df-120">Press 'n' at the prompt to create a **n**ew partition:</span></span>

    ```bash
    Command (m for help): n
    ```

3. <span data-ttu-id="3b5df-121">接著，請按 'p' 以建立 **主要**磁碟分割：</span><span class="sxs-lookup"><span data-stu-id="3b5df-121">Next, press 'p' to create a **p**rimary partition:</span></span>

    ```bash 
    Command action
            e   extended
            p   primary partition (1-4)
    ```

4. <span data-ttu-id="3b5df-122">按 '1' 以選取磁碟分割編號 1：</span><span class="sxs-lookup"><span data-stu-id="3b5df-122">Press '1' to select partition number 1:</span></span>

    ```bash
    Partition number (1-4): 1
    ```

5. <span data-ttu-id="3b5df-123">選取新磁碟分割的起始點，或按 `<enter>` 接受預設值，將磁碟分割置於磁碟機上可用空間的開始位置：</span><span class="sxs-lookup"><span data-stu-id="3b5df-123">Select the starting point of the new partition, or press `<enter>` to accept the default to place the partition at the beginning of the free space on the drive:</span></span>

    ```bash   
    First cylinder (1-1305, default 1):
    Using default value 1
    ```

6. <span data-ttu-id="3b5df-124">選取磁碟分割的大小，例如，輸入 '+10G' 以建立 10 GB 的磁碟分割。</span><span class="sxs-lookup"><span data-stu-id="3b5df-124">Select the size of the partition, for example type '+10G' to create a 10 gigabyte partition.</span></span> <span data-ttu-id="3b5df-125">或者，按 `<enter>` 建立跨越整個磁碟機的單一磁碟分割：</span><span class="sxs-lookup"><span data-stu-id="3b5df-125">Or, press `<enter>` create a single partition that spans the entire drive:</span></span>

    ```bash   
    Last cylinder, +cylinders or +size{K,M,G} (1-1305, default 1305): 
    Using default value 1305
    ```

7. <span data-ttu-id="3b5df-126">接著，將磁碟分割的 ID 和類型 ( **t**) 從預設的 ID '83' (Linux) 變更為 ID 'fd' (Linux raid auto)：</span><span class="sxs-lookup"><span data-stu-id="3b5df-126">Next, change the ID and **t**ype of the partition from the default ID '83' (Linux) to ID 'fd' (Linux raid auto):</span></span>

    ```bash  
    Command (m for help): t
    Selected partition 1
    Hex code (type L to list codes): fd
    ```

8. <span data-ttu-id="3b5df-127">最後，將磁碟分割資料表寫入磁碟機並結束 fdisk：</span><span class="sxs-lookup"><span data-stu-id="3b5df-127">Finally, write the partition table to the drive and exit fdisk:</span></span>

    ```bash   
    Command (m for help): w
    The partition table has been altered!
    ```

## <a name="create-the-raid-array"></a><span data-ttu-id="3b5df-128">建立 RAID 陣列</span><span class="sxs-lookup"><span data-stu-id="3b5df-128">Create the RAID array</span></span>
1. <span data-ttu-id="3b5df-129">下列範例將「分割」(RAID 層級 0) 位於三個不同資料磁碟 (sdc1、sdd1、sde1) 的三個磁碟分割。</span><span class="sxs-lookup"><span data-stu-id="3b5df-129">The following example will "stripe" (RAID level 0) three partitions located on three separate data disks (sdc1, sdd1, sde1).</span></span>  <span data-ttu-id="3b5df-130">執行此命令之後，即會建立一個名為 **/dev/md127** 的新 RAID 裝置。</span><span class="sxs-lookup"><span data-stu-id="3b5df-130">After running this command a new RAID device called **/dev/md127** is created.</span></span> <span data-ttu-id="3b5df-131">同時請注意，如果這些資料磁碟先前是另一個無用 RAID 陣列的一部分，則您可能需要在 `mdadm` 命令中加上 `--force` 參數：</span><span class="sxs-lookup"><span data-stu-id="3b5df-131">Also note that if these data disks we previously part of another defunct RAID array it may be necessary to add the `--force` parameter to the `mdadm` command:</span></span>

    ```bash  
    sudo mdadm --create /dev/md127 --level 0 --raid-devices 3 \
        /dev/sdc1 /dev/sdd1 /dev/sde1
    ```

2. <span data-ttu-id="3b5df-132">在新的 RAID 裝置上建立檔案系統</span><span class="sxs-lookup"><span data-stu-id="3b5df-132">Create the file system on the new RAID device</span></span>
   
    <span data-ttu-id="3b5df-133">a.</span><span class="sxs-lookup"><span data-stu-id="3b5df-133">a.</span></span> <span data-ttu-id="3b5df-134">**CentOS、Oracle Linux、SLES 12、openSUSE 和 Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="3b5df-134">**CentOS, Oracle Linux, SLES 12, openSUSE, and Ubuntu**</span></span>

    ```bash   
    sudo mkfs -t ext4 /dev/md127
    ```
   
    <span data-ttu-id="3b5df-135">b.</span><span class="sxs-lookup"><span data-stu-id="3b5df-135">b.</span></span> <span data-ttu-id="3b5df-136">**SLES 11**</span><span class="sxs-lookup"><span data-stu-id="3b5df-136">**SLES 11**</span></span>

    ```bash
    sudo mkfs -t ext3 /dev/md127
    ```
   
    <span data-ttu-id="3b5df-137">c.</span><span class="sxs-lookup"><span data-stu-id="3b5df-137">c.</span></span> <span data-ttu-id="3b5df-138">**SLES 11** - 啟用 boot.md 並建立 mdadm.conf</span><span class="sxs-lookup"><span data-stu-id="3b5df-138">**SLES 11** - enable boot.md and create mdadm.conf</span></span>

    ```bash
    sudo -i chkconfig --add boot.md
    sudo echo 'DEVICE /dev/sd*[0-9]' >> /etc/mdadm.conf
    ```
   
   > [!NOTE]
   > <span data-ttu-id="3b5df-139">在 SUSE 系統上進行這些變更之後，可能需要重新開機。</span><span class="sxs-lookup"><span data-stu-id="3b5df-139">A reboot may be required after making these changes on SUSE systems.</span></span> <span data-ttu-id="3b5df-140">針對 SLES 12，這在並 *非* 必要步驟。</span><span class="sxs-lookup"><span data-stu-id="3b5df-140">This step is *not* required on SLES 12.</span></span>
   > 
   > 

## <a name="add-the-new-file-system-to-etcfstab"></a><span data-ttu-id="3b5df-141">將新的檔案系統新增至 /etc/fstab</span><span class="sxs-lookup"><span data-stu-id="3b5df-141">Add the new file system to /etc/fstab</span></span>
> [!IMPORTANT]
> <span data-ttu-id="3b5df-142">不當編輯 /etc/fstab 檔案會導致系統無法開機。</span><span class="sxs-lookup"><span data-stu-id="3b5df-142">Improperly editing the /etc/fstab file could result in an unbootable system.</span></span> <span data-ttu-id="3b5df-143">如果不確定，請參閱散發套件的文件，以取得如何適當編輯此檔案的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="3b5df-143">If unsure, refer to the distribution's documentation for information on how to properly edit this file.</span></span> <span data-ttu-id="3b5df-144">在編輯之前，也建議先備份 /etc/fstab 檔案。</span><span class="sxs-lookup"><span data-stu-id="3b5df-144">It is also recommended that a backup of the /etc/fstab file is created before editing.</span></span>

1. <span data-ttu-id="3b5df-145">建立新檔案系統所需的掛接點，例如：</span><span class="sxs-lookup"><span data-stu-id="3b5df-145">Create the desired mount point for your new file system, for example:</span></span>

    ```bash
    sudo mkdir /data
    ```
2. <span data-ttu-id="3b5df-146">編輯 /etc/fstab 時，應使用 **UUID** (而非使用裝置名稱) 來參考檔案系統。</span><span class="sxs-lookup"><span data-stu-id="3b5df-146">When editing /etc/fstab, the **UUID** should be used to reference the file system rather than the device name.</span></span>  <span data-ttu-id="3b5df-147">使用 `blkid` 公用程式來決定新檔案系統的 UUID：</span><span class="sxs-lookup"><span data-stu-id="3b5df-147">Use the `blkid` utility to determine the UUID for the new file system:</span></span>

    ```bash   
    sudo /sbin/blkid
    ...........
    /dev/md127: UUID="aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee" TYPE="ext4"
    ```

3. <span data-ttu-id="3b5df-148">在文字編輯器中開啟 /etc/fstab，並為新檔案系統新增項目，例如：</span><span class="sxs-lookup"><span data-stu-id="3b5df-148">Open /etc/fstab in a text editor and add an entry for the new file system, for example:</span></span>

    ```bash   
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults  0  2
    ```
   
    <span data-ttu-id="3b5df-149">或者，在 **SLES 11** 上：</span><span class="sxs-lookup"><span data-stu-id="3b5df-149">Or on **SLES 11**:</span></span>

    ```bash
    /dev/disk/by-uuid/aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext3  defaults  0  2
    ```
   
    <span data-ttu-id="3b5df-150">接著，儲存並關閉 /etc/fstab。</span><span class="sxs-lookup"><span data-stu-id="3b5df-150">Then, save and close /etc/fstab.</span></span>

4. <span data-ttu-id="3b5df-151">測試 /etc/fstab 項目是否正確：</span><span class="sxs-lookup"><span data-stu-id="3b5df-151">Test that the /etc/fstab entry is correct:</span></span>

    ```bash  
    sudo mount -a
    ```

    <span data-ttu-id="3b5df-152">如果此命令會產生錯誤訊息，請檢查 /etc/fstab 檔案中的語法。</span><span class="sxs-lookup"><span data-stu-id="3b5df-152">If this command results in an error message, please check the syntax in the /etc/fstab file.</span></span>
   
    <span data-ttu-id="3b5df-153">接下來，執行 `mount` 命令，以確保已掛接檔案系統：</span><span class="sxs-lookup"><span data-stu-id="3b5df-153">Next run the `mount` command to ensure the file system is mounted:</span></span>

    ```bash   
    mount
    .................
    /dev/md127 on /data type ext4 (rw)
    ```

5. <span data-ttu-id="3b5df-154">(選擇性) 保全開機參數</span><span class="sxs-lookup"><span data-stu-id="3b5df-154">(Optional) Failsafe Boot Parameters</span></span>
   
    <span data-ttu-id="3b5df-155">**fstab 組態**</span><span class="sxs-lookup"><span data-stu-id="3b5df-155">**fstab configuration**</span></span>
   
    <span data-ttu-id="3b5df-156">許多散發套件包含 `nobootwait` 或 `nofail` 掛接參數，可加入至 /etc/fstab 檔案。</span><span class="sxs-lookup"><span data-stu-id="3b5df-156">Many distributions include either the `nobootwait` or `nofail` mount parameters that may be added to the /etc/fstab file.</span></span> <span data-ttu-id="3b5df-157">這些參數容許發生掛接特定檔案系統失敗，並容許 Linux 系統繼續開機，即使它無法正確地掛接 RAID 檔案系統。</span><span class="sxs-lookup"><span data-stu-id="3b5df-157">These parameters allow for failures when mounting a particular file system and allow the Linux system to continue to boot even if it is unable to properly mount the RAID file system.</span></span> <span data-ttu-id="3b5df-158">請參閱散發套件的文件，以取得這些參數的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="3b5df-158">Refer to your distribution's documentation for more information on these parameters.</span></span>
   
    <span data-ttu-id="3b5df-159">範例 (Ubuntu)：</span><span class="sxs-lookup"><span data-stu-id="3b5df-159">Example (Ubuntu):</span></span>

    ```bash  
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults,nobootwait  0  2
    ```   

    <span data-ttu-id="3b5df-160">**Linux 開機參數**</span><span class="sxs-lookup"><span data-stu-id="3b5df-160">**Linux boot parameters**</span></span>
   
    <span data-ttu-id="3b5df-161">除了上述參數之外，即使 RAID 看起來已損壞或效能不佳，核心參數 "`bootdegraded=true`" 仍可讓系統開機，例如，將資料磁碟機從虛擬機器中不當移除。</span><span class="sxs-lookup"><span data-stu-id="3b5df-161">In addition to the above parameters, the kernel parameter "`bootdegraded=true`" can allow the system to boot even if the RAID is perceived as damaged or degraded, for example if a data drive is inadvertently removed from the virtual machine.</span></span> <span data-ttu-id="3b5df-162">依預設，這也會造成無法開機的系統。</span><span class="sxs-lookup"><span data-stu-id="3b5df-162">By default this could also result in a non-bootable system.</span></span>
   
    <span data-ttu-id="3b5df-163">請參閱散發套件的文件，以取得如何正確編輯核心參數的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="3b5df-163">Please refer to your distribution's documentation on how to properly edit kernel parameters.</span></span> <span data-ttu-id="3b5df-164">例如，在許多散發套件 (CentOS、Oracle Linux、SLES 11) 中，可手動將這些參數加入至 "`/boot/grub/menu.lst`" 檔案。</span><span class="sxs-lookup"><span data-stu-id="3b5df-164">For example, in many distributions (CentOS, Oracle Linux, SLES 11) these parameters may be added manually to the "`/boot/grub/menu.lst`" file.</span></span>  <span data-ttu-id="3b5df-165">在 Ubuntu 上，可將此參數加入至 "/etc/default/grub" 上的 `GRUB_CMDLINE_LINUX_DEFAULT` 變數。</span><span class="sxs-lookup"><span data-stu-id="3b5df-165">On Ubuntu this parameter can be added to the `GRUB_CMDLINE_LINUX_DEFAULT` variable on "/etc/default/grub".</span></span>


## <a name="trimunmap-support"></a><span data-ttu-id="3b5df-166">TRIM/UNMAP 支援</span><span class="sxs-lookup"><span data-stu-id="3b5df-166">TRIM/UNMAP support</span></span>
<span data-ttu-id="3b5df-167">有些 Linux 核心會支援 TRIM/UNMAP 作業以捨棄磁碟上未使用的區塊。</span><span class="sxs-lookup"><span data-stu-id="3b5df-167">Some Linux kernels support TRIM/UNMAP operations to discard unused blocks on the disk.</span></span> <span data-ttu-id="3b5df-168">這些作業主要是在標準儲存體中相當實用，可用來通知 Azure 已刪除的頁面已不再有效而可予以捨棄。</span><span class="sxs-lookup"><span data-stu-id="3b5df-168">These operations are primarily useful in standard storage to inform Azure that deleted pages are no longer valid and can be discarded.</span></span> <span data-ttu-id="3b5df-169">如果您建立大型檔案，然後再將它們刪除，捨棄頁面可以節省成本。</span><span class="sxs-lookup"><span data-stu-id="3b5df-169">Discarding pages can save cost if you create large files and then delete them.</span></span>

> [!NOTE]
> <span data-ttu-id="3b5df-170">如果陣列的區塊大小設定為小於預設值 (512KB)，則 RAID 可能不會發出捨棄命令。</span><span class="sxs-lookup"><span data-stu-id="3b5df-170">RAID may not issue discard commands if the chunk size for the array is set to less than the default (512KB).</span></span> <span data-ttu-id="3b5df-171">這是因為主機上的 unmap 細微度也是 512KB。</span><span class="sxs-lookup"><span data-stu-id="3b5df-171">This is because the unmap granularity on the Host is also 512KB.</span></span> <span data-ttu-id="3b5df-172">如果您透過 mdadm 的 `--chunk=` 參數修改陣列的區塊大小，則核心可能會忽略 TRIM/unmap 要求。</span><span class="sxs-lookup"><span data-stu-id="3b5df-172">If you modified the array's chunk size via mdadm's `--chunk=` parameter, then TRIM/unmap requests may be ignored by the kernel.</span></span>

<span data-ttu-id="3b5df-173">有兩種方式可在 Linux VM 中啟用 TRIM 支援。</span><span class="sxs-lookup"><span data-stu-id="3b5df-173">There are two ways to enable TRIM support in your Linux VM.</span></span> <span data-ttu-id="3b5df-174">像往常一樣，請參閱您的散發套件以了解建議的方法︰</span><span class="sxs-lookup"><span data-stu-id="3b5df-174">As usual, consult your distribution for the recommended approach:</span></span>

- <span data-ttu-id="3b5df-175">在 `/etc/fstab` 中使用 `discard` 掛接選項，例如：</span><span class="sxs-lookup"><span data-stu-id="3b5df-175">Use the `discard` mount option in `/etc/fstab`, for example:</span></span>

    ```bash
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults,discard  0  2
    ```

- <span data-ttu-id="3b5df-176">在某些情況下，`discard` 選項可能會影響效能。</span><span class="sxs-lookup"><span data-stu-id="3b5df-176">In some cases the `discard` option may have performance implications.</span></span> <span data-ttu-id="3b5df-177">或者，您也可以從命令列手動執行 `fstrim` 命令，或將它新增到 crontab 來定期執行︰</span><span class="sxs-lookup"><span data-stu-id="3b5df-177">Alternatively, you can run the `fstrim` command manually from the command line, or add it to your crontab to run regularly:</span></span>

    <span data-ttu-id="3b5df-178">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="3b5df-178">**Ubuntu**</span></span>

    ```bash
    # sudo apt-get install util-linux
    # sudo fstrim /data
    ```

    <span data-ttu-id="3b5df-179">**RHEL/CentOS**</span><span class="sxs-lookup"><span data-stu-id="3b5df-179">**RHEL/CentOS**</span></span>
    ```bash
    # sudo yum install util-linux
    # sudo fstrim /data
    ```
