---
title: "在 Azure Linux 上最佳化 MySQL 效能 | Microsoft Docs"
description: "了解如何最佳化在執行 Linux 之 Azure 虛擬機器 (VM) 上執行的 MySQL。"
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
ms.openlocfilehash: 8f2ec884fa98e989448ac11675e71f39aa21fa7f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="optimize-mysql-performance-on-azure-linux-vms"></a><span data-ttu-id="77258-103">在 Azure Linux 上最佳化 MySQL 效能</span><span class="sxs-lookup"><span data-stu-id="77258-103">Optimize MySQL Performance on Azure Linux VMs</span></span>
<span data-ttu-id="77258-104">有許多因素會影響 Azure 上的 MySQL 效能，均與虛擬硬體選取和軟體設定有關。</span><span class="sxs-lookup"><span data-stu-id="77258-104">There are many factors that affect MySQL performance on Azure, both in virtual hardware selection and software configuration.</span></span> <span data-ttu-id="77258-105">本文著重於透過儲存體、系統和資料庫設定最佳化效能。</span><span class="sxs-lookup"><span data-stu-id="77258-105">This article focuses on optimizing performance through storage, system, and database configurations.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="77258-106">Azure 建立和處理資源的部署模型有兩種：[Azure Resource Manager](../../../resource-manager-deployment-model.md) 和傳統。</span><span class="sxs-lookup"><span data-stu-id="77258-106">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager](../../../resource-manager-deployment-model.md) and classic.</span></span> <span data-ttu-id="77258-107">本文涵蓋之內容包括使用傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="77258-107">This article covers using the classic deployment model.</span></span> <span data-ttu-id="77258-108">Microsoft 建議讓大部分的新部署使用資源管理員模式。</span><span class="sxs-lookup"><span data-stu-id="77258-108">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="77258-109">如需使用 Resource Manager 模型進行 Linux VM 最佳化的詳細資訊，請參閱[在 Azure 上最佳化您的 Linux VM](../optimization.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="77258-109">For information about Linux VM optimizations with the Resource Manager model, see [Optimize your Linux VM on Azure](../optimization.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="utilize-raid-on-an-azure-virtual-machine"></a><span data-ttu-id="77258-110">在 Azure 虛擬機器上利用 RAID</span><span class="sxs-lookup"><span data-stu-id="77258-110">Utilize RAID on an Azure virtual machine</span></span>
<span data-ttu-id="77258-111">儲存體是影響雲端環境中的資料庫效能的關鍵因素。</span><span class="sxs-lookup"><span data-stu-id="77258-111">Storage is the key factor that affects database performance in cloud environments.</span></span> <span data-ttu-id="77258-112">相較於單一磁碟，RAID 可透過並行提供更快速的存取。</span><span class="sxs-lookup"><span data-stu-id="77258-112">Compared to a single disk, RAID can provide faster access via concurrency.</span></span> <span data-ttu-id="77258-113">如需詳細資訊，請參閱[標準 RAID 層級](http://en.wikipedia.org/wiki/Standard_RAID_levels)。</span><span class="sxs-lookup"><span data-stu-id="77258-113">For more information, see [Standard RAID levels](http://en.wikipedia.org/wiki/Standard_RAID_levels).</span></span>   

<span data-ttu-id="77258-114">可透過 RAID 改進 Azure 中的磁碟 I/O 輸送量和 I/O 回應時間。</span><span class="sxs-lookup"><span data-stu-id="77258-114">Disk I/O throughput and I/O response time in Azure can be improved through RAID.</span></span> <span data-ttu-id="77258-115">我們的實驗室測試顯示︰當 RAID 磁碟數目增加一倍 (從 2 到 4、4 到 8 等) 時，磁碟 I/O 輸送量可以增加一倍，而 I/O 回應時間則平均減少一半。</span><span class="sxs-lookup"><span data-stu-id="77258-115">Our lab tests show that disk I/O throughput can be doubled and I/O response time can be reduced by half on average when the number of RAID disks is doubled (from two to four, four to eight, etc.).</span></span> <span data-ttu-id="77258-116">如需詳細資訊，請參閱 [附錄 A](#AppendixA) 。</span><span class="sxs-lookup"><span data-stu-id="77258-116">See [Appendix A](#AppendixA) for details.</span></span>  

<span data-ttu-id="77258-117">除了磁碟 I/O 以外，MySQL 效能會在您提高 RAID 層級時改善。</span><span class="sxs-lookup"><span data-stu-id="77258-117">In addition to disk I/O, MySQL performance improves when you increase the RAID level.</span></span>  <span data-ttu-id="77258-118">如需詳細資訊，請參閱 [附錄 B](#AppendixB) 。</span><span class="sxs-lookup"><span data-stu-id="77258-118">See [Appendix B](#AppendixB) for details.</span></span>  

<span data-ttu-id="77258-119">您也可能要考慮區塊大小。</span><span class="sxs-lookup"><span data-stu-id="77258-119">You might also want to consider the chunk size.</span></span> <span data-ttu-id="77258-120">通常當您有較大的區塊大小時，您的額外負荷會比較低，尤其是大量寫入時。</span><span class="sxs-lookup"><span data-stu-id="77258-120">In general, when you have a larger chunk size, you get lower overhead, especially for large writes.</span></span> <span data-ttu-id="77258-121">不過，當區塊大小太大時，可能會增加額外的負荷，進而使您無法利用 RAID。</span><span class="sxs-lookup"><span data-stu-id="77258-121">However, when the chunk size is too large, it might add additional overhead that prevents you from taking advantage of RAID.</span></span> <span data-ttu-id="77258-122">目前的預設大小為 512 KB，經證明是大多數一般實際執行環境的最佳大小。</span><span class="sxs-lookup"><span data-stu-id="77258-122">The current default size is 512 KB, which is proven to be optimal for most general production environments.</span></span> <span data-ttu-id="77258-123">如需詳細資訊，請參閱 [附錄 C](#AppendixC) 。</span><span class="sxs-lookup"><span data-stu-id="77258-123">See [Appendix C](#AppendixC) for details.</span></span>   

<span data-ttu-id="77258-124">您可針對不同虛擬機器類型新增的磁碟數目會有所限制。</span><span class="sxs-lookup"><span data-stu-id="77258-124">There are limits on how many disks you can add for different virtual machine types.</span></span> <span data-ttu-id="77258-125">[Azure 的虛擬機器和雲端服務大小](http://msdn.microsoft.com/library/azure/dn197896.aspx)中有這些限制的詳細說明。</span><span class="sxs-lookup"><span data-stu-id="77258-125">These limits are detailed in [Virtual machine and cloud service sizes for Azure](http://msdn.microsoft.com/library/azure/dn197896.aspx).</span></span> <span data-ttu-id="77258-126">雖然您可以選擇設定具有較少磁碟的 RAID，但您需要連接四個資料磁碟，才能遵循本文中的 RAID 4 範例。</span><span class="sxs-lookup"><span data-stu-id="77258-126">You will need four attached data disks to follow the RAID example in this article, although you can choose to set up RAID with fewer disks.</span></span>  

<span data-ttu-id="77258-127">本文假設您已經建立 Linux 虛擬機器並已安裝及設定 MYSQL 。</span><span class="sxs-lookup"><span data-stu-id="77258-127">This article assumes you have already created a Linux virtual machine and have MYSQL installed and configured.</span></span> <span data-ttu-id="77258-128">如需開始使用的詳細資訊，請參閱「如何在 Azure 上安裝 MySQL」。</span><span class="sxs-lookup"><span data-stu-id="77258-128">For more information on getting started, see How to install MySQL on Azure.</span></span>  

### <a name="set-up-raid-on-azure"></a><span data-ttu-id="77258-129">在 Azure 上設定 RAID</span><span class="sxs-lookup"><span data-stu-id="77258-129">Set up RAID on Azure</span></span>
<span data-ttu-id="77258-130">下列步驟說明如何使用 Azure 入口網站，在 Azure 上建立 RAID。</span><span class="sxs-lookup"><span data-stu-id="77258-130">The following steps show how to create RAID on Azure by using the Azure portal.</span></span> <span data-ttu-id="77258-131">您也可以使用 Windows PowerShell 指令碼設定 RAID。</span><span class="sxs-lookup"><span data-stu-id="77258-131">You can also set up RAID by using Windows PowerShell scripts.</span></span>
<span data-ttu-id="77258-132">在此範例中，我們將設定具有四個磁碟的 RAID 0。</span><span class="sxs-lookup"><span data-stu-id="77258-132">In this example, we will configure RAID 0 with four disks.</span></span>  

#### <a name="add-a-data-disk-to-your-virtual-machine"></a><span data-ttu-id="77258-133">將資料磁碟新增至您的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="77258-133">Add a data disk to your virtual machine</span></span>
<span data-ttu-id="77258-134">在 Azure 入口網站中移至儀表板，並選取要新增資料磁碟的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="77258-134">In the Azure portal, go to the dashboard and select the virtual machine to which you want to add a data disk.</span></span> <span data-ttu-id="77258-135">在此範例中，虛擬機器是 mysqlnode1。</span><span class="sxs-lookup"><span data-stu-id="77258-135">In this example, the virtual machine is mysqlnode1.</span></span>  

<!--![Virtual machines][1]-->

<span data-ttu-id="77258-136">按一下 [磁碟]，然後按一下 [連結新項目]。</span><span class="sxs-lookup"><span data-stu-id="77258-136">Click **Disks** and then click **Attach New**.</span></span>

![虛擬機器新增磁碟](media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-Disks-option.png)

<span data-ttu-id="77258-138">建立一個新的 500 GB 磁碟。</span><span class="sxs-lookup"><span data-stu-id="77258-138">Create a new 500 GB disk.</span></span> <span data-ttu-id="77258-139">確定 [主機快取偏好設定] 是設為 [無]。</span><span class="sxs-lookup"><span data-stu-id="77258-139">Make sure that **Host Cache Preference** is set to **None**.</span></span>  <span data-ttu-id="77258-140">完成時，請按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="77258-140">When you're finished, click **OK**.</span></span>

![連接空的磁碟](media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-attach-empty-disk.png)


<span data-ttu-id="77258-142">這會將一個空的磁碟新增到虛擬機器中。</span><span class="sxs-lookup"><span data-stu-id="77258-142">This adds one empty disk into your virtual machine.</span></span> <span data-ttu-id="77258-143">再重複執行此步驟三次，您的 RAID 就有四個資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="77258-143">Repeat this step three more times so that you have four data disks for RAID.</span></span>  

<span data-ttu-id="77258-144">查看核心訊息記錄檔，您可以看到虛擬機器中新增的磁碟機。</span><span class="sxs-lookup"><span data-stu-id="77258-144">You can see the added drives in the virtual machine by looking at the kernel message log.</span></span> <span data-ttu-id="77258-145">例如，若要在 Ubuntu 上查看此資料，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="77258-145">For example, to see this on Ubuntu, use the following command:</span></span>  

    sudo grep SCSI /var/log/dmesg

#### <a name="create-raid-with-the-additional-disks"></a><span data-ttu-id="77258-146">建立具有額外磁碟的 RAID</span><span class="sxs-lookup"><span data-stu-id="77258-146">Create RAID with the additional disks</span></span>
<span data-ttu-id="77258-147">下列步驟說明如何[在 Linux 上設定軟體 RAID](../configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="77258-147">The following steps describe how to [configure software RAID on Linux](../configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

> [!NOTE]
> <span data-ttu-id="77258-148">如果您使用 XFS 檔案系統，請在建立 RAID 後執行下列步驟。</span><span class="sxs-lookup"><span data-stu-id="77258-148">If you are using the XFS file system, execute the following steps after you have created RAID.</span></span>
>
>

<span data-ttu-id="77258-149">若要在 Debian、Ubuntu 或 Linux Mint 上安裝 XFS，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="77258-149">To install XFS on Debian, Ubuntu, or Linux Mint, use the following command:</span></span>  

    apt-get -y install xfsprogs  

<span data-ttu-id="77258-150">若要在 Fedora 、CentOS 或 RHEL 上安裝 XFS，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="77258-150">To install XFS on Fedora, CentOS, or RHEL, use the following command:</span></span>  

    yum -y install xfsprogs  xfsdump


#### <a name="set-up-a-new-storage-path"></a><span data-ttu-id="77258-151">設定新的儲存體路徑</span><span class="sxs-lookup"><span data-stu-id="77258-151">Set up a new storage path</span></span>
<span data-ttu-id="77258-152">使用下列命令來設定新的儲存體路徑：</span><span class="sxs-lookup"><span data-stu-id="77258-152">Use the following command to set up a new storage path:</span></span>  

    root@mysqlnode1:~# mkdir -p /RAID0/mysql

#### <a name="copy-the-original-data-to-the-new-storage-path"></a><span data-ttu-id="77258-153">將原始資料複製到新的儲存體路徑</span><span class="sxs-lookup"><span data-stu-id="77258-153">Copy the original data to the new storage path</span></span>
<span data-ttu-id="77258-154">使用下列命令將資料複製到新的儲存體路徑：</span><span class="sxs-lookup"><span data-stu-id="77258-154">Use the following command to copy data to the new storage path:</span></span>  

    root@mysqlnode1:~# cp -rp /var/lib/mysql/* /RAID0/mysql/

#### <a name="modify-permissions-so-mysql-can-access-read-and-write-the-data-disk"></a><span data-ttu-id="77258-155">修改權限，因此 MySQL 可以存取 (讀取和寫入) 資料磁碟</span><span class="sxs-lookup"><span data-stu-id="77258-155">Modify permissions so MySQL can access (read and write) the data disk</span></span>
<span data-ttu-id="77258-156">使用下列命令來修改權限：</span><span class="sxs-lookup"><span data-stu-id="77258-156">Use the following command to modify permissions:</span></span>  

    root@mysqlnode1:~# chown -R mysql.mysql /RAID0/mysql && chmod -R 755 /RAID0/mysql


## <a name="adjust-the-disk-io-scheduling-algorithm"></a><span data-ttu-id="77258-157">調整磁碟 I/O 排程演算法</span><span class="sxs-lookup"><span data-stu-id="77258-157">Adjust the disk I/O scheduling algorithm</span></span>
<span data-ttu-id="77258-158">Linux 會實作四種類型的 I/O 排程演算法：</span><span class="sxs-lookup"><span data-stu-id="77258-158">Linux implements four types of I/O scheduling algorithms:</span></span>  

* <span data-ttu-id="77258-159">NOOP 演算法 (沒有作業)</span><span class="sxs-lookup"><span data-stu-id="77258-159">NOOP algorithm (No Operation)</span></span>
* <span data-ttu-id="77258-160">期限演算法 (期限)</span><span class="sxs-lookup"><span data-stu-id="77258-160">Deadline algorithm (Deadline)</span></span>
* <span data-ttu-id="77258-161">完全公平佇列演算法 (CFQ)</span><span class="sxs-lookup"><span data-stu-id="77258-161">Completely fair queuing algorithm (CFQ)</span></span>
* <span data-ttu-id="77258-162">預算週期演算法 (預期)</span><span class="sxs-lookup"><span data-stu-id="77258-162">Budget period algorithm (Anticipatory)</span></span>  

<span data-ttu-id="77258-163">您可以在不同的狀況下選取不同的 I/O 排程器，讓效能達到最佳化。</span><span class="sxs-lookup"><span data-stu-id="77258-163">You can select different I/O schedulers under different scenarios to optimize performance.</span></span> <span data-ttu-id="77258-164">在完全隨機存取環境中，CFQ 與期限演算法之間的效能沒有明顯差別。</span><span class="sxs-lookup"><span data-stu-id="77258-164">In a completely random access environment, there is not a significant difference between the CFQ and Deadline algorithms for performance.</span></span> <span data-ttu-id="77258-165">我們建議將 MySQL 資料庫環境設為 [期限]，以求穩定性。</span><span class="sxs-lookup"><span data-stu-id="77258-165">We recommend that you set the MySQL database environment to Deadline for stability.</span></span> <span data-ttu-id="77258-166">如果有大量循序 I/O，CFQ 可能會降低磁碟 I/O 效能。</span><span class="sxs-lookup"><span data-stu-id="77258-166">If there is a lot of sequential I/O, CFQ might reduce disk I/O performance.</span></span>   

<span data-ttu-id="77258-167">對於 SSD 和其他設備，NOOP 或 [期限] 可達到比預設排程器更佳的效能。</span><span class="sxs-lookup"><span data-stu-id="77258-167">For SSD and other equipment, NOOP or Deadline can achieve better performance than the default scheduler.</span></span>   

<span data-ttu-id="77258-168">在核心 2.5 之前，預設 I/O 排程演算法為 [期限]。</span><span class="sxs-lookup"><span data-stu-id="77258-168">Prior to the kernel 2.5, the default I/O scheduling algorithm is Deadline.</span></span> <span data-ttu-id="77258-169">從核心 2.6.18 開始，CFQ 成為預設 I/O 排程演算法。</span><span class="sxs-lookup"><span data-stu-id="77258-169">Starting with the kernel 2.6.18, CFQ became the default I/O scheduling algorithm.</span></span>  <span data-ttu-id="77258-170">您可以在核心開機時指定此設定，或在系統執行時動態修改此設定。</span><span class="sxs-lookup"><span data-stu-id="77258-170">You can specify this setting at kernel boot time or dynamically modify this setting when the system is running.</span></span>  

<span data-ttu-id="77258-171">下列範例示範如何檢查預設排程器並將其設定為 Debian 散發版本系列中的 NOOP 演算法。</span><span class="sxs-lookup"><span data-stu-id="77258-171">The following example demonstrates how to check and set the default scheduler to the NOOP algorithm in the Debian distribution family.</span></span>  

### <a name="view-the-current-io-scheduler"></a><span data-ttu-id="77258-172">檢視目前的 I/O 排程器</span><span class="sxs-lookup"><span data-stu-id="77258-172">View the current I/O scheduler</span></span>
<span data-ttu-id="77258-173">若要檢視排程器，請執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="77258-173">To view the scheduler run the following command:</span></span>  

    root@mysqlnode1:~# cat /sys/block/sda/queue/scheduler

<span data-ttu-id="77258-174">您會看到下列輸出，其表示目前的排程器：</span><span class="sxs-lookup"><span data-stu-id="77258-174">You will see following output, which indicates the current scheduler:</span></span>  

    noop [deadline] cfq


### <a name="change-the-current-device-devsda-of-the-io-scheduling-algorithm"></a><span data-ttu-id="77258-175">變更 I/O 排程演算法的目前裝置 (/dev/sda)</span><span class="sxs-lookup"><span data-stu-id="77258-175">Change the current device (/dev/sda) of the I/O scheduling algorithm</span></span>
<span data-ttu-id="77258-176">執行下列命令以變更目前的裝置：</span><span class="sxs-lookup"><span data-stu-id="77258-176">Run the following commands to change the current device:</span></span>  

    azureuser@mysqlnode1:~$ sudo su -
    root@mysqlnode1:~# echo "noop" >/sys/block/sda/queue/scheduler
    root@mysqlnode1:~# sed -i 's/GRUB_CMDLINE_LINUX=""/GRUB_CMDLINE_LINUX_DEFAULT="quiet splash elevator=noop"/g' /etc/default/grub
    root@mysqlnode1:~# update-grub

> [!NOTE]
> <span data-ttu-id="77258-177">單獨針對 /dev/sda 設定此項並不是很有用。</span><span class="sxs-lookup"><span data-stu-id="77258-177">Setting this for /dev/sda alone is not useful.</span></span> <span data-ttu-id="77258-178">必須在資料庫所在的所有資料磁碟上進行設定。</span><span class="sxs-lookup"><span data-stu-id="77258-178">It must be set on all data disks where the database resides.</span></span>  
>
>

<span data-ttu-id="77258-179">您應會看到下列輸出，表示 grub.cfg 已成功重建且預設排程器已更新為 NOOP：</span><span class="sxs-lookup"><span data-stu-id="77258-179">You should see the following output, indicating that grub.cfg has been rebuilt successfully and that the default scheduler has been updated to NOOP:</span></span>  

    Generating grub configuration file ...
    Found linux image: /boot/vmlinuz-3.13.0-34-generic
    Found initrd image: /boot/initrd.img-3.13.0-34-generic
    Found linux image: /boot/vmlinuz-3.13.0-32-generic
    Found initrd image: /boot/initrd.img-3.13.0-32-generic
    Found memtest86+ image: /memtest86+.elf
    Found memtest86+ image: /memtest86+.bin
    done

<span data-ttu-id="77258-180">若為 Red Hat 散發版本系列，您只需要使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="77258-180">For the Red Hat distribution family, you need only the following command:</span></span>

    echo 'echo noop >/sys/block/sda/queue/scheduler' >> /etc/rc.local

## <a name="configure-system-file-operations-settings"></a><span data-ttu-id="77258-181">設定系統檔案作業設定</span><span class="sxs-lookup"><span data-stu-id="77258-181">Configure system file operations settings</span></span>
<span data-ttu-id="77258-182">最佳作法是停用檔案系統上的 atime 記錄功能。</span><span class="sxs-lookup"><span data-stu-id="77258-182">One best practice is to disable the *atime* logging feature on the file system.</span></span> <span data-ttu-id="77258-183">Atime 是上次檔案存取時間。</span><span class="sxs-lookup"><span data-stu-id="77258-183">Atime is the last file access time.</span></span> <span data-ttu-id="77258-184">每當存取檔案時，檔案系統就會在記錄檔中記錄時間戳記。</span><span class="sxs-lookup"><span data-stu-id="77258-184">Whenever a file is accessed, the file system records the timestamp in the log.</span></span> <span data-ttu-id="77258-185">不過，很少使用這項資訊。</span><span class="sxs-lookup"><span data-stu-id="77258-185">However, this information is rarely used.</span></span> <span data-ttu-id="77258-186">如果您不需要它，可予以停用，將會減少整體的磁碟存取時間。</span><span class="sxs-lookup"><span data-stu-id="77258-186">You can disable it if you don't need it, which will reduce overall disk access time.</span></span>  

<span data-ttu-id="77258-187">若要停用 atime 記錄，您必須修改檔案系統組態檔案 /etc/ fstab，並新增 **noatime** 選項。</span><span class="sxs-lookup"><span data-stu-id="77258-187">To disable atime logging, you need to modify the file system configuration file /etc/ fstab and add the **noatime** option.</span></span>  

<span data-ttu-id="77258-188">例如，編輯 vim /etc/fstab 檔案，新增如下範例所示的 noatime：</span><span class="sxs-lookup"><span data-stu-id="77258-188">For example, edit the vim /etc/fstab file, adding the noatime as shown in the following sample:</span></span>  

    # CLOUD_IMG: This file was created/modified by the Cloud Image build process
    UUID=3cc98c06-d649-432d-81df-6dcd2a584d41       /        ext4   defaults,discard        0 0
    #Add the “noatime” option below to disable atime logging
    UUID="431b1e78-8226-43ec-9460-514a9adf060e"     /RAID0   xfs   defaults,nobootwait, noatime 0 0
    /dev/sdb1       /mnt    auto    defaults,nobootwait,comment=cloudconfig 0       2

<span data-ttu-id="77258-189">然後，使用下列命令重新掛接檔案系統：</span><span class="sxs-lookup"><span data-stu-id="77258-189">Then, remount the file system with the following command:</span></span>  

    mount -o remount /RAID0

<span data-ttu-id="77258-190">測試修改過的結果。</span><span class="sxs-lookup"><span data-stu-id="77258-190">Test the modified result.</span></span> <span data-ttu-id="77258-191">當您修改測試檔案時，存取時間不會更新。</span><span class="sxs-lookup"><span data-stu-id="77258-191">When you modify the test file, the access time is not updated.</span></span> <span data-ttu-id="77258-192">下列範例顯示修改之前和之後的程式碼外觀。</span><span class="sxs-lookup"><span data-stu-id="77258-192">The following examples show what the code looks like before and after modification.</span></span>

<span data-ttu-id="77258-193">之前：</span><span class="sxs-lookup"><span data-stu-id="77258-193">Before:</span></span>        

![存取修改前的程式碼][5]

<span data-ttu-id="77258-195">之後︰</span><span class="sxs-lookup"><span data-stu-id="77258-195">After:</span></span>

![存取修改後的程式碼][6]

## <a name="increase-the-maximum-number-of-system-handles-for-high-concurrency"></a><span data-ttu-id="77258-197">增加高並行存取的系統控制代碼數目上限</span><span class="sxs-lookup"><span data-stu-id="77258-197">Increase the maximum number of system handles for high concurrency</span></span>
<span data-ttu-id="77258-198">MySQL 是高並行存取資料庫。</span><span class="sxs-lookup"><span data-stu-id="77258-198">MySQL is a high concurrency database.</span></span> <span data-ttu-id="77258-199">Linux 的並行控制代碼預設數目為 1024，這並不足夠。</span><span class="sxs-lookup"><span data-stu-id="77258-199">The default number of concurrent handles is 1024 for Linux, which is not always sufficient.</span></span> <span data-ttu-id="77258-200">使用下列步驟來增加系統的並行控制代碼上限，以支援 MySQL 的高並行存取。</span><span class="sxs-lookup"><span data-stu-id="77258-200">Use the following steps to increase the maximum concurrent handles of the system to support high concurrency of MySQL.</span></span>

### <a name="modify-the-limitsconf-file"></a><span data-ttu-id="77258-201">修改 limits.conf 檔案</span><span class="sxs-lookup"><span data-stu-id="77258-201">Modify the limits.conf file</span></span>
<span data-ttu-id="77258-202">若要增加允許的並行控制代碼上限，在 /etc/security/limits.conf 檔案中新增下列四行。</span><span class="sxs-lookup"><span data-stu-id="77258-202">To increase the maximum allowed concurrent handles, add the following four lines in the /etc/security/limits.conf file.</span></span> <span data-ttu-id="77258-203">請注意 65536 是系統可支援的數目上限。</span><span class="sxs-lookup"><span data-stu-id="77258-203">Note that 65536 is the maximum number that the system can support.</span></span>   

    * <span data-ttu-id="77258-204">soft nofile 65536</span><span class="sxs-lookup"><span data-stu-id="77258-204">soft nofile 65536</span></span>
    * <span data-ttu-id="77258-205">hard nofile 65536</span><span class="sxs-lookup"><span data-stu-id="77258-205">hard nofile 65536</span></span>
    * <span data-ttu-id="77258-206">soft nproc 65536</span><span class="sxs-lookup"><span data-stu-id="77258-206">soft nproc 65536</span></span>
    * <span data-ttu-id="77258-207">hard nproc 65536</span><span class="sxs-lookup"><span data-stu-id="77258-207">hard nproc 65536</span></span>

### <a name="update-the-system-for-the-new-limits"></a><span data-ttu-id="77258-208">更新系統，以取得新的限制</span><span class="sxs-lookup"><span data-stu-id="77258-208">Update the system for the new limits</span></span>
<span data-ttu-id="77258-209">若要更新系統，請執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="77258-209">To update the system, run the following commands:</span></span>  

    ulimit -SHn 65536
    ulimit -SHu 65536

### <a name="ensure-that-the-limits-are-updated-at-boot-time"></a><span data-ttu-id="77258-210">確定會在開機時更新限制</span><span class="sxs-lookup"><span data-stu-id="77258-210">Ensure that the limits are updated at boot time</span></span>
<span data-ttu-id="77258-211">將下列啟動命令放入 /etc/rc.local 檔案中，以便在開機時生效。</span><span class="sxs-lookup"><span data-stu-id="77258-211">Put the following startup commands in the /etc/rc.local file so it will take effect at boot time.</span></span>  

    echo “ulimit -SHn 65536” >>/etc/rc.local
    echo “ulimit -SHu 65536” >>/etc/rc.local

## <a name="mysql-database-optimization"></a><span data-ttu-id="77258-212">MySQL 資料庫最佳化</span><span class="sxs-lookup"><span data-stu-id="77258-212">MySQL database optimization</span></span>
<span data-ttu-id="77258-213">若要在 Azure 上設定 MySQL，您可以使用與內部部署電腦上使用的相同效能微調策略。</span><span class="sxs-lookup"><span data-stu-id="77258-213">To configure MySQL on Azure, you can use the same performance-tuning strategy you use on an on-premises machine.</span></span>  

<span data-ttu-id="77258-214">主要的 I/O 最佳化規則如下：</span><span class="sxs-lookup"><span data-stu-id="77258-214">The main I/O optimization rules are:</span></span>   

* <span data-ttu-id="77258-215">增加快取的大小。</span><span class="sxs-lookup"><span data-stu-id="77258-215">Increase the cache size.</span></span>
* <span data-ttu-id="77258-216">減少 I/O 回應時間。</span><span class="sxs-lookup"><span data-stu-id="77258-216">Reduce I/O response time.</span></span>  

<span data-ttu-id="77258-217">若要最佳化 MySQL 伺服器設定，您可以更新 my.cnf 檔案，該檔案是伺服器和用戶端電腦的預設組態檔。</span><span class="sxs-lookup"><span data-stu-id="77258-217">To optimize MySQL server settings, you can update the my.cnf file, which is the default configuration file for both server and client computers.</span></span>  

<span data-ttu-id="77258-218">下列組態項目是影響 MySQL 效能的主要因素：</span><span class="sxs-lookup"><span data-stu-id="77258-218">The following configuration items are the main factors that affect MySQL performance:</span></span>  

* <span data-ttu-id="77258-219">**innodb_buffer_pool_size**：緩衝集區包含經過緩衝處理的資料和索引。</span><span class="sxs-lookup"><span data-stu-id="77258-219">**innodb_buffer_pool_size**: The buffer pool contains buffered data and the index.</span></span> <span data-ttu-id="77258-220">這通常設定為 70% 的實體記憶體。</span><span class="sxs-lookup"><span data-stu-id="77258-220">This is usually set to 70 percent of physical memory.</span></span>
* <span data-ttu-id="77258-221">**innodb_log_file_size**：這是重做記錄檔的大小。</span><span class="sxs-lookup"><span data-stu-id="77258-221">**innodb_log_file_size**: This is the redo log size.</span></span> <span data-ttu-id="77258-222">您可以使用重做記錄檔來確保寫入作業快速、可靠並可在當機後復原。</span><span class="sxs-lookup"><span data-stu-id="77258-222">You use redo logs to ensure that write operations are fast, reliable, and recoverable after a crash.</span></span> <span data-ttu-id="77258-223">這會設定為 512 MB，將提供大量空間給您記錄寫入作業。</span><span class="sxs-lookup"><span data-stu-id="77258-223">This is set to 512 MB, which will give you plenty of space for logging write operations.</span></span>
* <span data-ttu-id="77258-224">**max_connections**：應用程式有時不會正確關閉連線。</span><span class="sxs-lookup"><span data-stu-id="77258-224">**max_connections**: Sometimes applications do not close connections properly.</span></span> <span data-ttu-id="77258-225">較大的值讓伺服器有更多的時間來回收閒置的連線。</span><span class="sxs-lookup"><span data-stu-id="77258-225">A larger value will give the server more time to recycle idled connections.</span></span> <span data-ttu-id="77258-226">連線數目上限為 10000，但建議的上限為 5000。</span><span class="sxs-lookup"><span data-stu-id="77258-226">The maximum number of connections is 10,000, but the recommended maximum is 5,000.</span></span>
* <span data-ttu-id="77258-227">**Innodb_file_per_table**：此設定可啟用或停用 InnoDB 在個別檔案中儲存資料表的功能。</span><span class="sxs-lookup"><span data-stu-id="77258-227">**Innodb_file_per_table**: This setting enables or disables the ability of InnoDB to store tables in separate files.</span></span> <span data-ttu-id="77258-228">開啟此選項可確保有效地套用數個進階管理作業。</span><span class="sxs-lookup"><span data-stu-id="77258-228">Turn on the option to ensure that several advanced administration operations can be applied efficiently.</span></span> <span data-ttu-id="77258-229">從效能觀點來看，它可以加速資料表空間傳輸，並將 debris 管理效能最佳化。</span><span class="sxs-lookup"><span data-stu-id="77258-229">From a performance point of view, it can speed up the table space transmission and optimize the debris management performance.</span></span> <span data-ttu-id="77258-230">這個選項的建議設定為 ON。</span><span class="sxs-lookup"><span data-stu-id="77258-230">The recommended setting for this option is ON.</span></span></br></br>
<span data-ttu-id="77258-231">從 MySQL 5.6 開始，預設設定為 ON，所以不需要採取任何動作。</span><span class="sxs-lookup"><span data-stu-id="77258-231">From MySQL 5.6, the default setting is ON, so no action is required.</span></span> <span data-ttu-id="77258-232">舊版的預設值為 OFF。</span><span class="sxs-lookup"><span data-stu-id="77258-232">For earlier versions, the default setting is OFF.</span></span> <span data-ttu-id="77258-233">應在載入資料之前變更此設定，因為只有新建的資料表會受影響。</span><span class="sxs-lookup"><span data-stu-id="77258-233">The setting should be changed before data is loaded, because only newly created tables are affected.</span></span>
* <span data-ttu-id="77258-234">**innodb_flush_log_at_trx_commit**：預設值為 1，其範圍設為 0~2。</span><span class="sxs-lookup"><span data-stu-id="77258-234">**innodb_flush_log_at_trx_commit**: The default value is 1, with the scope set to 0~2.</span></span> <span data-ttu-id="77258-235">對獨立 MySQL DB 而言，預設值是最適合的選項。</span><span class="sxs-lookup"><span data-stu-id="77258-235">The default value is the most suitable option for standalone MySQL DB.</span></span> <span data-ttu-id="77258-236">設定為 2 可達到最大資料完整性，適合於 MySQL 叢集中的主機。</span><span class="sxs-lookup"><span data-stu-id="77258-236">The setting of 2 enables the most data integrity and is suitable for Master in MySQL Cluster.</span></span> <span data-ttu-id="77258-237">設定為 0 會讓資料遺失，這可能會影響可靠性，在某些情況下，效能會更佳，適合於 MySQL 叢集中的從屬。</span><span class="sxs-lookup"><span data-stu-id="77258-237">The setting of 0 allows data loss, which can affect reliability (in some cases with better performance), and is suitable for Slave in MySQL Cluster.</span></span>
* <span data-ttu-id="77258-238">**Innodb_log_buffer_size**：記錄緩衝區允許交易執行，而不需在交易認可前將記錄檔排清到磁碟。</span><span class="sxs-lookup"><span data-stu-id="77258-238">**Innodb_log_buffer_size**: The log buffer allows transactions to run without having to flush the log to disk before the transactions commit.</span></span> <span data-ttu-id="77258-239">不過，如果有大型二進位物件或文字欄位，將會快速地耗用快取，並將觸發頻繁的磁碟 I/O。</span><span class="sxs-lookup"><span data-stu-id="77258-239">However, if there is large binary object or text field, the cache will be consumed quickly and frequent disk I/O will be triggered.</span></span> <span data-ttu-id="77258-240">如果 Innodb_log_waits 狀態變數不是 0，最好能增加緩衝區大小。</span><span class="sxs-lookup"><span data-stu-id="77258-240">It is better increase the buffer size if Innodb_log_waits state variable is not 0.</span></span>
* <span data-ttu-id="77258-241">**query_cache_size**：最佳選項是一開始就將它停用。</span><span class="sxs-lookup"><span data-stu-id="77258-241">**query_cache_size**: The best option is to disable it from the outset.</span></span> <span data-ttu-id="77258-242">將 query_cache_size 設為 0 (這是 MySQL 5.6 中的預設值)，並使用其他方法來加速查詢。</span><span class="sxs-lookup"><span data-stu-id="77258-242">Set query_cache_size to 0 (this is the default setting in MySQL 5.6) and use other methods to speed up queries.</span></span>  

<span data-ttu-id="77258-243">請參閱[附錄 D](#AppendixD) 來比較最佳化前後的效能。</span><span class="sxs-lookup"><span data-stu-id="77258-243">See [Appendix D](#AppendixD) for a comparison of performance before and after the optimization.</span></span>

## <a name="turn-on-the-mysql-slow-query-log-for-analyzing-the-performance-bottleneck"></a><span data-ttu-id="77258-244">開啟 MySQL 緩慢查詢記錄，以便分析效能瓶頸</span><span class="sxs-lookup"><span data-stu-id="77258-244">Turn on the MySQL slow query log for analyzing the performance bottleneck</span></span>
<span data-ttu-id="77258-245">MySQL 緩慢查詢記錄檔可協助您識別 MySQL 的較慢查詢。</span><span class="sxs-lookup"><span data-stu-id="77258-245">The MySQL slow query log can help you identify the slow queries for MySQL.</span></span> <span data-ttu-id="77258-246">啟用 MySQL 緩慢查詢記錄檔之後，您可以使用 **mysqldumpslow** 之類的 MySQL 工具來識別效能瓶頸。</span><span class="sxs-lookup"><span data-stu-id="77258-246">After enabling the MySQL slow query log, you can use MySQL tools like **mysqldumpslow** to identify the performance bottleneck.</span></span>  

<span data-ttu-id="77258-247">預設不會啟用此項目。</span><span class="sxs-lookup"><span data-stu-id="77258-247">By default, this is not enabled.</span></span> <span data-ttu-id="77258-248">開啟緩慢查詢記錄檔可能會耗用一些 CPU 資源。</span><span class="sxs-lookup"><span data-stu-id="77258-248">Turning on the slow query log might consume some CPU resources.</span></span> <span data-ttu-id="77258-249">我們建議您暫時啟用這個選項，以便排解效能瓶頸。</span><span class="sxs-lookup"><span data-stu-id="77258-249">We recommend that you enable this temporarily for troubleshooting performance bottlenecks.</span></span> <span data-ttu-id="77258-250">若要開啟緩慢查詢記錄檔︰</span><span class="sxs-lookup"><span data-stu-id="77258-250">To turn on the slow query log:</span></span>

1. <span data-ttu-id="77258-251">將下列幾行加至 my.cnf 檔案結尾，以修改該檔案：</span><span class="sxs-lookup"><span data-stu-id="77258-251">Modify the my.cnf file by adding the following lines to the end:</span></span>

        long_query_time = 2
        slow_query_log = 1
        slow_query_log_file = /RAID0/mysql/mysql-slow.log

2. <span data-ttu-id="77258-252">重新啟動 MySQL 伺服器。</span><span class="sxs-lookup"><span data-stu-id="77258-252">Restart the MySQL server.</span></span>

        service  mysql  restart

3. <span data-ttu-id="77258-253">使用 **show** 命令檢查設定是否生效。</span><span class="sxs-lookup"><span data-stu-id="77258-253">Check whether the setting is taking effect by using the **show** command.</span></span>

![Slow-query-log ON][7]   

![Slow-query-log 結果][8]

<span data-ttu-id="77258-256">在此範例中，您可以看到緩慢查詢功能已開啟。</span><span class="sxs-lookup"><span data-stu-id="77258-256">In this example, you can see that the slow query feature has been turned on.</span></span> <span data-ttu-id="77258-257">您可以接著使用 **mysqldumpslow** 工具，判斷效能瓶頸並將效能最佳化，例如，新增索引。</span><span class="sxs-lookup"><span data-stu-id="77258-257">You can then use the **mysqldumpslow** tool to determine performance bottlenecks and optimize performance, such as adding indexes.</span></span>

## <a name="appendices"></a><span data-ttu-id="77258-258">附錄</span><span class="sxs-lookup"><span data-stu-id="77258-258">Appendices</span></span>
<span data-ttu-id="77258-259">以下是在目標實驗室環境中產生的範例效能測試資料。</span><span class="sxs-lookup"><span data-stu-id="77258-259">The following are sample performance test data produced in a targeted lab environment.</span></span> <span data-ttu-id="77258-260">其提供採用不同效能調整方法之效能資料趨勢的一般背景。</span><span class="sxs-lookup"><span data-stu-id="77258-260">They provide general background on the performance data trend with different performance tuning approaches.</span></span> <span data-ttu-id="77258-261">在不同的環境或產品版本之下，結果可能會有所不同。</span><span class="sxs-lookup"><span data-stu-id="77258-261">The results might vary under different environment or product versions.</span></span>

### <span data-ttu-id="77258-262"><a name="AppendixA"></a>附錄 A</span><span class="sxs-lookup"><span data-stu-id="77258-262"><a name="AppendixA"></a>Appendix A</span></span>  
<span data-ttu-id="77258-263">**不同 RAID 層級的磁碟效能 (IOPS)**</span><span class="sxs-lookup"><span data-stu-id="77258-263">**Disk performance (IOPS) with different RAID levels**</span></span>

![不同 RAID 層級的磁碟 IOPS][9]

<span data-ttu-id="77258-265">**測試命令**</span><span class="sxs-lookup"><span data-stu-id="77258-265">**Test commands**</span></span>  

    fio -filename=/path/test -iodepth=64 -ioengine=libaio -direct=1 -rw=randwrite -bs=4k -size=5G -numjobs=64 -runtime=30 -group_reporting -name=test-randwrite

> [!NOTE]
> <span data-ttu-id="77258-266">這項測試的工作負載會使用 64 個執行緒，並嘗試達到 RAID 的上限。</span><span class="sxs-lookup"><span data-stu-id="77258-266">The workload of this test uses 64 threads, trying to reach the upper limit of RAID.</span></span>
>
>

### <span data-ttu-id="77258-267"><a name="AppendixB"></a>附錄 B</span><span class="sxs-lookup"><span data-stu-id="77258-267"><a name="AppendixB"></a>Appendix B</span></span>  
<span data-ttu-id="77258-268">**不同 RAID 層級的 MySQL 效能 (輸送量) 比較** </span><span class="sxs-lookup"><span data-stu-id="77258-268">**MySQL performance (throughput) comparison with different RAID levels** </span></span>  
<span data-ttu-id="77258-269">(XFS檔案系統)</span><span class="sxs-lookup"><span data-stu-id="77258-269">(XFS file system)</span></span>

![不同 RAID 層級的 MySQL 效能比較][10]  
![不同 RAID 層級的 MySQL 效能比較][11]

<span data-ttu-id="77258-272">**測試命令**</span><span class="sxs-lookup"><span data-stu-id="77258-272">**Test commands**</span></span>

    mysqlslap -p0ps.123 --concurrency=2 --iterations=1 --number-int-cols=10 --number-char-cols=10 -a --auto-generate-sql-guid-primary --number-of-queries=10000 --auto-generate-sql-load-type=write –engine=innodb

<span data-ttu-id="77258-273">**不同 RAID 層級的 MySQL 效能 (OLTP) 比較**</span><span class="sxs-lookup"><span data-stu-id="77258-273">**MySQL performance (OLTP) comparison with different RAID levels**</span></span>  
<span data-ttu-id="77258-274">![不同 RAID 層級的 MySQL 效能 (OLTP) 比較][12]</span><span class="sxs-lookup"><span data-stu-id="77258-274">![MySQL performance (OLTP) comparison with different RAID levels][12]</span></span>

<span data-ttu-id="77258-275">**測試命令**</span><span class="sxs-lookup"><span data-stu-id="77258-275">**Test commands**</span></span>

    time sysbench --test=oltp --db-driver=mysql --mysql-user=root --mysql-password=0ps.123  --mysql-table-engine=innodb --mysql-host=127.0.0.1 --mysql-port=3306 --mysql-socket=/var/run/mysqld/mysqld.sock --mysql-db=test --oltp-table-size=1000000 prepare

### <span data-ttu-id="77258-276"><a name="AppendixC"></a>附錄 C</span><span class="sxs-lookup"><span data-stu-id="77258-276"><a name="AppendixC"></a>Appendix C</span></span>   
<span data-ttu-id="77258-277">**不同區塊大小的磁碟效能 (IOPS) 比較**</span><span class="sxs-lookup"><span data-stu-id="77258-277">**Disk performance (IOPS) comparison for different chunk sizes**</span></span>  
<span data-ttu-id="77258-278">(XFS檔案系統)</span><span class="sxs-lookup"><span data-stu-id="77258-278">(XFS file system)</span></span>

![][13]

<span data-ttu-id="77258-279">**測試命令**</span><span class="sxs-lookup"><span data-stu-id="77258-279">**Test commands**</span></span>  

    fio -filename=/path/test -iodepth=64 -ioengine=libaio -direct=1 -rw=randwrite -bs=4k -size=30G -numjobs=64 -runtime=30 -group_reporting -name=test-randwrite
    fio -filename=/path/test -iodepth=64 -ioengine=libaio -direct=1 -rw=randwrite -bs=4k -size=1G -numjobs=64 -runtime=30 -group_reporting -name=test-randwrite  

<span data-ttu-id="77258-280">這項測試所使用的檔案大小分別為 30 GB 和 1 GB，搭配 RAID 0 (4 磁碟) XFS fie 系統。</span><span class="sxs-lookup"><span data-stu-id="77258-280">The file sizes used for this testing are 30 GB and 1 GB, respectively, with RAID 0 (4 disks) XFS file system.</span></span>

### <span data-ttu-id="77258-281"><a name="AppendixD"></a>附錄 D</span><span class="sxs-lookup"><span data-stu-id="77258-281"><a name="AppendixD"></a>Appendix D</span></span>  
<span data-ttu-id="77258-282">**最佳化之前和之後的 MySQL 效能 (輸送量) 比較**</span><span class="sxs-lookup"><span data-stu-id="77258-282">**MySQL performance (throughput) comparison before and after optimization**</span></span>  
<span data-ttu-id="77258-283">(XFS檔案系統)</span><span class="sxs-lookup"><span data-stu-id="77258-283">(XFS File System)</span></span>

![最佳化之前和之後的 MySQL 效能 (輸送量) 比較][14]

<span data-ttu-id="77258-285">**測試命令**</span><span class="sxs-lookup"><span data-stu-id="77258-285">**Test commands**</span></span>

    mysqlslap -p0ps.123 --concurrency=2 --iterations=1 --number-int-cols=10 --number-char-cols=10 -a --auto-generate-sql-guid-primary --number-of-queries=10000 --auto-generate-sql-load-type=write –engine=innodb,misam

<span data-ttu-id="77258-286">**預設值與最佳化的組態設定如下所示：**</span><span class="sxs-lookup"><span data-stu-id="77258-286">**The configuration setting for default and optimization is as follows:**</span></span>

| <span data-ttu-id="77258-287">參數</span><span class="sxs-lookup"><span data-stu-id="77258-287">Parameters</span></span> | <span data-ttu-id="77258-288">預設值</span><span class="sxs-lookup"><span data-stu-id="77258-288">Default</span></span> | <span data-ttu-id="77258-289">最佳化</span><span class="sxs-lookup"><span data-stu-id="77258-289">Optimization</span></span> |
| --- | --- | --- |
| <span data-ttu-id="77258-290">**innodb_buffer_pool_size**</span><span class="sxs-lookup"><span data-stu-id="77258-290">**innodb_buffer_pool_size**</span></span> |<span data-ttu-id="77258-291">None</span><span class="sxs-lookup"><span data-stu-id="77258-291">None</span></span> |<span data-ttu-id="77258-292">7 GB</span><span class="sxs-lookup"><span data-stu-id="77258-292">7 GB</span></span> |
| <span data-ttu-id="77258-293">**innodb_log_file_size**</span><span class="sxs-lookup"><span data-stu-id="77258-293">**innodb_log_file_size**</span></span> |<span data-ttu-id="77258-294">5 MB</span><span class="sxs-lookup"><span data-stu-id="77258-294">5 MB</span></span> |<span data-ttu-id="77258-295">512 MB</span><span class="sxs-lookup"><span data-stu-id="77258-295">512 MB</span></span> |
| <span data-ttu-id="77258-296">**max_connections**</span><span class="sxs-lookup"><span data-stu-id="77258-296">**max_connections**</span></span> |<span data-ttu-id="77258-297">100</span><span class="sxs-lookup"><span data-stu-id="77258-297">100</span></span> |<span data-ttu-id="77258-298">5000</span><span class="sxs-lookup"><span data-stu-id="77258-298">5000</span></span> |
| <span data-ttu-id="77258-299">**innodb_file_per_table**</span><span class="sxs-lookup"><span data-stu-id="77258-299">**innodb_file_per_table**</span></span> |<span data-ttu-id="77258-300">0</span><span class="sxs-lookup"><span data-stu-id="77258-300">0</span></span> |<span data-ttu-id="77258-301">1</span><span class="sxs-lookup"><span data-stu-id="77258-301">1</span></span> |
| <span data-ttu-id="77258-302">**innodb_flush_log_at_trx_commit**</span><span class="sxs-lookup"><span data-stu-id="77258-302">**innodb_flush_log_at_trx_commit**</span></span> |<span data-ttu-id="77258-303">1</span><span class="sxs-lookup"><span data-stu-id="77258-303">1</span></span> |<span data-ttu-id="77258-304">2</span><span class="sxs-lookup"><span data-stu-id="77258-304">2</span></span> |
| <span data-ttu-id="77258-305">**innodb_log_buffer_size**</span><span class="sxs-lookup"><span data-stu-id="77258-305">**innodb_log_buffer_size**</span></span> |<span data-ttu-id="77258-306">8 MB</span><span class="sxs-lookup"><span data-stu-id="77258-306">8 MB</span></span> |<span data-ttu-id="77258-307">128 MB</span><span class="sxs-lookup"><span data-stu-id="77258-307">128 MB</span></span> |
| <span data-ttu-id="77258-308">**query_cache_size**</span><span class="sxs-lookup"><span data-stu-id="77258-308">**query_cache_size**</span></span> |<span data-ttu-id="77258-309">16 MB</span><span class="sxs-lookup"><span data-stu-id="77258-309">16 MB</span></span> |<span data-ttu-id="77258-310">0</span><span class="sxs-lookup"><span data-stu-id="77258-310">0</span></span> |

<span data-ttu-id="77258-311">如需更詳細的[最佳化設定參數](http://dev.mysql.com/doc/refman/5.6/en/innodb-configuration.html)，請參閱 [MySQL 官方指示](http://dev.mysql.com/doc/refman/5.6/en/innodb-parameters.html#sysvar_innodb_flush_method)。</span><span class="sxs-lookup"><span data-stu-id="77258-311">For more detailed [optimization configuration parameters](http://dev.mysql.com/doc/refman/5.6/en/innodb-configuration.html), refer to the [MySQL official instructions](http://dev.mysql.com/doc/refman/5.6/en/innodb-parameters.html#sysvar_innodb_flush_method).</span></span>  

  <span data-ttu-id="77258-312">**測試環境**</span><span class="sxs-lookup"><span data-stu-id="77258-312">**Test environment**</span></span>  

| <span data-ttu-id="77258-313">硬體</span><span class="sxs-lookup"><span data-stu-id="77258-313">Hardware</span></span> | <span data-ttu-id="77258-314">詳細資料</span><span class="sxs-lookup"><span data-stu-id="77258-314">Details</span></span> |
| --- | --- |
| <span data-ttu-id="77258-315">CPU</span><span class="sxs-lookup"><span data-stu-id="77258-315">CPU</span></span> |<span data-ttu-id="77258-316">AMD Opteron(tm) 處理器 4171 HE/4 核心</span><span class="sxs-lookup"><span data-stu-id="77258-316">AMD Opteron(tm) Processor 4171 HE/4 cores</span></span> |
| <span data-ttu-id="77258-317">記憶體</span><span class="sxs-lookup"><span data-stu-id="77258-317">Memory</span></span> |<span data-ttu-id="77258-318">14 GB</span><span class="sxs-lookup"><span data-stu-id="77258-318">14 GB</span></span> |
| <span data-ttu-id="77258-319">磁碟</span><span class="sxs-lookup"><span data-stu-id="77258-319">Disk</span></span> |<span data-ttu-id="77258-320">10 GB/磁碟</span><span class="sxs-lookup"><span data-stu-id="77258-320">10 GB/disk</span></span> |
| <span data-ttu-id="77258-321">作業系統</span><span class="sxs-lookup"><span data-stu-id="77258-321">OS</span></span> |<span data-ttu-id="77258-322">Ubuntu 14.04.1 LTS</span><span class="sxs-lookup"><span data-stu-id="77258-322">Ubuntu 14.04.1 LTS</span></span> |

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

