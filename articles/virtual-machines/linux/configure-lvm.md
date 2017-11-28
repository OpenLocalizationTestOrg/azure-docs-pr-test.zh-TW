---
title: "在執行 Linux 的虛擬機器上的 aaaConfigure LVM |Microsoft 文件"
description: "深入了解如何在 Azure 中 Linux 上 LVM tooconfigure。"
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
ms.openlocfilehash: 8daf792d87c6bb3d91a2eddcd01cfab34fd28cff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-lvm-on-a-linux-vm-in-azure"></a><span data-ttu-id="a1328-103">設定 Azure 中 Linux VM 的 LVM</span><span class="sxs-lookup"><span data-stu-id="a1328-103">Configure LVM on a Linux VM in Azure</span></span>
<span data-ttu-id="a1328-104">本文將討論如何在 Azure 虛擬機器 tooconfigure 邏輯磁碟區管理員 (LVM)。</span><span class="sxs-lookup"><span data-stu-id="a1328-104">This document will discuss how tooconfigure Logical Volume Manager (LVM) in your Azure virtual machine.</span></span> <span data-ttu-id="a1328-105">雖然可行 tooconfigure LVM 的任何磁碟附加 toohello 虛擬機器，預設不會有映像的大部分雲端 LVM 上設定 hello 作業系統磁碟。</span><span class="sxs-lookup"><span data-stu-id="a1328-105">While it is feasible tooconfigure LVM on any disk attached toohello virtual machine, by default most cloud images will not have LVM configured on hello OS disk.</span></span> <span data-ttu-id="a1328-106">這是重複的磁碟區群組的 tooprevent 問題如果 hello 作業系統磁碟時附加 tooanother hello 的 VM 相同的分佈和類型，也就是在復原案例。</span><span class="sxs-lookup"><span data-stu-id="a1328-106">This is tooprevent problems with duplicate volume groups if hello OS disk is ever attached tooanother VM of hello same distribution and type, i.e. during a recovery scenario.</span></span> <span data-ttu-id="a1328-107">因此，建議您使用只 toouse LVM hello 資料磁碟上。</span><span class="sxs-lookup"><span data-stu-id="a1328-107">Therefore it is recommended only toouse LVM on hello data disks.</span></span>

## <a name="linear-vs-striped-logical-volumes"></a><span data-ttu-id="a1328-108">線性與等量邏輯磁碟區</span><span class="sxs-lookup"><span data-stu-id="a1328-108">Linear vs. striped logical volumes</span></span>
<span data-ttu-id="a1328-109">LVM 可以是使用的 toocombine 到單一存放磁碟區的實體磁碟的數量。</span><span class="sxs-lookup"><span data-stu-id="a1328-109">LVM can be used toocombine a number of physical disks into a single storage volume.</span></span> <span data-ttu-id="a1328-110">根據預設 LVM 通常會建立線性的邏輯磁碟區，這表示 hello 實體儲存體串連在一起。</span><span class="sxs-lookup"><span data-stu-id="a1328-110">By default LVM will usually create linear logical volumes, which means that hello physical storage is concatenated together.</span></span> <span data-ttu-id="a1328-111">在此情況下讀取/寫入作業通常只會傳送 tooa 單一磁碟。</span><span class="sxs-lookup"><span data-stu-id="a1328-111">In this case read/write operations will typically only be sent tooa single disk.</span></span> <span data-ttu-id="a1328-112">相反地，我們也可以建立等量邏輯磁碟區讀取和寫入是分散式的 toomultiple hello 磁碟區群組 (也就是類似 tooRAID0) 中所包含的磁碟。</span><span class="sxs-lookup"><span data-stu-id="a1328-112">In contrast, we can also create striped logical volumes where reads and writes are distributed toomultiple disks contained in hello volume group (i.e. similar tooRAID0).</span></span> <span data-ttu-id="a1328-113">基於效能的考量，很可能您會想 toostripe 邏輯磁碟區，以便讀取和寫入利用所有連接的資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="a1328-113">For performance reasons it is likely you will want toostripe your logical volumes so that reads and writes utilize all your attached data disks.</span></span>

