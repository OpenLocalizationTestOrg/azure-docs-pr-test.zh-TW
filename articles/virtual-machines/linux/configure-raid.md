---
title: "aaaConfigure 軟體上執行 Linux 的虛擬機器的 RAID |Microsoft 文件"
description: "了解 toouse mdadm tooconfigure RAID 在 Azure 中 Linux 上的方式。"
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
ms.openlocfilehash: f06e2679d953faf88ffee9991226cdb3cc1cbdb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-software-raid-on-linux"></a><span data-ttu-id="48d26-103">在 Linux 上設定軟體 RAID</span><span class="sxs-lookup"><span data-stu-id="48d26-103">Configure Software RAID on Linux</span></span>
<span data-ttu-id="48d26-104">常見的案例 toouse 軟體 RAID Linux 虛擬機器上處於 Azure toopresent 多個連接的資料磁碟做為單一的 RAID 裝置。</span><span class="sxs-lookup"><span data-stu-id="48d26-104">It's a common scenario toouse software RAID on Linux virtual machines in Azure toopresent multiple attached data disks as a single RAID device.</span></span> <span data-ttu-id="48d26-105">通常這可以使用的 tooimprove 效能，以及允許針對改善輸送量比較 toousing 只有單一磁碟。</span><span class="sxs-lookup"><span data-stu-id="48d26-105">Typically this can be used tooimprove performance and allow for improved throughput compared toousing just a single disk.</span></span>

