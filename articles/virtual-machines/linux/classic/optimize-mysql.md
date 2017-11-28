---
title: "在 Linux 上的 MySQL 效能 aaaOptimize |Microsoft 文件"
description: "深入了解如何 toooptimize MySQL Azure 虛擬機器 (VM) 執行 Linux 上執行。"
services: virtual-machines-linux
documentationcenter: 
author: NingKuang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 0c1c7fc5-a528-4d84-b65d-2df225f2233f
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: ningk
ms.openlocfilehash: 9e6458723233721e06f30b9de33635d403eefcba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-mysql-performance-on-azure-linux-vms"></a><span data-ttu-id="3915a-103">在 Azure Linux 上最佳化 MySQL 效能</span><span class="sxs-lookup"><span data-stu-id="3915a-103">Optimize MySQL Performance on Azure Linux VMs</span></span>
<span data-ttu-id="3915a-104">有許多因素會影響 Azure 上的 MySQL 效能，均與虛擬硬體選取和軟體設定有關。</span><span class="sxs-lookup"><span data-stu-id="3915a-104">There are many factors that affect MySQL performance on Azure, both in virtual hardware selection and software configuration.</span></span> <span data-ttu-id="3915a-105">本文著重於透過儲存體、系統和資料庫設定最佳化效能。</span><span class="sxs-lookup"><span data-stu-id="3915a-105">This article focuses on optimizing performance through storage, system, and database configurations.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3915a-106">Azure 建立和處理資源的部署模型有兩種：[Azure Resource Manager](../../../resource-manager-deployment-model.md) 和傳統。</span><span class="sxs-lookup"><span data-stu-id="3915a-106">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager](../../../resource-manager-deployment-model.md) and classic.</span></span> <span data-ttu-id="3915a-107">本文說明如何使用 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="3915a-107">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="3915a-108">Microsoft 建議最新的部署使用 hello 資源管理員的模型。</span><span class="sxs-lookup"><span data-stu-id="3915a-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="3915a-109">Linux VM 最佳化與 hello 資源管理員模型的相關資訊，請參閱[最佳化您的 Linux VM 在 Azure 上](../optimization.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="3915a-109">For information about Linux VM optimizations with hello Resource Manager model, see [Optimize your Linux VM on Azure](../optimization.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="utilize-raid-on-an-azure-virtual-machine"></a><span data-ttu-id="3915a-110">在 Azure 虛擬機器上利用 RAID</span><span class="sxs-lookup"><span data-stu-id="3915a-110">Utilize RAID on an Azure virtual machine</span></span>
<span data-ttu-id="3915a-111">儲存體是 hello 會影響雲端環境中的資料庫效能的關鍵因素。</span><span class="sxs-lookup"><span data-stu-id="3915a-111">Storage is hello key factor that affects database performance in cloud environments.</span></span> <span data-ttu-id="3915a-112">比較的 tooa 單一磁碟，RAID 可提供透過並行存取速度。</span><span class="sxs-lookup"><span data-stu-id="3915a-112">Compared tooa single disk, RAID can provide faster access via concurrency.</span></span> <span data-ttu-id="3915a-113">如需詳細資訊，請參閱[標準 RAID 層級](http://en.wikipedia.org/wiki/Standard_RAID_levels)。</span><span class="sxs-lookup"><span data-stu-id="3915a-113">For more information, see [Standard RAID levels](http://en.wikipedia.org/wiki/Standard_RAID_levels).</span></span>   

<span data-ttu-id="3915a-114">可透過 RAID 改進 Azure 中的磁碟 I/O 輸送量和 I/O 回應時間。</span><span class="sxs-lookup"><span data-stu-id="3915a-114">Disk I/O throughput and I/O response time in Azure can be improved through RAID.</span></span> <span data-ttu-id="3915a-115">我們的實驗室測試顯示磁碟 I/O 輸送量可以兩倍，且 I/O 回應時間可以降低一半平均的 RAID 磁碟 hello 數目會加倍 （從兩個 toofour、 四個 tooeight 等）。</span><span class="sxs-lookup"><span data-stu-id="3915a-115">Our lab tests show that disk I/O throughput can be doubled and I/O response time can be reduced by half on average when hello number of RAID disks is doubled (from two toofour, four tooeight, etc.).</span></span> <span data-ttu-id="3915a-116">如需詳細資訊，請參閱 [附錄 A](#AppendixA) 。</span><span class="sxs-lookup"><span data-stu-id="3915a-116">See [Appendix A](#AppendixA) for details.</span></span>  

<span data-ttu-id="3915a-117">此外 toodisk I/O MySQL 效能會提升增加 hello RAID 層級。</span><span class="sxs-lookup"><span data-stu-id="3915a-117">In addition toodisk I/O, MySQL performance improves when you increase hello RAID level.</span></span>  <span data-ttu-id="3915a-118">如需詳細資訊，請參閱 [附錄 B](#AppendixB) 。</span><span class="sxs-lookup"><span data-stu-id="3915a-118">See [Appendix B](#AppendixB) for details.</span></span>  

<span data-ttu-id="3915a-119">您也可以 tooconsider hello 區塊大小。</span><span class="sxs-lookup"><span data-stu-id="3915a-119">You might also want tooconsider hello chunk size.</span></span> <span data-ttu-id="3915a-120">通常當您有較大的區塊大小時，您的額外負荷會比較低，尤其是大量寫入時。</span><span class="sxs-lookup"><span data-stu-id="3915a-120">In general, when you have a larger chunk size, you get lower overhead, especially for large writes.</span></span> <span data-ttu-id="3915a-121">不過，hello 區塊大小太大時，它可能會加入額外負擔，使您無法利用 RAID。</span><span class="sxs-lookup"><span data-stu-id="3915a-121">However, when hello chunk size is too large, it might add additional overhead that prevents you from taking advantage of RAID.</span></span> <span data-ttu-id="3915a-122">hello 目前的預設大小為 512 KB，證明 toobe 最常見的實際執行環境的最佳選擇。</span><span class="sxs-lookup"><span data-stu-id="3915a-122">hello current default size is 512 KB, which is proven toobe optimal for most general production environments.</span></span> <span data-ttu-id="3915a-123">如需詳細資訊，請參閱 [附錄 C](#AppendixC) 。</span><span class="sxs-lookup"><span data-stu-id="3915a-123">See [Appendix C](#AppendixC) for details.</span></span>   

<span data-ttu-id="3915a-124">您可針對不同虛擬機器類型新增的磁碟數目會有所限制。</span><span class="sxs-lookup"><span data-stu-id="3915a-124">There are limits on how many disks you can add for different virtual machine types.</span></span> <span data-ttu-id="3915a-125">[Azure 的虛擬機器和雲端服務大小](http://msdn.microsoft.com/library/azure/dn197896.aspx)中有這些限制的詳細說明。</span><span class="sxs-lookup"><span data-stu-id="3915a-125">These limits are detailed in [Virtual machine and cloud service sizes for Azure](http://msdn.microsoft.com/library/azure/dn197896.aspx).</span></span> <span data-ttu-id="3915a-126">雖然您可以選擇 tooset RAID 設定具有較少的磁碟，您將需要四個連接的資料磁碟 toofollow hello RAID 範例在本文中。</span><span class="sxs-lookup"><span data-stu-id="3915a-126">You will need four attached data disks toofollow hello RAID example in this article, although you can choose tooset up RAID with fewer disks.</span></span>  

<span data-ttu-id="3915a-127">本文假設您已經建立 Linux 虛擬機器並已安裝及設定 MYSQL 。</span><span class="sxs-lookup"><span data-stu-id="3915a-127">This article assumes you have already created a Linux virtual machine and have MYSQL installed and configured.</span></span> <span data-ttu-id="3915a-128">如需有關如何開始使用的詳細資訊，請參閱 < 如何在 Azure 上 MySQL tooinstall。</span><span class="sxs-lookup"><span data-stu-id="3915a-128">For more information on getting started, see How tooinstall MySQL on Azure.</span></span>  

### <a name="set-up-raid-on-azure"></a><span data-ttu-id="3915a-129">在 Azure 上設定 RAID</span><span class="sxs-lookup"><span data-stu-id="3915a-129">Set up RAID on Azure</span></span>
<span data-ttu-id="3915a-130">hello 下列步驟說明在 Azure 上 toocreate RAID hello Azure 入口網站的使用方式。</span><span class="sxs-lookup"><span data-stu-id="3915a-130">hello following steps show how toocreate RAID on Azure by using hello Azure portal.</span></span> <span data-ttu-id="3915a-131">您也可以使用 Windows PowerShell 指令碼設定 RAID。</span><span class="sxs-lookup"><span data-stu-id="3915a-131">You can also set up RAID by using Windows PowerShell scripts.</span></span>
<span data-ttu-id="3915a-132">在此範例中，我們將設定具有四個磁碟的 RAID 0。</span><span class="sxs-lookup"><span data-stu-id="3915a-132">In this example, we will configure RAID 0 with four disks.</span></span>  

#### <a name="add-a-data-disk-tooyour-virtual-machine"></a><span data-ttu-id="3915a-133">新增資料磁碟 tooyour 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="3915a-133">Add a data disk tooyour virtual machine</span></span>
<span data-ttu-id="3915a-134">在 hello Azure 入口網站，移 toohello 儀表板，然後選取您想要的資料磁碟 tooadd hello 虛擬機器 toowhich。</span><span class="sxs-lookup"><span data-stu-id="3915a-134">In hello Azure portal, go toohello dashboard and select hello virtual machine toowhich you want tooadd a data disk.</span></span> <span data-ttu-id="3915a-135">在此範例中，hello 虛擬機器是 mysqlnode1。</span><span class="sxs-lookup"><span data-stu-id="3915a-135">In this example, hello virtual machine is mysqlnode1.</span></span>  

<!--![Virtual machines][1]-->

<span data-ttu-id="3915a-136">按一下 磁碟，然後按一下連結新項目。</span><span class="sxs-lookup"><span data-stu-id="3915a-136">Click **Disks** and then click **Attach New**.</span></span>

![虛擬機器新增磁碟](media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-Disks-option.png)

<span data-ttu-id="3915a-138">建立一個新的 500 GB 磁碟。</span><span class="sxs-lookup"><span data-stu-id="3915a-138">Create a new 500 GB disk.</span></span> <span data-ttu-id="3915a-139">請確定**主機快取喜好設定**設定得**無**。</span><span class="sxs-lookup"><span data-stu-id="3915a-139">Make sure that **Host Cache Preference** is set too**None**.</span></span>  <span data-ttu-id="3915a-140">完成時，請按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="3915a-140">When you're finished, click **OK**.</span></span>

![連接空的磁碟](media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-attach-empty-disk.png)


<span data-ttu-id="3915a-142">這會將一個空的磁碟新增到虛擬機器中。</span><span class="sxs-lookup"><span data-stu-id="3915a-142">This adds one empty disk into your virtual machine.</span></span> <span data-ttu-id="3915a-143">再重複執行此步驟三次，您的 RAID 就有四個資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="3915a-143">Repeat this step three more times so that you have four data disks for RAID.</span></span>  

<span data-ttu-id="3915a-144">您可以查看加入 hello 藉由查看 hello 核心訊息記錄檔中 hello 虛擬機器磁碟機。</span><span class="sxs-lookup"><span data-stu-id="3915a-144">You can see hello added drives in hello virtual machine by looking at hello kernel message log.</span></span> <span data-ttu-id="3915a-145">例如，toosee 這在 Ubuntu，下列命令使用 hello:</span><span class="sxs-lookup"><span data-stu-id="3915a-145">For example, toosee this on Ubuntu, use hello following command:</span></span>  

    sudo grep SCSI /var/log/dmesg

#### <a name="create-raid-with-hello-additional-disks"></a><span data-ttu-id="3915a-146">建立以 hello 更多磁碟的 RAID</span><span class="sxs-lookup"><span data-stu-id="3915a-146">Create RAID with hello additional disks</span></span>
<span data-ttu-id="3915a-147">hello 下列步驟說明如何太[設定軟體 RAID on Linux](../configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="3915a-147">hello following steps describe how too[configure software RAID on Linux](../configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

> [!NOTE]
> <span data-ttu-id="3915a-148">如果您使用 hello XFS 檔案系統，執行下列步驟之後您已經建立 RAID, hello。</span><span class="sxs-lookup"><span data-stu-id="3915a-148">If you are using hello XFS file system, execute hello following steps after you have created RAID.</span></span>
>
>

<span data-ttu-id="3915a-149">在 Debian，Ubuntu 或 Linux 迷你澆，下列命令使用 hello tooinstall XFS:</span><span class="sxs-lookup"><span data-stu-id="3915a-149">tooinstall XFS on Debian, Ubuntu, or Linux Mint, use hello following command:</span></span>  

    apt-get -y install xfsprogs  

<span data-ttu-id="3915a-150">tooinstall XFS 上 Fedora、 CentOS、 或 RHEL、 使用 hello，下列命令：</span><span class="sxs-lookup"><span data-stu-id="3915a-150">tooinstall XFS on Fedora, CentOS, or RHEL, use hello following command:</span></span>  

    yum -y install xfsprogs  xfsdump


#### <a name="set-up-a-new-storage-path"></a><span data-ttu-id="3915a-151">設定新的儲存體路徑</span><span class="sxs-lookup"><span data-stu-id="3915a-151">Set up a new storage path</span></span>
<span data-ttu-id="3915a-152">使用下列新的儲存體路徑的命令 tooset hello:</span><span class="sxs-lookup"><span data-stu-id="3915a-152">Use hello following command tooset up a new storage path:</span></span>  

    root@mysqlnode1:~# mkdir -p /RAID0/mysql

#### <a name="copy-hello-original-data-toohello-new-storage-path"></a><span data-ttu-id="3915a-153">複製 hello 原始資料 toohello 新儲存體路徑</span><span class="sxs-lookup"><span data-stu-id="3915a-153">Copy hello original data toohello new storage path</span></span>
<span data-ttu-id="3915a-154">使用下列命令 toocopy 資料 toohello 新儲存體路徑 hello:</span><span class="sxs-lookup"><span data-stu-id="3915a-154">Use hello following command toocopy data toohello new storage path:</span></span>  

    root@mysqlnode1:~# cp -rp /var/lib/mysql/* /RAID0/mysql/

#### <a name="modify-permissions-so-mysql-can-access-read-and-write-hello-data-disk"></a><span data-ttu-id="3915a-155">修改權限，因此可以存取 MySQL （讀取和寫入） hello 資料磁碟</span><span class="sxs-lookup"><span data-stu-id="3915a-155">Modify permissions so MySQL can access (read and write) hello data disk</span></span>
<span data-ttu-id="3915a-156">使用下列命令 toomodify 權限的 hello:</span><span class="sxs-lookup"><span data-stu-id="3915a-156">Use hello following command toomodify permissions:</span></span>  

    root@mysqlnode1:~# chown -R mysql.mysql /RAID0/mysql && chmod -R 755 /RAID0/mysql


## <a name="adjust-hello-disk-io-scheduling-algorithm"></a><span data-ttu-id="3915a-157">調整排程演算法 hello 磁碟 I/O</span><span class="sxs-lookup"><span data-stu-id="3915a-157">Adjust hello disk I/O scheduling algorithm</span></span>
<span data-ttu-id="3915a-158">Linux 會實作四種類型的 I/O 排程演算法：</span><span class="sxs-lookup"><span data-stu-id="3915a-158">Linux implements four types of I/O scheduling algorithms:</span></span>  

* <span data-ttu-id="3915a-159">NOOP 演算法 (沒有作業)</span><span class="sxs-lookup"><span data-stu-id="3915a-159">NOOP algorithm (No Operation)</span></span>
* <span data-ttu-id="3915a-160">期限演算法 (期限)</span><span class="sxs-lookup"><span data-stu-id="3915a-160">Deadline algorithm (Deadline)</span></span>
* <span data-ttu-id="3915a-161">完全公平佇列演算法 (CFQ)</span><span class="sxs-lookup"><span data-stu-id="3915a-161">Completely fair queuing algorithm (CFQ)</span></span>
* <span data-ttu-id="3915a-162">預算週期演算法 (預期)</span><span class="sxs-lookup"><span data-stu-id="3915a-162">Budget period algorithm (Anticipatory)</span></span>  

<span data-ttu-id="3915a-163">您可以選取不同的 I/O 排程器，在不同的案例 toooptimize 效能。</span><span class="sxs-lookup"><span data-stu-id="3915a-163">You can select different I/O schedulers under different scenarios toooptimize performance.</span></span> <span data-ttu-id="3915a-164">在完全隨機存取環境中，沒有顯著的差異 hello CFQ 以及期限之演算法的效能。</span><span class="sxs-lookup"><span data-stu-id="3915a-164">In a completely random access environment, there is not a significant difference between hello CFQ and Deadline algorithms for performance.</span></span> <span data-ttu-id="3915a-165">我們建議您設定 hello MySQL 資料庫環境 tooDeadline 的穩定性。</span><span class="sxs-lookup"><span data-stu-id="3915a-165">We recommend that you set hello MySQL database environment tooDeadline for stability.</span></span> <span data-ttu-id="3915a-166">如果有大量循序 I/O，CFQ 可能會降低磁碟 I/O 效能。</span><span class="sxs-lookup"><span data-stu-id="3915a-166">If there is a lot of sequential I/O, CFQ might reduce disk I/O performance.</span></span>   

<span data-ttu-id="3915a-167">針對 SSD 和其他設備，NOOP 或期限可以達到較佳的效能比 hello 預設排程器。</span><span class="sxs-lookup"><span data-stu-id="3915a-167">For SSD and other equipment, NOOP or Deadline can achieve better performance than hello default scheduler.</span></span>   

<span data-ttu-id="3915a-168">先前 toohello 核心 2.5，hello 預設 I/O 排程演算法會是期限。</span><span class="sxs-lookup"><span data-stu-id="3915a-168">Prior toohello kernel 2.5, hello default I/O scheduling algorithm is Deadline.</span></span> <span data-ttu-id="3915a-169">從開始 hello 核心 2.6.18，CFQ 變成 hello 預設 I/O 排程演算法。</span><span class="sxs-lookup"><span data-stu-id="3915a-169">Starting with hello kernel 2.6.18, CFQ became hello default I/O scheduling algorithm.</span></span>  <span data-ttu-id="3915a-170">您可以指定此設定會在核心開機時，或 hello 系統正在運作時，動態修改此設定。</span><span class="sxs-lookup"><span data-stu-id="3915a-170">You can specify this setting at kernel boot time or dynamically modify this setting when hello system is running.</span></span>  

<span data-ttu-id="3915a-171">下列範例中的 hello 示範 toocheck 以及組 hello hello Debian 發佈系列中的預設排程器 toohello NOOP 演算法。</span><span class="sxs-lookup"><span data-stu-id="3915a-171">hello following example demonstrates how toocheck and set hello default scheduler toohello NOOP algorithm in hello Debian distribution family.</span></span>  

### <a name="view-hello-current-io-scheduler"></a><span data-ttu-id="3915a-172">檢視 hello 目前 I/O 排程器</span><span class="sxs-lookup"><span data-stu-id="3915a-172">View hello current I/O scheduler</span></span>
<span data-ttu-id="3915a-173">tooview hello 排程器執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="3915a-173">tooview hello scheduler run hello following command:</span></span>  

    root@mysqlnode1:~# cat /sys/block/sda/queue/scheduler

<span data-ttu-id="3915a-174">您會看到下列輸出，指出目前排程器 hello:</span><span class="sxs-lookup"><span data-stu-id="3915a-174">You will see following output, which indicates hello current scheduler:</span></span>  

    noop [deadline] cfq


### <a name="change-hello-current-device-devsda-of-hello-io-scheduling-algorithm"></a><span data-ttu-id="3915a-175">變更 hello 目前裝置 (/ 開發/sda) hello I/O 排程演算法</span><span class="sxs-lookup"><span data-stu-id="3915a-175">Change hello current device (/dev/sda) of hello I/O scheduling algorithm</span></span>
<span data-ttu-id="3915a-176">執行下列命令 toochange hello 目前裝置 hello:</span><span class="sxs-lookup"><span data-stu-id="3915a-176">Run hello following commands toochange hello current device:</span></span>  

    azureuser@mysqlnode1:~$ sudo su -
    root@mysqlnode1:~# echo "noop" >/sys/block/sda/queue/scheduler
    root@mysqlnode1:~# sed -i 's/GRUB_CMDLINE_LINUX=""/GRUB_CMDLINE_LINUX_DEFAULT="quiet splash elevator=noop"/g' /etc/default/grub
    root@mysqlnode1:~# update-grub

> [!NOTE]
> <span data-ttu-id="3915a-177">單獨針對 /dev/sda 設定此項並不是很有用。</span><span class="sxs-lookup"><span data-stu-id="3915a-177">Setting this for /dev/sda alone is not useful.</span></span> <span data-ttu-id="3915a-178">它必須設定所有資料磁碟上 hello 資料庫所在的位置。</span><span class="sxs-lookup"><span data-stu-id="3915a-178">It must be set on all data disks where hello database resides.</span></span>  
>
>

<span data-ttu-id="3915a-179">您應該會看到下列輸出，表示已成功重建 grub.cfg，且該 hello 預設排程器已更新的 tooNOOP hello:</span><span class="sxs-lookup"><span data-stu-id="3915a-179">You should see hello following output, indicating that grub.cfg has been rebuilt successfully and that hello default scheduler has been updated tooNOOP:</span></span>  

    Generating grub configuration file ...
    Found linux image: /boot/vmlinuz-3.13.0-34-generic
    Found initrd image: /boot/initrd.img-3.13.0-34-generic
    Found linux image: /boot/vmlinuz-3.13.0-32-generic
    Found initrd image: /boot/initrd.img-3.13.0-32-generic
    Found memtest86+ image: /memtest86+.elf
    Found memtest86+ image: /memtest86+.bin
    done

<span data-ttu-id="3915a-180">Hello Red Hat 發佈系列，您只需要 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="3915a-180">For hello Red Hat distribution family, you need only hello following command:</span></span>

    echo 'echo noop >/sys/block/sda/queue/scheduler' >> /etc/rc.local

## <a name="configure-system-file-operations-settings"></a><span data-ttu-id="3915a-181">設定系統檔案作業設定</span><span class="sxs-lookup"><span data-stu-id="3915a-181">Configure system file operations settings</span></span>
<span data-ttu-id="3915a-182">一個最佳作法是 toodisable hello *atime* hello 檔案系統上的記錄功能。</span><span class="sxs-lookup"><span data-stu-id="3915a-182">One best practice is toodisable hello *atime* logging feature on hello file system.</span></span> <span data-ttu-id="3915a-183">Atime 是 hello 上次檔案存取時間。</span><span class="sxs-lookup"><span data-stu-id="3915a-183">Atime is hello last file access time.</span></span> <span data-ttu-id="3915a-184">存取檔案，每當 hello 檔案系統記錄 hello hello 記錄檔中的時間戳記。</span><span class="sxs-lookup"><span data-stu-id="3915a-184">Whenever a file is accessed, hello file system records hello timestamp in hello log.</span></span> <span data-ttu-id="3915a-185">不過，很少使用這項資訊。</span><span class="sxs-lookup"><span data-stu-id="3915a-185">However, this information is rarely used.</span></span> <span data-ttu-id="3915a-186">如果您不需要它，可予以停用，將會減少整體的磁碟存取時間。</span><span class="sxs-lookup"><span data-stu-id="3915a-186">You can disable it if you don't need it, which will reduce overall disk access time.</span></span>  

<span data-ttu-id="3915a-187">toodisable atime 記錄，您需要 toomodify hello 檔案系統的組態檔 /etc/ fstab 並新增 hello **noatime**選項。</span><span class="sxs-lookup"><span data-stu-id="3915a-187">toodisable atime logging, you need toomodify hello file system configuration file /etc/ fstab and add hello **noatime** option.</span></span>  

<span data-ttu-id="3915a-188">例如，編輯 hello vim /etc/fstab 檔案，新增 hello noatime hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="3915a-188">For example, edit hello vim /etc/fstab file, adding hello noatime as shown in hello following sample:</span></span>  

    # CLOUD_IMG: This file was created/modified by hello Cloud Image build process
    UUID=3cc98c06-d649-432d-81df-6dcd2a584d41       /        ext4   defaults,discard        0 0
    #Add hello “noatime” option below toodisable atime logging
    UUID="431b1e78-8226-43ec-9460-514a9adf060e"     /RAID0   xfs   defaults,nobootwait, noatime 0 0
    /dev/sdb1       /mnt    auto    defaults,nobootwait,comment=cloudconfig 0       2

<span data-ttu-id="3915a-189">然後，重新 hello 檔案系統掛接具有 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="3915a-189">Then, remount hello file system with hello following command:</span></span>  

    mount -o remount /RAID0

<span data-ttu-id="3915a-190">測試 hello 修改結果。</span><span class="sxs-lookup"><span data-stu-id="3915a-190">Test hello modified result.</span></span> <span data-ttu-id="3915a-191">當您修改 hello 測試檔案時，不會更新 hello 存取時間。</span><span class="sxs-lookup"><span data-stu-id="3915a-191">When you modify hello test file, hello access time is not updated.</span></span> <span data-ttu-id="3915a-192">下列範例會顯示哪些 hello 程式碼看起來像，修改前後的 hello。</span><span class="sxs-lookup"><span data-stu-id="3915a-192">hello following examples show what hello code looks like before and after modification.</span></span>

<span data-ttu-id="3915a-193">之前：</span><span class="sxs-lookup"><span data-stu-id="3915a-193">Before:</span></span>        

![存取修改前的程式碼][5]

<span data-ttu-id="3915a-195">之後︰</span><span class="sxs-lookup"><span data-stu-id="3915a-195">After:</span></span>

![存取修改後的程式碼][6]

## <a name="increase-hello-maximum-number-of-system-handles-for-high-concurrency"></a><span data-ttu-id="3915a-197">增加 hello 系統的高並行處理的控制代碼的數目上限</span><span class="sxs-lookup"><span data-stu-id="3915a-197">Increase hello maximum number of system handles for high concurrency</span></span>
<span data-ttu-id="3915a-198">MySQL 是高並行存取資料庫。</span><span class="sxs-lookup"><span data-stu-id="3915a-198">MySQL is a high concurrency database.</span></span> <span data-ttu-id="3915a-199">並行控制代碼的 hello 預設數目為 1024，對於 Linux，這並不足夠。</span><span class="sxs-lookup"><span data-stu-id="3915a-199">hello default number of concurrent handles is 1024 for Linux, which is not always sufficient.</span></span> <span data-ttu-id="3915a-200">使用下列步驟 tooincrease hello 最大並行控制代碼的 MySQL 的 hello 系統 toosupport 高並行的 hello。</span><span class="sxs-lookup"><span data-stu-id="3915a-200">Use hello following steps tooincrease hello maximum concurrent handles of hello system toosupport high concurrency of MySQL.</span></span>

### <a name="modify-hello-limitsconf-file"></a><span data-ttu-id="3915a-201">修改 hello limits.conf 檔案</span><span class="sxs-lookup"><span data-stu-id="3915a-201">Modify hello limits.conf file</span></span>
<span data-ttu-id="3915a-202">tooincrease hello 最大允許並行的控制代碼，並將下列四個線條 hello /etc/security/limits.conf 檔案中的 hello。</span><span class="sxs-lookup"><span data-stu-id="3915a-202">tooincrease hello maximum allowed concurrent handles, add hello following four lines in hello /etc/security/limits.conf file.</span></span> <span data-ttu-id="3915a-203">請注意，65536 hello hello 系統可支援的最大數目。</span><span class="sxs-lookup"><span data-stu-id="3915a-203">Note that 65536 is hello maximum number that hello system can support.</span></span>   

    * <span data-ttu-id="3915a-204">soft nofile 65536</span><span class="sxs-lookup"><span data-stu-id="3915a-204">soft nofile 65536</span></span>
    * <span data-ttu-id="3915a-205">hard nofile 65536</span><span class="sxs-lookup"><span data-stu-id="3915a-205">hard nofile 65536</span></span>
    * <span data-ttu-id="3915a-206">soft nproc 65536</span><span class="sxs-lookup"><span data-stu-id="3915a-206">soft nproc 65536</span></span>
    * <span data-ttu-id="3915a-207">hard nproc 65536</span><span class="sxs-lookup"><span data-stu-id="3915a-207">hard nproc 65536</span></span>

### <a name="update-hello-system-for-hello-new-limits"></a><span data-ttu-id="3915a-208">更新 hello 新限制的 hello 系統</span><span class="sxs-lookup"><span data-stu-id="3915a-208">Update hello system for hello new limits</span></span>
<span data-ttu-id="3915a-209">tooupdate hello 系統，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="3915a-209">tooupdate hello system, run hello following commands:</span></span>  

    ulimit -SHn 65536
    ulimit -SHu 65536

### <a name="ensure-that-hello-limits-are-updated-at-boot-time"></a><span data-ttu-id="3915a-210">請確定在開機時，會更新 hello 限制</span><span class="sxs-lookup"><span data-stu-id="3915a-210">Ensure that hello limits are updated at boot time</span></span>
<span data-ttu-id="3915a-211">Put 的 hello 遵循 hello /etc/rc.local 檔案中的啟動命令，如此它在開機時才會生效。</span><span class="sxs-lookup"><span data-stu-id="3915a-211">Put hello following startup commands in hello /etc/rc.local file so it will take effect at boot time.</span></span>  

    echo “ulimit -SHn 65536” >>/etc/rc.local
    echo “ulimit -SHu 65536” >>/etc/rc.local

## <a name="mysql-database-optimization"></a><span data-ttu-id="3915a-212">MySQL 資料庫最佳化</span><span class="sxs-lookup"><span data-stu-id="3915a-212">MySQL database optimization</span></span>
<span data-ttu-id="3915a-213">您可以使用 tooconfigure 在 Azure 上 MySQL，hello 您在內部部署電腦使用相同的效能調整的策略。</span><span class="sxs-lookup"><span data-stu-id="3915a-213">tooconfigure MySQL on Azure, you can use hello same performance-tuning strategy you use on an on-premises machine.</span></span>  

<span data-ttu-id="3915a-214">hello 主要 I/O 最佳化規則如下：</span><span class="sxs-lookup"><span data-stu-id="3915a-214">hello main I/O optimization rules are:</span></span>   

* <span data-ttu-id="3915a-215">Hello 快取大小增加。</span><span class="sxs-lookup"><span data-stu-id="3915a-215">Increase hello cache size.</span></span>
* <span data-ttu-id="3915a-216">減少 I/O 回應時間。</span><span class="sxs-lookup"><span data-stu-id="3915a-216">Reduce I/O response time.</span></span>  

<span data-ttu-id="3915a-217">toooptimize MySQL 伺服器的設定，您可以更新 hello my.cnf 檔案，這是伺服器和用戶端電腦的 hello 預設組態檔。</span><span class="sxs-lookup"><span data-stu-id="3915a-217">toooptimize MySQL server settings, you can update hello my.cnf file, which is hello default configuration file for both server and client computers.</span></span>  

<span data-ttu-id="3915a-218">hello 下列設定項目是 hello 影響 MySQL 效能的主要因素：</span><span class="sxs-lookup"><span data-stu-id="3915a-218">hello following configuration items are hello main factors that affect MySQL performance:</span></span>  

* <span data-ttu-id="3915a-219">**innodb_buffer_pool_size**: hello 緩衝集區包含經過緩衝處理的資料與 hello 索引。</span><span class="sxs-lookup"><span data-stu-id="3915a-219">**innodb_buffer_pool_size**: hello buffer pool contains buffered data and hello index.</span></span> <span data-ttu-id="3915a-220">此設定通常 too70 的實體記憶體的百分比。</span><span class="sxs-lookup"><span data-stu-id="3915a-220">This is usually set too70 percent of physical memory.</span></span>
* <span data-ttu-id="3915a-221">**innodb_log_file_size**： 這是 hello 重做記錄檔大小。</span><span class="sxs-lookup"><span data-stu-id="3915a-221">**innodb_log_file_size**: This is hello redo log size.</span></span> <span data-ttu-id="3915a-222">您使用的寫入作業將會快速、 可靠且可復原損毀之後的重做記錄檔 tooensure。</span><span class="sxs-lookup"><span data-stu-id="3915a-222">You use redo logs tooensure that write operations are fast, reliable, and recoverable after a crash.</span></span> <span data-ttu-id="3915a-223">這會設定 too512 MB，這樣會提供您足夠的空間的寫入作業記錄。</span><span class="sxs-lookup"><span data-stu-id="3915a-223">This is set too512 MB, which will give you plenty of space for logging write operations.</span></span>
* <span data-ttu-id="3915a-224">**max_connections**：應用程式有時不會正確關閉連線。</span><span class="sxs-lookup"><span data-stu-id="3915a-224">**max_connections**: Sometimes applications do not close connections properly.</span></span> <span data-ttu-id="3915a-225">較大的值會讓伺服器 hello toorecycle 閒置連線的更多時間。</span><span class="sxs-lookup"><span data-stu-id="3915a-225">A larger value will give hello server more time toorecycle idled connections.</span></span> <span data-ttu-id="3915a-226">hello 的連線數目上限為 10000，但是 hello 建議的最大值是 5000。</span><span class="sxs-lookup"><span data-stu-id="3915a-226">hello maximum number of connections is 10,000, but hello recommended maximum is 5,000.</span></span>
* <span data-ttu-id="3915a-227">**Innodb_file_per_table**： 此設定啟用或停用 hello 能力 InnoDB toostore 資料表在個別的檔案。</span><span class="sxs-lookup"><span data-stu-id="3915a-227">**Innodb_file_per_table**: This setting enables or disables hello ability of InnoDB toostore tables in separate files.</span></span> <span data-ttu-id="3915a-228">開啟 hello 選項 tooensure 可以有效地套用數個進階的管理作業。</span><span class="sxs-lookup"><span data-stu-id="3915a-228">Turn on hello option tooensure that several advanced administration operations can be applied efficiently.</span></span> <span data-ttu-id="3915a-229">從效能觀點來看，它可以加速 hello 資料表空間傳輸，並將 hello 瓦礫管理效能最佳化。</span><span class="sxs-lookup"><span data-stu-id="3915a-229">From a performance point of view, it can speed up hello table space transmission and optimize hello debris management performance.</span></span> <span data-ttu-id="3915a-230">hello 建議使用這個選項的設定是 ON。</span><span class="sxs-lookup"><span data-stu-id="3915a-230">hello recommended setting for this option is ON.</span></span></br></br>
<span data-ttu-id="3915a-231">從 MySQL 5.6 hello 預設設定是 ON，因此不不需要任何動作。</span><span class="sxs-lookup"><span data-stu-id="3915a-231">From MySQL 5.6, hello default setting is ON, so no action is required.</span></span> <span data-ttu-id="3915a-232">針對先前的版本，hello 預設設定為 OFF。</span><span class="sxs-lookup"><span data-stu-id="3915a-232">For earlier versions, hello default setting is OFF.</span></span> <span data-ttu-id="3915a-233">hello 應該變更設定之前已載入資料，因為只有新建立的資料表會受到影響。</span><span class="sxs-lookup"><span data-stu-id="3915a-233">hello setting should be changed before data is loaded, because only newly created tables are affected.</span></span>
* <span data-ttu-id="3915a-234">**innodb_flush_log_at_trx_commit**: hello 預設值為 1，以 hello 範圍設定 too0 ~ 2。</span><span class="sxs-lookup"><span data-stu-id="3915a-234">**innodb_flush_log_at_trx_commit**: hello default value is 1, with hello scope set too0~2.</span></span> <span data-ttu-id="3915a-235">hello 預設值為 hello 獨立 MySQL 資料庫最適合的選項。</span><span class="sxs-lookup"><span data-stu-id="3915a-235">hello default value is hello most suitable option for standalone MySQL DB.</span></span> <span data-ttu-id="3915a-236">hello 設定 2 啟用 hello 大部分的資料完整性，並適用於 MySQL 的叢集中的主機。</span><span class="sxs-lookup"><span data-stu-id="3915a-236">hello setting of 2 enables hello most data integrity and is suitable for Master in MySQL Cluster.</span></span> <span data-ttu-id="3915a-237">hello 值為 0 可讓資料遺失，可能會影響可靠性 （在某些情況下，效能更佳），以及適用於 MySQL 的叢集中的從屬版本。</span><span class="sxs-lookup"><span data-stu-id="3915a-237">hello setting of 0 allows data loss, which can affect reliability (in some cases with better performance), and is suitable for Slave in MySQL Cluster.</span></span>
* <span data-ttu-id="3915a-238">**Innodb_log_buffer_size**: hello 記錄緩衝區而不需要 tooflush hello 記錄 toodisk hello 交易認可之前允許交易 toorun。</span><span class="sxs-lookup"><span data-stu-id="3915a-238">**Innodb_log_buffer_size**: hello log buffer allows transactions toorun without having tooflush hello log toodisk before hello transactions commit.</span></span> <span data-ttu-id="3915a-239">不過，如果沒有大型二進位物件或文字欄位，hello 快取將會快速耗盡，而且經常磁碟 I/O，將會觸發。</span><span class="sxs-lookup"><span data-stu-id="3915a-239">However, if there is large binary object or text field, hello cache will be consumed quickly and frequent disk I/O will be triggered.</span></span> <span data-ttu-id="3915a-240">它是進一步增加 hello 的緩衝區大小，如果 Innodb_log_waits 狀態變數不是 0。</span><span class="sxs-lookup"><span data-stu-id="3915a-240">It is better increase hello buffer size if Innodb_log_waits state variable is not 0.</span></span>
* <span data-ttu-id="3915a-241">**query_cache_size**: hello 最好的選擇是 toodisable 從 hello 開始。</span><span class="sxs-lookup"><span data-stu-id="3915a-241">**query_cache_size**: hello best option is toodisable it from hello outset.</span></span> <span data-ttu-id="3915a-242">設定 query_cache_size too0 （這是 MySQL 5.6 hello 預設設定），並使用其他的方法 toospeed 機操作查詢。</span><span class="sxs-lookup"><span data-stu-id="3915a-242">Set query_cache_size too0 (this is hello default setting in MySQL 5.6) and use other methods toospeed up queries.</span></span>  

<span data-ttu-id="3915a-243">請參閱[附錄 D](#AppendixD)前後 hello 最佳化效能的比較。</span><span class="sxs-lookup"><span data-stu-id="3915a-243">See [Appendix D](#AppendixD) for a comparison of performance before and after hello optimization.</span></span>

## <a name="turn-on-hello-mysql-slow-query-log-for-analyzing-hello-performance-bottleneck"></a><span data-ttu-id="3915a-244">開啟分析 hello 效能瓶頸的 hello MySQL 慢速查詢記錄檔</span><span class="sxs-lookup"><span data-stu-id="3915a-244">Turn on hello MySQL slow query log for analyzing hello performance bottleneck</span></span>
<span data-ttu-id="3915a-245">hello MySQL 慢速查詢記錄檔可協助您識別用於 MySQL 的 hello 慢速查詢。</span><span class="sxs-lookup"><span data-stu-id="3915a-245">hello MySQL slow query log can help you identify hello slow queries for MySQL.</span></span> <span data-ttu-id="3915a-246">啟用 hello MySQL 慢速查詢記錄檔之後，您可以使用 MySQL 工具，像是**mysqldumpslow** tooidentify hello 效能瓶頸。</span><span class="sxs-lookup"><span data-stu-id="3915a-246">After enabling hello MySQL slow query log, you can use MySQL tools like **mysqldumpslow** tooidentify hello performance bottleneck.</span></span>  

<span data-ttu-id="3915a-247">預設不會啟用此項目。</span><span class="sxs-lookup"><span data-stu-id="3915a-247">By default, this is not enabled.</span></span> <span data-ttu-id="3915a-248">開啟 hello 慢速查詢記錄檔可能會耗用一些 CPU 資源。</span><span class="sxs-lookup"><span data-stu-id="3915a-248">Turning on hello slow query log might consume some CPU resources.</span></span> <span data-ttu-id="3915a-249">我們建議您暫時啟用這個選項，以便排解效能瓶頸。</span><span class="sxs-lookup"><span data-stu-id="3915a-249">We recommend that you enable this temporarily for troubleshooting performance bottlenecks.</span></span> <span data-ttu-id="3915a-250">tooturn hello 慢速查詢記錄檔：</span><span class="sxs-lookup"><span data-stu-id="3915a-250">tooturn on hello slow query log:</span></span>

1. <span data-ttu-id="3915a-251">修改 hello my.cnf 檔案有新增下列幾行 toohello 結束 hello:</span><span class="sxs-lookup"><span data-stu-id="3915a-251">Modify hello my.cnf file by adding hello following lines toohello end:</span></span>

        long_query_time = 2
        slow_query_log = 1
        slow_query_log_file = /RAID0/mysql/mysql-slow.log

2. <span data-ttu-id="3915a-252">重新啟動 hello MySQL 伺服器。</span><span class="sxs-lookup"><span data-stu-id="3915a-252">Restart hello MySQL server.</span></span>

        service  mysql  restart

3. <span data-ttu-id="3915a-253">檢查是否 hello 設定生效使用 hello**顯示**命令。</span><span class="sxs-lookup"><span data-stu-id="3915a-253">Check whether hello setting is taking effect by using hello **show** command.</span></span>

![Slow-query-log ON][7]   

![Slow-query-log 結果][8]

<span data-ttu-id="3915a-256">在此範例中，您可以查看已開啟該 hello 緩慢的查詢功能。</span><span class="sxs-lookup"><span data-stu-id="3915a-256">In this example, you can see that hello slow query feature has been turned on.</span></span> <span data-ttu-id="3915a-257">然後，您可以使用 hello **mysqldumpslow**工具 toodetermine 效能瓶頸，並最佳化效能，例如加入索引。</span><span class="sxs-lookup"><span data-stu-id="3915a-257">You can then use hello **mysqldumpslow** tool toodetermine performance bottlenecks and optimize performance, such as adding indexes.</span></span>

## <a name="appendices"></a><span data-ttu-id="3915a-258">附錄</span><span class="sxs-lookup"><span data-stu-id="3915a-258">Appendices</span></span>
<span data-ttu-id="3915a-259">hello 以下是在目標的實驗室環境中所產生的範例效能測試資料。</span><span class="sxs-lookup"><span data-stu-id="3915a-259">hello following are sample performance test data produced in a targeted lab environment.</span></span> <span data-ttu-id="3915a-260">提供在 hello 效能資料趨勢的一般背景，具有不同的效能微調方法。</span><span class="sxs-lookup"><span data-stu-id="3915a-260">They provide general background on hello performance data trend with different performance tuning approaches.</span></span> <span data-ttu-id="3915a-261">hello 結果可能會因不同的環境或產品版本而異。</span><span class="sxs-lookup"><span data-stu-id="3915a-261">hello results might vary under different environment or product versions.</span></span>

### <span data-ttu-id="3915a-262"><a name="AppendixA"></a>附錄 A</span><span class="sxs-lookup"><span data-stu-id="3915a-262"><a name="AppendixA"></a>Appendix A</span></span>  
<span data-ttu-id="3915a-263">**不同 RAID 層級的磁碟效能 (IOPS)**</span><span class="sxs-lookup"><span data-stu-id="3915a-263">**Disk performance (IOPS) with different RAID levels**</span></span>

![不同 RAID 層級的磁碟 IOPS][9]

<span data-ttu-id="3915a-265">**測試命令**</span><span class="sxs-lookup"><span data-stu-id="3915a-265">**Test commands**</span></span>  

    fio -filename=/path/test -iodepth=64 -ioengine=libaio -direct=1 -rw=randwrite -bs=4k -size=5G -numjobs=64 -runtime=30 -group_reporting -name=test-randwrite

> [!NOTE]
> <span data-ttu-id="3915a-266">hello 工作負載的這項測試會使用 64 個執行緒，嘗試的 RAID tooreach hello 時間上限。</span><span class="sxs-lookup"><span data-stu-id="3915a-266">hello workload of this test uses 64 threads, trying tooreach hello upper limit of RAID.</span></span>
>
>

### <span data-ttu-id="3915a-267"><a name="AppendixB"></a>附錄 B</span><span class="sxs-lookup"><span data-stu-id="3915a-267"><a name="AppendixB"></a>Appendix B</span></span>  
<span data-ttu-id="3915a-268">**不同 RAID 層級的 MySQL 效能 (輸送量) 比較** </span><span class="sxs-lookup"><span data-stu-id="3915a-268">**MySQL performance (throughput) comparison with different RAID levels** </span></span>  
<span data-ttu-id="3915a-269">(XFS檔案系統)</span><span class="sxs-lookup"><span data-stu-id="3915a-269">(XFS file system)</span></span>

![不同 RAID 層級的 MySQL 效能比較][10]  
![不同 RAID 層級的 MySQL 效能比較][11]

<span data-ttu-id="3915a-272">**測試命令**</span><span class="sxs-lookup"><span data-stu-id="3915a-272">**Test commands**</span></span>

    mysqlslap -p0ps.123 --concurrency=2 --iterations=1 --number-int-cols=10 --number-char-cols=10 -a --auto-generate-sql-guid-primary --number-of-queries=10000 --auto-generate-sql-load-type=write –engine=innodb

<span data-ttu-id="3915a-273">**不同 RAID 層級的 MySQL 效能 (OLTP) 比較**</span><span class="sxs-lookup"><span data-stu-id="3915a-273">**MySQL performance (OLTP) comparison with different RAID levels**</span></span>  
<span data-ttu-id="3915a-274">![不同 RAID 層級的 MySQL 效能 (OLTP) 比較][12]</span><span class="sxs-lookup"><span data-stu-id="3915a-274">![MySQL performance (OLTP) comparison with different RAID levels][12]</span></span>

<span data-ttu-id="3915a-275">**測試命令**</span><span class="sxs-lookup"><span data-stu-id="3915a-275">**Test commands**</span></span>

    time sysbench --test=oltp --db-driver=mysql --mysql-user=root --mysql-password=0ps.123  --mysql-table-engine=innodb --mysql-host=127.0.0.1 --mysql-port=3306 --mysql-socket=/var/run/mysqld/mysqld.sock --mysql-db=test --oltp-table-size=1000000 prepare

### <span data-ttu-id="3915a-276"><a name="AppendixC"></a>附錄 C</span><span class="sxs-lookup"><span data-stu-id="3915a-276"><a name="AppendixC"></a>Appendix C</span></span>   
<span data-ttu-id="3915a-277">**不同區塊大小的磁碟效能 (IOPS) 比較**</span><span class="sxs-lookup"><span data-stu-id="3915a-277">**Disk performance (IOPS) comparison for different chunk sizes**</span></span>  
<span data-ttu-id="3915a-278">(XFS檔案系統)</span><span class="sxs-lookup"><span data-stu-id="3915a-278">(XFS file system)</span></span>

![][13]

<span data-ttu-id="3915a-279">**測試命令**</span><span class="sxs-lookup"><span data-stu-id="3915a-279">**Test commands**</span></span>  

    fio -filename=/path/test -iodepth=64 -ioengine=libaio -direct=1 -rw=randwrite -bs=4k -size=30G -numjobs=64 -runtime=30 -group_reporting -name=test-randwrite
    fio -filename=/path/test -iodepth=64 -ioengine=libaio -direct=1 -rw=randwrite -bs=4k -size=1G -numjobs=64 -runtime=30 -group_reporting -name=test-randwrite  

<span data-ttu-id="3915a-280">使用這項測試的 hello 檔案大小 30 GB 和 1 GB，分別為，與 RAID 0 （4 個磁碟） XFS 檔案系統。</span><span class="sxs-lookup"><span data-stu-id="3915a-280">hello file sizes used for this testing are 30 GB and 1 GB, respectively, with RAID 0 (4 disks) XFS file system.</span></span>

### <span data-ttu-id="3915a-281"><a name="AppendixD"></a>附錄 D</span><span class="sxs-lookup"><span data-stu-id="3915a-281"><a name="AppendixD"></a>Appendix D</span></span>  
<span data-ttu-id="3915a-282">**最佳化之前和之後的 MySQL 效能 (輸送量) 比較**</span><span class="sxs-lookup"><span data-stu-id="3915a-282">**MySQL performance (throughput) comparison before and after optimization**</span></span>  
<span data-ttu-id="3915a-283">(XFS檔案系統)</span><span class="sxs-lookup"><span data-stu-id="3915a-283">(XFS File System)</span></span>

![最佳化之前和之後的 MySQL 效能 (輸送量) 比較][14]

<span data-ttu-id="3915a-285">**測試命令**</span><span class="sxs-lookup"><span data-stu-id="3915a-285">**Test commands**</span></span>

    mysqlslap -p0ps.123 --concurrency=2 --iterations=1 --number-int-cols=10 --number-char-cols=10 -a --auto-generate-sql-guid-primary --number-of-queries=10000 --auto-generate-sql-load-type=write –engine=innodb,misam

<span data-ttu-id="3915a-286">**預設和最佳化 hello 組態設定如下所示：**</span><span class="sxs-lookup"><span data-stu-id="3915a-286">**hello configuration setting for default and optimization is as follows:**</span></span>

| <span data-ttu-id="3915a-287">參數</span><span class="sxs-lookup"><span data-stu-id="3915a-287">Parameters</span></span> | <span data-ttu-id="3915a-288">預設值</span><span class="sxs-lookup"><span data-stu-id="3915a-288">Default</span></span> | <span data-ttu-id="3915a-289">最佳化</span><span class="sxs-lookup"><span data-stu-id="3915a-289">Optimization</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3915a-290">**innodb_buffer_pool_size**</span><span class="sxs-lookup"><span data-stu-id="3915a-290">**innodb_buffer_pool_size**</span></span> |<span data-ttu-id="3915a-291">None</span><span class="sxs-lookup"><span data-stu-id="3915a-291">None</span></span> |<span data-ttu-id="3915a-292">7 GB</span><span class="sxs-lookup"><span data-stu-id="3915a-292">7 GB</span></span> |
| <span data-ttu-id="3915a-293">**innodb_log_file_size**</span><span class="sxs-lookup"><span data-stu-id="3915a-293">**innodb_log_file_size**</span></span> |<span data-ttu-id="3915a-294">5 MB</span><span class="sxs-lookup"><span data-stu-id="3915a-294">5 MB</span></span> |<span data-ttu-id="3915a-295">512 MB</span><span class="sxs-lookup"><span data-stu-id="3915a-295">512 MB</span></span> |
| <span data-ttu-id="3915a-296">**max_connections**</span><span class="sxs-lookup"><span data-stu-id="3915a-296">**max_connections**</span></span> |<span data-ttu-id="3915a-297">100</span><span class="sxs-lookup"><span data-stu-id="3915a-297">100</span></span> |<span data-ttu-id="3915a-298">5000</span><span class="sxs-lookup"><span data-stu-id="3915a-298">5000</span></span> |
| <span data-ttu-id="3915a-299">**innodb_file_per_table**</span><span class="sxs-lookup"><span data-stu-id="3915a-299">**innodb_file_per_table**</span></span> |<span data-ttu-id="3915a-300">0</span><span class="sxs-lookup"><span data-stu-id="3915a-300">0</span></span> |<span data-ttu-id="3915a-301">1</span><span class="sxs-lookup"><span data-stu-id="3915a-301">1</span></span> |
| <span data-ttu-id="3915a-302">**innodb_flush_log_at_trx_commit**</span><span class="sxs-lookup"><span data-stu-id="3915a-302">**innodb_flush_log_at_trx_commit**</span></span> |<span data-ttu-id="3915a-303">1</span><span class="sxs-lookup"><span data-stu-id="3915a-303">1</span></span> |<span data-ttu-id="3915a-304">2</span><span class="sxs-lookup"><span data-stu-id="3915a-304">2</span></span> |
| <span data-ttu-id="3915a-305">**innodb_log_buffer_size**</span><span class="sxs-lookup"><span data-stu-id="3915a-305">**innodb_log_buffer_size**</span></span> |<span data-ttu-id="3915a-306">8 MB</span><span class="sxs-lookup"><span data-stu-id="3915a-306">8 MB</span></span> |<span data-ttu-id="3915a-307">128 MB</span><span class="sxs-lookup"><span data-stu-id="3915a-307">128 MB</span></span> |
| <span data-ttu-id="3915a-308">**query_cache_size**</span><span class="sxs-lookup"><span data-stu-id="3915a-308">**query_cache_size**</span></span> |<span data-ttu-id="3915a-309">16 MB</span><span class="sxs-lookup"><span data-stu-id="3915a-309">16 MB</span></span> |<span data-ttu-id="3915a-310">0</span><span class="sxs-lookup"><span data-stu-id="3915a-310">0</span></span> |

<span data-ttu-id="3915a-311">更多詳細的[最佳化組態參數](http://dev.mysql.com/doc/refman/5.6/en/innodb-configuration.html)，請參閱 toohello [MySQL 官方指示](http://dev.mysql.com/doc/refman/5.6/en/innodb-parameters.html#sysvar_innodb_flush_method)。</span><span class="sxs-lookup"><span data-stu-id="3915a-311">For more detailed [optimization configuration parameters](http://dev.mysql.com/doc/refman/5.6/en/innodb-configuration.html), refer toohello [MySQL official instructions](http://dev.mysql.com/doc/refman/5.6/en/innodb-parameters.html#sysvar_innodb_flush_method).</span></span>  

  <span data-ttu-id="3915a-312">**測試環境**</span><span class="sxs-lookup"><span data-stu-id="3915a-312">**Test environment**</span></span>  

| <span data-ttu-id="3915a-313">硬體</span><span class="sxs-lookup"><span data-stu-id="3915a-313">Hardware</span></span> | <span data-ttu-id="3915a-314">詳細資料</span><span class="sxs-lookup"><span data-stu-id="3915a-314">Details</span></span> |
| --- | --- |
| <span data-ttu-id="3915a-315">CPU</span><span class="sxs-lookup"><span data-stu-id="3915a-315">CPU</span></span> |<span data-ttu-id="3915a-316">AMD Opteron(tm) 處理器 4171 HE/4 核心</span><span class="sxs-lookup"><span data-stu-id="3915a-316">AMD Opteron(tm) Processor 4171 HE/4 cores</span></span> |
| <span data-ttu-id="3915a-317">記憶體</span><span class="sxs-lookup"><span data-stu-id="3915a-317">Memory</span></span> |<span data-ttu-id="3915a-318">14 GB</span><span class="sxs-lookup"><span data-stu-id="3915a-318">14 GB</span></span> |
| <span data-ttu-id="3915a-319">磁碟</span><span class="sxs-lookup"><span data-stu-id="3915a-319">Disk</span></span> |<span data-ttu-id="3915a-320">10 GB/磁碟</span><span class="sxs-lookup"><span data-stu-id="3915a-320">10 GB/disk</span></span> |
| <span data-ttu-id="3915a-321">作業系統</span><span class="sxs-lookup"><span data-stu-id="3915a-321">OS</span></span> |<span data-ttu-id="3915a-322">Ubuntu 14.04.1 LTS</span><span class="sxs-lookup"><span data-stu-id="3915a-322">Ubuntu 14.04.1 LTS</span></span> |

[1]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-01.png
[2]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-02.png
[3]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-03.png
[4]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-04.png
[5]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-05.png
[6]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-06.png
[7]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-07.png
[8]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-08.png
[9]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-09.png
[10]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-10.png
[11]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-11.png
[12]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-12.png
[13]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-13.png
[14]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-14.png