<span data-ttu-id="a1328-114">本文件將說明如何 toocombine 數個資料磁碟到單一磁碟區群組中，然後再建立等量邏輯磁碟區。</span><span class="sxs-lookup"><span data-stu-id="a1328-114">This document will describe how toocombine several data disks into a single volume group, and then create a striped logical volume.</span></span> <span data-ttu-id="a1328-115">有些一般化的 toowork 大部分分佈，則 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="a1328-115">hello steps below are somewhat generalized toowork with most distributions.</span></span> <span data-ttu-id="a1328-116">在大部分情況下 hello 公用程式和管理 LVM 在 Azure 上的工作流程不是本質上不同於其他環境。</span><span class="sxs-lookup"><span data-stu-id="a1328-116">In most cases hello utilities and workflows for managing LVM on Azure are not fundamentally different than other environments.</span></span> <span data-ttu-id="a1328-117">像往常一樣，也請向您的 Linux 廠商洽詢搭配特定散發套件使用 LVM 的文件和最佳做法。</span><span class="sxs-lookup"><span data-stu-id="a1328-117">As usual, please also consult your Linux vendor for documentation and best practices for using LVM with your particular distribution.</span></span>

## <a name="attaching-data-disks"></a><span data-ttu-id="a1328-118">連接資料磁碟</span><span class="sxs-lookup"><span data-stu-id="a1328-118">Attaching data disks</span></span>
<span data-ttu-id="a1328-119">其中一個通常會想 toostart 有兩個或多個空的資料磁碟時使用 LVM。</span><span class="sxs-lookup"><span data-stu-id="a1328-119">One will usually want toostart with two or more empty data disks when using LVM.</span></span> <span data-ttu-id="a1328-120">根據您的 IO 需求，您可以選擇儲存在我們的標準儲存體，與總 too500 IO/每個磁碟或使用向上 too5000 IO/每個磁碟 ps 我們高階儲存體 ps tooattach 磁碟。</span><span class="sxs-lookup"><span data-stu-id="a1328-120">Based on your IO needs, you can choose tooattach disks that are stored in our Standard Storage, with up too500 IO/ps per disk or our Premium storage with up too5000 IO/ps per disk.</span></span> <span data-ttu-id="a1328-121">本文會深入說明如何 tooprovision 和附加資料磁碟 tooa Linux 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a1328-121">This article will not go into detail on how tooprovision and attach data disks tooa Linux virtual machine.</span></span> <span data-ttu-id="a1328-122">請參閱 hello Microsoft Azure 文件[連接磁碟](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)如需有關如何 tooattach 空的資料磁碟在 Azure 上 tooa Linux 虛擬機器的詳細指示。</span><span class="sxs-lookup"><span data-stu-id="a1328-122">Please see hello Microsoft Azure article [attach a disk](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for detailed instructions on how tooattach an empty data disk tooa Linux virtual machine on Azure.</span></span>

## <a name="install-hello-lvm-utilities"></a><span data-ttu-id="a1328-123">安裝 hello LVM 公用程式</span><span class="sxs-lookup"><span data-stu-id="a1328-123">Install hello LVM utilities</span></span>
* <span data-ttu-id="a1328-124">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="a1328-124">**Ubuntu**</span></span>

    ```bash  
    sudo apt-get update
    sudo apt-get install lvm2
    ```

* <span data-ttu-id="a1328-125">**RHEL、CentOS 和 Oracle Linux**</span><span class="sxs-lookup"><span data-stu-id="a1328-125">**RHEL, CentOS & Oracle Linux**</span></span>

    ```bash   
    sudo yum install lvm2
    ```

* <span data-ttu-id="a1328-126">**SLES 12 和 openSUSE**</span><span class="sxs-lookup"><span data-stu-id="a1328-126">**SLES 12 and openSUSE**</span></span>

    ```bash   
    sudo zypper install lvm2
    ```