## <a name="attaching-data-disks"></a><span data-ttu-id="48d26-106">連接資料磁碟</span><span class="sxs-lookup"><span data-stu-id="48d26-106">Attaching data disks</span></span>
<span data-ttu-id="48d26-107">兩個或多個空的資料磁碟都需要的 tooconfigure RAID 裝置。</span><span class="sxs-lookup"><span data-stu-id="48d26-107">Two or more empty data disks are needed tooconfigure a RAID device.</span></span>  <span data-ttu-id="48d26-108">hello 建立 RAID 裝置的主要原因是磁碟的 tooimprove 效能 IO。</span><span class="sxs-lookup"><span data-stu-id="48d26-108">hello primary reason for creating a RAID device is tooimprove performance of your disk IO.</span></span>  <span data-ttu-id="48d26-109">根據您的 IO 需求，您可以選擇儲存在我們的標準儲存體，與總 too500 IO/每個磁碟或使用向上 too5000 IO/每個磁碟 ps 我們高階儲存體 ps tooattach 磁碟。</span><span class="sxs-lookup"><span data-stu-id="48d26-109">Based on your IO needs, you can choose tooattach disks that are stored in our Standard Storage, with up too500 IO/ps per disk or our Premium storage with up too5000 IO/ps per disk.</span></span> <span data-ttu-id="48d26-110">這篇文章不會深入說明如何 tooprovision 和附加資料磁碟 tooa Linux 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="48d26-110">This article does not go into detail on how tooprovision and attach data disks tooa Linux virtual machine.</span></span>  <span data-ttu-id="48d26-111">請參閱 hello Microsoft Azure 文件[連接磁碟](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)如需有關如何 tooattach 空的資料磁碟在 Azure 上 tooa Linux 虛擬機器的詳細指示。</span><span class="sxs-lookup"><span data-stu-id="48d26-111">See hello Microsoft Azure article [attach a disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for detailed instructions on how tooattach an empty data disk tooa Linux virtual machine on Azure.</span></span>

## <a name="install-hello-mdadm-utility"></a><span data-ttu-id="48d26-112">安裝 hello mdadm 公用程式</span><span class="sxs-lookup"><span data-stu-id="48d26-112">Install hello mdadm utility</span></span>
* <span data-ttu-id="48d26-113">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="48d26-113">**Ubuntu**</span></span>
```bash
sudo apt-get update
sudo apt-get install mdadm
```

* <span data-ttu-id="48d26-114">**CentOS & Oracle Linux**</span><span class="sxs-lookup"><span data-stu-id="48d26-114">**CentOS & Oracle Linux**</span></span>
```bash
sudo yum install mdadm
```

* <span data-ttu-id="48d26-115">**SLES 和 openSUSE**</span><span class="sxs-lookup"><span data-stu-id="48d26-115">**SLES and openSUSE**</span></span>
```bash  
zypper install mdadm
```

## <a name="create-hello-disk-partitions"></a><span data-ttu-id="48d26-116">建立 hello 磁碟分割</span><span class="sxs-lookup"><span data-stu-id="48d26-116">Create hello disk partitions</span></span>
<span data-ttu-id="48d26-117">在本範例中，我們會在 /dev/sdc 上建立單一磁碟分割。</span><span class="sxs-lookup"><span data-stu-id="48d26-117">In this example, we create a single disk partition on /dev/sdc.</span></span> <span data-ttu-id="48d26-118">會呼叫 /dev/sdc1 hello 新磁碟分割。</span><span class="sxs-lookup"><span data-stu-id="48d26-118">hello new disk partition will be called /dev/sdc1.</span></span>

1. <span data-ttu-id="48d26-119">啟動`fdisk`toobegin 建立資料分割</span><span class="sxs-lookup"><span data-stu-id="48d26-119">Start `fdisk` toobegin creating partitions</span></span>

    ```bash
    sudo fdisk /dev/sdc
    Device contains neither a valid DOS partition table, nor Sun, SGI or OSF disklabel
    Building a new DOS disklabel with disk identifier 0xa34cb70c.
    Changes will remain in memory only, until you decide toowrite them.
    After that, of course, hello previous content won't be recoverable.

    WARNING: DOS-compatible mode is deprecated. It's strongly recommended to
                    switch off hello mode (command 'c') and change display units to
                    sectors (command 'u').
    ```

2. <span data-ttu-id="48d26-120">按下 'n' 個在 hello 提示 toocreate  **n**新增磁碟分割：</span><span class="sxs-lookup"><span data-stu-id="48d26-120">Press 'n' at hello prompt toocreate a **n**ew partition:</span></span>

    ```bash
    Command (m for help): n
    ```

3. <span data-ttu-id="48d26-121">接下來，請按 'p' toocreate **p**主要磁碟分割：</span><span class="sxs-lookup"><span data-stu-id="48d26-121">Next, press 'p' toocreate a **p**rimary partition:</span></span>

    ```bash 
    Command action
            e   extended
            p   primary partition (1-4)
    ```

4. <span data-ttu-id="48d26-122">按下 '1' tooselect 資料分割編號 1:</span><span class="sxs-lookup"><span data-stu-id="48d26-122">Press '1' tooselect partition number 1:</span></span>

    ```bash
    Partition number (1-4): 1
    ```

5. <span data-ttu-id="48d26-123">選取 hello 起點 hello 新磁碟分割或按`<enter>`tooaccept hello 預設 tooplace hello 資料分割的 hello hello 磁碟機上的可用空間 hello 開頭：</span><span class="sxs-lookup"><span data-stu-id="48d26-123">Select hello starting point of hello new partition, or press `<enter>` tooaccept hello default tooplace hello partition at hello beginning of hello free space on hello drive:</span></span>

    ```bash   
    First cylinder (1-1305, default 1):
    Using default value 1
    ```

6. <span data-ttu-id="48d26-124">選取 hello hello 分割區，例如型別 '+10G' toocreate 10 gb 的磁碟分割大小。</span><span class="sxs-lookup"><span data-stu-id="48d26-124">Select hello size of hello partition, for example type '+10G' toocreate a 10 gigabyte partition.</span></span> <span data-ttu-id="48d26-125">或者，按下`<enter>`建立單一磁碟分割跨越 hello 整個磁碟機的：</span><span class="sxs-lookup"><span data-stu-id="48d26-125">Or, press `<enter>` create a single partition that spans hello entire drive:</span></span>

    ```bash   
    Last cylinder, +cylinders or +size{K,M,G} (1-1305, default 1305): 
    Using default value 1305
    ```

7. <span data-ttu-id="48d26-126">接下來，變更 hello 識別碼和**t**hello hello 預設值的資料分割的類型識別碼 '83' (Linux) tooID 'fd' （Linux raid 自動）：</span><span class="sxs-lookup"><span data-stu-id="48d26-126">Next, change hello ID and **t**ype of hello partition from hello default ID '83' (Linux) tooID 'fd' (Linux raid auto):</span></span>

    ```bash  
    Command (m for help): t
    Selected partition 1
    Hex code (type L toolist codes): fd
    ```

8. <span data-ttu-id="48d26-127">最後，撰寫 hello 資料分割資料表 toohello 磁碟機，並結束 fdisk:</span><span class="sxs-lookup"><span data-stu-id="48d26-127">Finally, write hello partition table toohello drive and exit fdisk:</span></span>

    ```bash   
    Command (m for help): w
    hello partition table has been altered!
    ```

## <a name="create-hello-raid-array"></a><span data-ttu-id="48d26-128">建立 hello RAID 陣列</span><span class="sxs-lookup"><span data-stu-id="48d26-128">Create hello RAID array</span></span>
1. <span data-ttu-id="48d26-129">下列範例將"等量磁碟區 」 （RAID 層級 0） 三個資料分割位於三個不同的資料磁碟 （sdc1、 sdd1、 sde1） hello。</span><span class="sxs-lookup"><span data-stu-id="48d26-129">hello following example will "stripe" (RAID level 0) three partitions located on three separate data disks (sdc1, sdd1, sde1).</span></span>  <span data-ttu-id="48d26-130">執行此命令之後，即會建立一個名為 **/dev/md127** 的新 RAID 裝置。</span><span class="sxs-lookup"><span data-stu-id="48d26-130">After running this command a new RAID device called **/dev/md127** is created.</span></span> <span data-ttu-id="48d26-131">也請注意，是否這些資料磁碟我們先前屬於另一個無用的 RAID 陣列可能需要 tooadd hello`--force`參數 toohello`mdadm`命令：</span><span class="sxs-lookup"><span data-stu-id="48d26-131">Also note that if these data disks we previously part of another defunct RAID array it may be necessary tooadd hello `--force` parameter toohello `mdadm` command:</span></span>

    ```bash  
    sudo mdadm --create /dev/md127 --level 0 --raid-devices 3 \
        /dev/sdc1 /dev/sdd1 /dev/sde1
    ```

2. <span data-ttu-id="48d26-132">在 hello 新 RAID 裝置上建立 hello 檔案系統</span><span class="sxs-lookup"><span data-stu-id="48d26-132">Create hello file system on hello new RAID device</span></span>
   
    <span data-ttu-id="48d26-133">a.</span><span class="sxs-lookup"><span data-stu-id="48d26-133">a.</span></span> <span data-ttu-id="48d26-134">**CentOS、Oracle Linux、SLES 12、openSUSE 和 Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="48d26-134">**CentOS, Oracle Linux, SLES 12, openSUSE, and Ubuntu**</span></span>

    ```bash   
    sudo mkfs -t ext4 /dev/md127
    ```
   
    <span data-ttu-id="48d26-135">b.</span><span class="sxs-lookup"><span data-stu-id="48d26-135">b.</span></span> <span data-ttu-id="48d26-136">**SLES 11**</span><span class="sxs-lookup"><span data-stu-id="48d26-136">**SLES 11**</span></span>

    ```bash
    sudo mkfs -t ext3 /dev/md127
    ```
   
    <span data-ttu-id="48d26-137">c.</span><span class="sxs-lookup"><span data-stu-id="48d26-137">c.</span></span> <span data-ttu-id="48d26-138">**SLES 11** - 啟用 boot.md 並建立 mdadm.conf</span><span class="sxs-lookup"><span data-stu-id="48d26-138">**SLES 11** - enable boot.md and create mdadm.conf</span></span>

    ```bash
    sudo -i chkconfig --add boot.md
    sudo echo 'DEVICE /dev/sd*[0-9]' >> /etc/mdadm.conf
    ```
   
   > [!NOTE]
   > <span data-ttu-id="48d26-139">在 SUSE 系統上進行這些變更之後，可能需要重新開機。</span><span class="sxs-lookup"><span data-stu-id="48d26-139">A reboot may be required after making these changes on SUSE systems.</span></span> <span data-ttu-id="48d26-140">針對 SLES 12，這在並 *非* 必要步驟。</span><span class="sxs-lookup"><span data-stu-id="48d26-140">This step is *not* required on SLES 12.</span></span>
   > 
   > 

## <a name="add-hello-new-file-system-tooetcfstab"></a><span data-ttu-id="48d26-141">新增 hello 新檔案系統太/等/fstab</span><span class="sxs-lookup"><span data-stu-id="48d26-141">Add hello new file system too/etc/fstab</span></span>
> [!IMPORTANT]
> <span data-ttu-id="48d26-142">不當編輯 hello /etc/fstab 檔案可能會導致系統無法重新啟動。</span><span class="sxs-lookup"><span data-stu-id="48d26-142">Improperly editing hello /etc/fstab file could result in an unbootable system.</span></span> <span data-ttu-id="48d26-143">如果不確定，請參閱 toohello 發佈文件，以取得 tooproperly 如何編輯此檔案的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="48d26-143">If unsure, refer toohello distribution's documentation for information on how tooproperly edit this file.</span></span> <span data-ttu-id="48d26-144">也建議在編輯之前建立的 hello /etc/fstab 檔案的備份。</span><span class="sxs-lookup"><span data-stu-id="48d26-144">It is also recommended that a backup of hello /etc/fstab file is created before editing.</span></span>

1. <span data-ttu-id="48d26-145">建立新的檔案系統，所需的 hello 掛接點，例如：</span><span class="sxs-lookup"><span data-stu-id="48d26-145">Create hello desired mount point for your new file system, for example:</span></span>

    ```bash
    sudo mkdir /data
    ```
2. <span data-ttu-id="48d26-146">當編輯 /etc/fstab，hello **UUID**應使用的 tooreference hello 檔案系統，而不是 hello 裝置名稱。</span><span class="sxs-lookup"><span data-stu-id="48d26-146">When editing /etc/fstab, hello **UUID** should be used tooreference hello file system rather than hello device name.</span></span>  <span data-ttu-id="48d26-147">使用 hello `blkid` hello 新的檔案系統的公用程式 toodetermine hello UUID:</span><span class="sxs-lookup"><span data-stu-id="48d26-147">Use hello `blkid` utility toodetermine hello UUID for hello new file system:</span></span>

    ```bash   
    sudo /sbin/blkid
    ...........
    /dev/md127: UUID="aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee" TYPE="ext4"
    ```

3. <span data-ttu-id="48d26-148">在文字編輯器中開啟 /etc/fstab 並新增 hello 新的檔案系統的項目，例如：</span><span class="sxs-lookup"><span data-stu-id="48d26-148">Open /etc/fstab in a text editor and add an entry for hello new file system, for example:</span></span>

    ```bash   
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults  0  2
    ```
   
    <span data-ttu-id="48d26-149">或者，在 **SLES 11** 上：</span><span class="sxs-lookup"><span data-stu-id="48d26-149">Or on **SLES 11**:</span></span>

    ```bash
    /dev/disk/by-uuid/aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext3  defaults  0  2
    ```
   
    <span data-ttu-id="48d26-150">接著，儲存並關閉 /etc/fstab。</span><span class="sxs-lookup"><span data-stu-id="48d26-150">Then, save and close /etc/fstab.</span></span>

4. <span data-ttu-id="48d26-151">測試該 hello /etc/fstab 輸入正確：</span><span class="sxs-lookup"><span data-stu-id="48d26-151">Test that hello /etc/fstab entry is correct:</span></span>

    ```bash  
    sudo mount -a
    ```

    <span data-ttu-id="48d26-152">如果此命令會產生錯誤訊息中，請檢查 hello /etc/fstab 檔案中的 hello 語法。</span><span class="sxs-lookup"><span data-stu-id="48d26-152">If this command results in an error message, please check hello syntax in hello /etc/fstab file.</span></span>
   
    <span data-ttu-id="48d26-153">接下來執行 hello`mount`命令 tooensure hello 檔案系統已裝載：</span><span class="sxs-lookup"><span data-stu-id="48d26-153">Next run hello `mount` command tooensure hello file system is mounted:</span></span>

    ```bash   
    mount
    .................
    /dev/md127 on /data type ext4 (rw)
    ```

5. <span data-ttu-id="48d26-154">(選擇性) 保全開機參數</span><span class="sxs-lookup"><span data-stu-id="48d26-154">(Optional) Failsafe Boot Parameters</span></span>
   
    <span data-ttu-id="48d26-155">**fstab 組態**</span><span class="sxs-lookup"><span data-stu-id="48d26-155">**fstab configuration**</span></span>
   
    <span data-ttu-id="48d26-156">許多發行包含任一 hello`nobootwait`或`nofail`掛接參數可能會加入 toohello /etc/hosts fstab 檔案。</span><span class="sxs-lookup"><span data-stu-id="48d26-156">Many distributions include either hello `nobootwait` or `nofail` mount parameters that may be added toohello /etc/fstab file.</span></span> <span data-ttu-id="48d26-157">這些參數時掛接特定檔案系統允許的失敗，並允許 hello Linux 系統 toocontinue tooboot，即使它是無法 tooproperly 掛接 hello RAID 檔案系統。</span><span class="sxs-lookup"><span data-stu-id="48d26-157">These parameters allow for failures when mounting a particular file system and allow hello Linux system toocontinue tooboot even if it is unable tooproperly mount hello RAID file system.</span></span> <span data-ttu-id="48d26-158">如需這些參數的詳細資訊，請參閱 tooyour 發佈文件。</span><span class="sxs-lookup"><span data-stu-id="48d26-158">Refer tooyour distribution's documentation for more information on these parameters.</span></span>
   
    <span data-ttu-id="48d26-159">範例 (Ubuntu)：</span><span class="sxs-lookup"><span data-stu-id="48d26-159">Example (Ubuntu):</span></span>

    ```bash  
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults,nobootwait  0  2
    ```   

    <span data-ttu-id="48d26-160">**Linux 開機參數**</span><span class="sxs-lookup"><span data-stu-id="48d26-160">**Linux boot parameters**</span></span>
   
    <span data-ttu-id="48d26-161">加法 toohello 上述參數，在 hello 核心參數 」`bootdegraded=true`」 可以讓 hello 系統 tooboot，即使 hello RAID 會被視為已損毀，或降級，例如，如果不小心從 hello 虛擬機器移除資料磁碟機。</span><span class="sxs-lookup"><span data-stu-id="48d26-161">In addition toohello above parameters, hello kernel parameter "`bootdegraded=true`" can allow hello system tooboot even if hello RAID is perceived as damaged or degraded, for example if a data drive is inadvertently removed from hello virtual machine.</span></span> <span data-ttu-id="48d26-162">依預設，這也會造成無法開機的系統。</span><span class="sxs-lookup"><span data-stu-id="48d26-162">By default this could also result in a non-bootable system.</span></span>
   
    <span data-ttu-id="48d26-163">請參閱上 tooproperly 如何編輯核心參數 tooyour 發佈文件。</span><span class="sxs-lookup"><span data-stu-id="48d26-163">Please refer tooyour distribution's documentation on how tooproperly edit kernel parameters.</span></span> <span data-ttu-id="48d26-164">比方說，在 CentOS、 Oracle Linux （SLES 11） 的許多發行這些參數可能加入手動 toohello"`/boot/grub/menu.lst`"檔案。</span><span class="sxs-lookup"><span data-stu-id="48d26-164">For example, in many distributions (CentOS, Oracle Linux, SLES 11) these parameters may be added manually toohello "`/boot/grub/menu.lst`" file.</span></span>  <span data-ttu-id="48d26-165">在 Ubuntu 上這個參數可以加入 toohello`GRUB_CMDLINE_LINUX_DEFAULT`變數上"/ 等/預設/幼蟲"。</span><span class="sxs-lookup"><span data-stu-id="48d26-165">On Ubuntu this parameter can be added toohello `GRUB_CMDLINE_LINUX_DEFAULT` variable on "/etc/default/grub".</span></span>


## <a name="trimunmap-support"></a><span data-ttu-id="48d26-166">TRIM/UNMAP 支援</span><span class="sxs-lookup"><span data-stu-id="48d26-166">TRIM/UNMAP support</span></span>
<span data-ttu-id="48d26-167">某些 Linux 核心支援 TRIM/UNMAP 作業 toodiscard hello 磁碟上未使用的區塊。</span><span class="sxs-lookup"><span data-stu-id="48d26-167">Some Linux kernels support TRIM/UNMAP operations toodiscard unused blocks on hello disk.</span></span> <span data-ttu-id="48d26-168">這些運算全都是主要適用於標準儲存體 tooinform 刪除頁面的 Azure 不再有效，以及可以捨棄。</span><span class="sxs-lookup"><span data-stu-id="48d26-168">These operations are primarily useful in standard storage tooinform Azure that deleted pages are no longer valid and can be discarded.</span></span> <span data-ttu-id="48d26-169">如果您建立大型檔案，然後再將它們刪除，捨棄頁面可以節省成本。</span><span class="sxs-lookup"><span data-stu-id="48d26-169">Discarding pages can save cost if you create large files and then delete them.</span></span>

> [!NOTE]
> <span data-ttu-id="48d26-170">如果 hello 陣列 hello 區塊大小設定 tooless hello 預設 (512 KB) 比 RAID 可能不會發出捨棄命令。</span><span class="sxs-lookup"><span data-stu-id="48d26-170">RAID may not issue discard commands if hello chunk size for hello array is set tooless than hello default (512KB).</span></span> <span data-ttu-id="48d26-171">這是因為 hello 取消對應 hello 主機上的資料粒度也是 512 KB。</span><span class="sxs-lookup"><span data-stu-id="48d26-171">This is because hello unmap granularity on hello Host is also 512KB.</span></span> <span data-ttu-id="48d26-172">如果您修改透過 mdadm 的 hello 陣列的區塊大小`--chunk=`hello 核心，則可能會忽略參數，則 TRIM/取消要求。</span><span class="sxs-lookup"><span data-stu-id="48d26-172">If you modified hello array's chunk size via mdadm's `--chunk=` parameter, then TRIM/unmap requests may be ignored by hello kernel.</span></span>

<span data-ttu-id="48d26-173">有兩種 tooenable TRIM 支援在 Linux VM 中。</span><span class="sxs-lookup"><span data-stu-id="48d26-173">There are two ways tooenable TRIM support in your Linux VM.</span></span> <span data-ttu-id="48d26-174">像往常一樣，參閱您的發佈 hello 建議的方法包括：</span><span class="sxs-lookup"><span data-stu-id="48d26-174">As usual, consult your distribution for hello recommended approach:</span></span>

- <span data-ttu-id="48d26-175">使用 hello`discard`掛接中的選項`/etc/fstab`，例如：</span><span class="sxs-lookup"><span data-stu-id="48d26-175">Use hello `discard` mount option in `/etc/fstab`, for example:</span></span>

    ```bash
    UUID=aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee  /data  ext4  defaults,discard  0  2
    ```

- <span data-ttu-id="48d26-176">在某些情況下 hello`discard`選項可能會影響效能。</span><span class="sxs-lookup"><span data-stu-id="48d26-176">In some cases hello `discard` option may have performance implications.</span></span> <span data-ttu-id="48d26-177">或者，您可以在其中執行 hello`fstrim`命令手動從 hello 命令列，或將它加入 tooyour crontab toorun 定期：</span><span class="sxs-lookup"><span data-stu-id="48d26-177">Alternatively, you can run hello `fstrim` command manually from hello command line, or add it tooyour crontab toorun regularly:</span></span>

    <span data-ttu-id="48d26-178">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="48d26-178">**Ubuntu**</span></span>

    ```bash
    # sudo apt-get install util-linux
    # sudo fstrim /data
    ```

    <span data-ttu-id="48d26-179">**RHEL/CentOS**</span><span class="sxs-lookup"><span data-stu-id="48d26-179">**RHEL/CentOS**</span></span>
    ```bash
    # sudo yum install util-linux
    # sudo fstrim /data
    ```