* <span data-ttu-id="a1328-127">**SLES 11**</span><span class="sxs-lookup"><span data-stu-id="a1328-127">**SLES 11**</span></span>

    ```bash   
    sudo zypper install lvm2
    ```

    <span data-ttu-id="a1328-128">SLES11 上則必須同時編輯`/etc/sysconfig/lvm`並設定`LVM_ACTIVATED_ON_DISCOVERED`太 「 啟用 」:</span><span class="sxs-lookup"><span data-stu-id="a1328-128">On SLES11 you must also edit `/etc/sysconfig/lvm` and set `LVM_ACTIVATED_ON_DISCOVERED` too"enable":</span></span>

    ```sh   
    LVM_ACTIVATED_ON_DISCOVERED="enable" 
    ```

## <a name="configure-lvm"></a><span data-ttu-id="a1328-129">設定 LVM</span><span class="sxs-lookup"><span data-stu-id="a1328-129">Configure LVM</span></span>
<span data-ttu-id="a1328-130">本指南中，我們將假設您已經附加三個資料磁碟，我們將參照 tooas `/dev/sdc`，`/dev/sdd`和`/dev/sde`。</span><span class="sxs-lookup"><span data-stu-id="a1328-130">In this guide we will assume you have attached three data disks, which we'll refer tooas `/dev/sdc`, `/dev/sdd` and `/dev/sde`.</span></span> <span data-ttu-id="a1328-131">請注意，這些可能不一定 hello 在 VM 中的相同路徑名稱。</span><span class="sxs-lookup"><span data-stu-id="a1328-131">Note that these may not always be hello same path names in your VM.</span></span> <span data-ttu-id="a1328-132">您可以執行 '`sudo fdisk -l`' 或類似的命令 toolist 可用的磁碟。</span><span class="sxs-lookup"><span data-stu-id="a1328-132">You can run '`sudo fdisk -l`' or similar command toolist your available disks.</span></span>

1. <span data-ttu-id="a1328-133">準備 hello 實體磁碟區：</span><span class="sxs-lookup"><span data-stu-id="a1328-133">Prepare hello physical volumes:</span></span>

    ```bash    
    sudo pvcreate /dev/sd[cde]
    Physical volume "/dev/sdc" successfully created
    Physical volume "/dev/sdd" successfully created
    Physical volume "/dev/sde" successfully created
    ```

2. <span data-ttu-id="a1328-134">建立磁碟區群組。</span><span class="sxs-lookup"><span data-stu-id="a1328-134">Create a volume group.</span></span> <span data-ttu-id="a1328-135">在此範例中，我們正在撥打 hello 磁碟區群組`data-vg01`:</span><span class="sxs-lookup"><span data-stu-id="a1328-135">In this example we are calling hello volume group `data-vg01`:</span></span>

    ```bash    
    sudo vgcreate data-vg01 /dev/sd[cde]
    Volume group "data-vg01" successfully created
    ```

3. <span data-ttu-id="a1328-136">建立 hello 邏輯磁碟區。</span><span class="sxs-lookup"><span data-stu-id="a1328-136">Create hello logical volume(s).</span></span> <span data-ttu-id="a1328-137">hello 命令以下我們會建立單一的邏輯磁碟區，以呼叫`data-lv01`toospan hello 整個磁碟區群組，但請注意，它也是可行的 toocreate hello 磁碟區群組中的多個邏輯磁碟區。</span><span class="sxs-lookup"><span data-stu-id="a1328-137">hello command below we will create a single logical volume called `data-lv01` toospan hello entire volume group, but note that it is also feasible toocreate multiple logical volumes in hello volume group.</span></span>

    ```bash   
    sudo lvcreate --extents 100%FREE --stripes 3 --name data-lv01 data-vg01
    Logical volume "data-lv01" created.
    ```

4. <span data-ttu-id="a1328-138">Hello 邏輯磁碟區格式化</span><span class="sxs-lookup"><span data-stu-id="a1328-138">Format hello logical volume</span></span>

    ```bash  
    sudo mkfs -t ext4 /dev/data-vg01/data-lv01
    ```
   
   > [!NOTE]
   > <span data-ttu-id="a1328-139">SLES11 請使用 `-t ext3` 而不是 ext4。</span><span class="sxs-lookup"><span data-stu-id="a1328-139">With SLES11 use `-t ext3` instead of ext4.</span></span> <span data-ttu-id="a1328-140">SLES11 僅支援唯讀存取 tooext4 檔案系統。</span><span class="sxs-lookup"><span data-stu-id="a1328-140">SLES11 only supports read-only access tooext4 filesystems.</span></span>

## <a name="add-hello-new-file-system-tooetcfstab"></a><span data-ttu-id="a1328-141">新增 hello 新檔案系統太/等/fstab</span><span class="sxs-lookup"><span data-stu-id="a1328-141">Add hello new file system too/etc/fstab</span></span>
> [!IMPORTANT]
> <span data-ttu-id="a1328-142">不當編輯 hello`/etc/fstab`檔案可能會導致系統無法重新啟動。</span><span class="sxs-lookup"><span data-stu-id="a1328-142">Improperly editing hello `/etc/fstab` file could result in an unbootable system.</span></span> <span data-ttu-id="a1328-143">如果不確定，請參閱 toohello 發佈文件 tooproperly 如何編輯此檔案的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="a1328-143">If unsure, please refer toohello distribution's documentation for information on how tooproperly edit this file.</span></span> <span data-ttu-id="a1328-144">它也是建議的 hello 備份`/etc/fstab`編輯之前建立檔案。</span><span class="sxs-lookup"><span data-stu-id="a1328-144">It is also recommended that a backup of hello `/etc/fstab` file is created before editing.</span></span>

1. <span data-ttu-id="a1328-145">建立新的檔案系統，所需的 hello 掛接點，例如：</span><span class="sxs-lookup"><span data-stu-id="a1328-145">Create hello desired mount point for your new file system, for example:</span></span>

    ```bash  
    sudo mkdir /data
    ```

2. <span data-ttu-id="a1328-146">找出 hello 邏輯磁碟區路徑</span><span class="sxs-lookup"><span data-stu-id="a1328-146">Locate hello logical volume path</span></span>

    ```bash    
    lvdisplay
    --- Logical volume ---
    LV Path                /dev/data-vg01/data-lv01
    ....
    ```

3. <span data-ttu-id="a1328-147">開啟`/etc/fstab`文字編輯器中，為新增項目 hello 新的檔案系統，例如：</span><span class="sxs-lookup"><span data-stu-id="a1328-147">Open `/etc/fstab` in a text editor and add an entry for hello new file system, for example:</span></span>

    ```bash    
    /dev/data-vg01/data-lv01  /data  ext4  defaults  0  2
    ```   
    <span data-ttu-id="a1328-148">然後，儲存並關閉 `/etc/fstab`。</span><span class="sxs-lookup"><span data-stu-id="a1328-148">Then, save and close `/etc/fstab`.</span></span>

4. <span data-ttu-id="a1328-149">測試該 hello`/etc/fstab`輸入是否正確：</span><span class="sxs-lookup"><span data-stu-id="a1328-149">Test that hello `/etc/fstab` entry is correct:</span></span>

    ```bash    
    sudo mount -a
    ```

    <span data-ttu-id="a1328-150">如果此命令會產生錯誤訊息請檢查在 hello hello 語法`/etc/fstab`檔案。</span><span class="sxs-lookup"><span data-stu-id="a1328-150">If this command results in an error message please check hello syntax in hello `/etc/fstab` file.</span></span>
   
    <span data-ttu-id="a1328-151">接下來執行 hello`mount`命令 tooensure hello 檔案系統已裝載：</span><span class="sxs-lookup"><span data-stu-id="a1328-151">Next run hello `mount` command tooensure hello file system is mounted:</span></span>

    ```bash    
    mount
    ......
    /dev/mapper/data--vg01-data--lv01 on /data type ext4 (rw)
    ```

5. <span data-ttu-id="a1328-152">(選擇性) 保全 `/etc/fstab`中的開機參數</span><span class="sxs-lookup"><span data-stu-id="a1328-152">(Optional) Failsafe boot parameters in `/etc/fstab`</span></span>
   
    <span data-ttu-id="a1328-153">許多發行包含任一 hello`nobootwait`或`nofail`掛接參數可能會加入 toohello`/etc/fstab`檔案。</span><span class="sxs-lookup"><span data-stu-id="a1328-153">Many distributions include either hello `nobootwait` or `nofail` mount parameters that may be added toohello `/etc/fstab` file.</span></span> <span data-ttu-id="a1328-154">這些參數時掛接特定檔案系統允許的失敗，並允許 hello Linux 系統 toocontinue tooboot，即使它是無法 tooproperly 掛接 hello RAID 檔案系統。</span><span class="sxs-lookup"><span data-stu-id="a1328-154">These parameters allow for failures when mounting a particular file system and allow hello Linux system toocontinue tooboot even if it is unable tooproperly mount hello RAID file system.</span></span> <span data-ttu-id="a1328-155">請如需這些參數的詳細資訊，參閱 tooyour 發佈文件。</span><span class="sxs-lookup"><span data-stu-id="a1328-155">Please refer tooyour distribution's documentation for more information on these parameters.</span></span>
   
    <span data-ttu-id="a1328-156">範例 (Ubuntu)：</span><span class="sxs-lookup"><span data-stu-id="a1328-156">Example (Ubuntu):</span></span>

    ```bash 
    /dev/data-vg01/data-lv01  /data  ext4  defaults,nobootwait  0  2
    ```

## <a name="trimunmap-support"></a><span data-ttu-id="a1328-157">TRIM/UNMAP 支援</span><span class="sxs-lookup"><span data-stu-id="a1328-157">TRIM/UNMAP support</span></span>
<span data-ttu-id="a1328-158">某些 Linux 核心支援 TRIM/UNMAP 作業 toodiscard hello 磁碟上未使用的區塊。</span><span class="sxs-lookup"><span data-stu-id="a1328-158">Some Linux kernels support TRIM/UNMAP operations toodiscard unused blocks on hello disk.</span></span> <span data-ttu-id="a1328-159">這些運算全都是主要適用於標準儲存體 tooinform 刪除頁面的 Azure 不再有效，以及可以捨棄。</span><span class="sxs-lookup"><span data-stu-id="a1328-159">These operations are primarily useful in standard storage tooinform Azure that deleted pages are no longer valid and can be discarded.</span></span> <span data-ttu-id="a1328-160">如果您建立大型檔案，然後再將它們刪除，捨棄頁面可以節省成本。</span><span class="sxs-lookup"><span data-stu-id="a1328-160">Discarding pages can save cost if you create large files and then delete them.</span></span>

<span data-ttu-id="a1328-161">有兩種 tooenable TRIM 支援在 Linux VM 中。</span><span class="sxs-lookup"><span data-stu-id="a1328-161">There are two ways tooenable TRIM support in your Linux VM.</span></span> <span data-ttu-id="a1328-162">像往常一樣，參閱您的發佈 hello 建議的方法包括：</span><span class="sxs-lookup"><span data-stu-id="a1328-162">As usual, consult your distribution for hello recommended approach:</span></span>

- <span data-ttu-id="a1328-163">使用 hello`discard`掛接中的選項`/etc/fstab`，例如：</span><span class="sxs-lookup"><span data-stu-id="a1328-163">Use hello `discard` mount option in `/etc/fstab`, for example:</span></span>

    ```bash 
    /dev/data-vg01/data-lv01  /data  ext4  defaults,discard  0  2
    ```

- <span data-ttu-id="a1328-164">在某些情況下 hello`discard`選項可能會影響效能。</span><span class="sxs-lookup"><span data-stu-id="a1328-164">In some cases hello `discard` option may have performance implications.</span></span> <span data-ttu-id="a1328-165">或者，您可以在其中執行 hello`fstrim`命令手動從 hello 命令列，或將它加入 tooyour crontab toorun 定期：</span><span class="sxs-lookup"><span data-stu-id="a1328-165">Alternatively, you can run hello `fstrim` command manually from hello command line, or add it tooyour crontab toorun regularly:</span></span>

    <span data-ttu-id="a1328-166">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="a1328-166">**Ubuntu**</span></span>

    ```bash 
    # sudo apt-get install util-linux
    # sudo fstrim /datadrive
    ```

    <span data-ttu-id="a1328-167">**RHEL/CentOS**</span><span class="sxs-lookup"><span data-stu-id="a1328-167">**RHEL/CentOS**</span></span>

    ```bash 
    # sudo yum install util-linux
    # sudo fstrim /datadrive
    ```
