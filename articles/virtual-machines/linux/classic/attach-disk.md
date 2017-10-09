---
title: "在 Azure 中的 Linux VM 的磁碟 tooa aaaAttach |Microsoft 文件"
description: "了解如何 tooattach 資料磁碟 tooa Linux VM 使用 hello 傳統部署模型，並初始化 hello 磁碟，讓它可供使用"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 4901384d-2a6f-4f46-bba0-337a348b7f87
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: c76d8479ac2b522d2b6df658cd28f242473f30ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooattach-a-data-disk-tooa-linux-virtual-machine"></a><span data-ttu-id="b236f-103">如何 tooAttach 資料磁碟 tooa Linux 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="b236f-103">How tooAttach a Data Disk tooa Linux Virtual Machine</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="b236f-104">Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="b236f-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="b236f-105">本文件涵蓋使用 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="b236f-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="b236f-106">Microsoft 建議最新的部署使用 hello 資源管理員的模型。</span><span class="sxs-lookup"><span data-stu-id="b236f-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="b236f-107">請參閱如何太[將使用 hello Resource Manager 部署模型的資料磁碟連接](../add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="b236f-107">See how too[attach a data disk using hello Resource Manager deployment model](../add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="b236f-108">您可以附加空磁碟及包含資料 tooyour Azure Vm 的磁碟。</span><span class="sxs-lookup"><span data-stu-id="b236f-108">You can attach both empty disks and disks that contain data tooyour Azure VMs.</span></span> <span data-ttu-id="b236f-109">這兩種類型的磁碟都是位於 Azure 儲存體帳戶中的 .vhd 檔案。</span><span class="sxs-lookup"><span data-stu-id="b236f-109">Both types of disks are .vhd files that reside in an Azure storage account.</span></span> <span data-ttu-id="b236f-110">新增的任何磁碟 tooa Linux 機器，附加 hello 磁碟之後，您需要 tooinitialize 和格式化它，讓它可供使用。</span><span class="sxs-lookup"><span data-stu-id="b236f-110">As with adding any disk tooa Linux machine, after you attach hello disk you need tooinitialize and format it so it's ready for use.</span></span> <span data-ttu-id="b236f-111">附加空磁碟和磁碟如何 toothen 初始化及格式化新的磁碟已經包含資料 tooyour Vm，以及此發行項詳細資料。</span><span class="sxs-lookup"><span data-stu-id="b236f-111">This article details attaching both empty disks and disks already containing data tooyour VMs, as well as how toothen initialize and format a new disk.</span></span>

> [!NOTE]
> <span data-ttu-id="b236f-112">它是最佳的作法 toouse 其中一個或多個個別磁碟 toostore 虛擬機器的資料。</span><span class="sxs-lookup"><span data-stu-id="b236f-112">It's a best practice toouse one or more separate disks toostore a virtual machine's data.</span></span> <span data-ttu-id="b236f-113">當您建立 Azure 虛擬機器時，它會有作業系統磁碟和暫存磁碟。</span><span class="sxs-lookup"><span data-stu-id="b236f-113">When you create an Azure virtual machine, it has an operating system disk and a temporary disk.</span></span> <span data-ttu-id="b236f-114">**請勿使用 hello 暫存磁碟 toostore 永續性資料。**</span><span class="sxs-lookup"><span data-stu-id="b236f-114">**Do not use hello temporary disk toostore persistent data.**</span></span> <span data-ttu-id="b236f-115">正如 hello 名，它會提供暫存儲存位置。</span><span class="sxs-lookup"><span data-stu-id="b236f-115">As hello name implies, it provides temporary storage only.</span></span> <span data-ttu-id="b236f-116">它並不提供備援或備份，因為它不在 Azure 儲存體內。</span><span class="sxs-lookup"><span data-stu-id="b236f-116">It offers no redundancy or backup because it doesn't reside in Azure storage.</span></span>
> <span data-ttu-id="b236f-117">hello 暫存磁碟通常由 hello Azure Linux 代理程式管理，且自動掛接太**/mnt/retention/ 資源**(或**/mnt** Ubuntu 映像上)。</span><span class="sxs-lookup"><span data-stu-id="b236f-117">hello temporary disk is typically managed by hello Azure Linux Agent and automatically mounted too**/mnt/resource** (or **/mnt** on Ubuntu images).</span></span> <span data-ttu-id="b236f-118">在 hello 另一方面，資料磁碟可能會命名為 hello Linux 核心類似`/dev/sdc`，而且您需要 toopartition，格式化及裝載此資源。</span><span class="sxs-lookup"><span data-stu-id="b236f-118">On hello other hand, a data disk might be named by hello Linux kernel something like `/dev/sdc`, and you need toopartition, format, and mount this resource.</span></span> <span data-ttu-id="b236f-119">請參閱 hello [Azure Linux 代理程式使用者指南][ Agent]如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="b236f-119">See hello [Azure Linux Agent User Guide][Agent] for details.</span></span>
> 
> 

[!INCLUDE [howto-attach-disk-windows-linux](../../../../includes/howto-attach-disk-linux.md)]

## <a name="initialize-a-new-data-disk-in-linux"></a><span data-ttu-id="b236f-120">在 Linux 中初始化新的資料磁碟</span><span class="sxs-lookup"><span data-stu-id="b236f-120">Initialize a new data disk in Linux</span></span>
1. <span data-ttu-id="b236f-121">SSH tooyour VM。</span><span class="sxs-lookup"><span data-stu-id="b236f-121">SSH tooyour VM.</span></span> <span data-ttu-id="b236f-122">如需詳細資訊，請參閱[如何 tooa 執行 Linux 的虛擬機器上的 toolog][Logon]。</span><span class="sxs-lookup"><span data-stu-id="b236f-122">For more information, see [How toolog on tooa virtual machine running Linux][Logon].</span></span>
2. <span data-ttu-id="b236f-123">接下來您需要 hello 資料磁碟 tooinitialize toofind hello 裝置識別碼。</span><span class="sxs-lookup"><span data-stu-id="b236f-123">Next you need toofind hello device identifier for hello data disk tooinitialize.</span></span> <span data-ttu-id="b236f-124">有兩種方式 toodo 的：</span><span class="sxs-lookup"><span data-stu-id="b236f-124">There are two ways toodo that:</span></span>
   
    <span data-ttu-id="b236f-125">SCSI 裝置 hello 中的 Grep a) 記錄，例如 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="b236f-125">a) Grep for SCSI devices in hello logs, such as in hello following command:</span></span>
   
    ```bash
    sudo grep SCSI /var/log/messages
    ```
   
    <span data-ttu-id="b236f-126">針對最近 Ubuntu 分佈，您可能需要 toouse`sudo grep SCSI /var/log/syslog`因為太記錄`/var/log/messages`預設可能會停用。</span><span class="sxs-lookup"><span data-stu-id="b236f-126">For recent Ubuntu distributions, you may need toouse `sudo grep SCSI /var/log/syslog` because logging too`/var/log/messages` might be disabled by default.</span></span>
   
    <span data-ttu-id="b236f-127">您可以找到 hello hello 最後一個資料磁碟的 hello 訊息中，會顯示已加入的識別項。</span><span class="sxs-lookup"><span data-stu-id="b236f-127">You can find hello identifier of hello last data disk that was added in hello messages that are displayed.</span></span>
   
    ![收到 hello 磁碟訊息](./media/attach-disk/scsidisklog.png)
   
    <span data-ttu-id="b236f-129">或</span><span class="sxs-lookup"><span data-stu-id="b236f-129">OR</span></span>
   
    <span data-ttu-id="b236f-130">b） 使用 hello`lsscsi`命令 toofind 出 hello 裝置識別碼。`lsscsi`可以透過安裝`yum install lsscsi`（Red hat 基底散發套件） 或`apt-get install lsscsi`（Debian 依據分佈）。</span><span class="sxs-lookup"><span data-stu-id="b236f-130">b) Use hello `lsscsi` command toofind out hello device id. `lsscsi` can be installed by either `yum install lsscsi` (on Red Hat based distributions) or `apt-get install lsscsi` (on Debian based distributions).</span></span> <span data-ttu-id="b236f-131">您可以找到您要尋找的 hello 磁碟其*lun*或**邏輯單元編號**。</span><span class="sxs-lookup"><span data-stu-id="b236f-131">You can find hello disk you are looking for by its *lun* or **logical unit number**.</span></span> <span data-ttu-id="b236f-132">例如，hello *lun*如您所連接的 hello 磁碟可以輕鬆地看到從`azure vm disk list <virtual-machine>`為：</span><span class="sxs-lookup"><span data-stu-id="b236f-132">For example, hello *lun* for hello disks you attached can be easily seen from `azure vm disk list <virtual-machine>` as:</span></span>

    ```azurecli
    azure vm disk list myVM
    ```

    <span data-ttu-id="b236f-133">hello 輸出是類似 toohello 下列：</span><span class="sxs-lookup"><span data-stu-id="b236f-133">hello output is similar toohello following:</span></span>

    ```azurecli
    info:    Executing command vm disk list
    + Fetching disk images
    + Getting virtual machines
    + Getting VM disks
    data:    Lun  Size(GB)  Blob-Name                         OS
    data:    ---  --------  --------------------------------  -----
    data:         30        myVM-2645b8030676c8f8.vhd  Linux
    data:    0    100       myVM-76f7ee1ef0f6dddc.vhd
    info:    vm disk list command OK
    ```
   
    <span data-ttu-id="b236f-134">比較此資料與 hello 輸出`lsscsi`hello 相同範例虛擬機器：</span><span class="sxs-lookup"><span data-stu-id="b236f-134">Compare this data with hello output of `lsscsi` for hello same sample virtual machine:</span></span>
   
    ```bash
    [1:0:0:0]    cd/dvd  Msft     Virtual CD/ROM   1.0   /dev/sr0
    [2:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sda
    [3:0:1:0]    disk    Msft     Virtual Disk     1.0   /dev/sdb
    [5:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sdc
    ```
   
    <span data-ttu-id="b236f-135">hello hello tuple 中每個資料列中的最後一個號碼為 hello *lun*。</span><span class="sxs-lookup"><span data-stu-id="b236f-135">hello last number in hello tuple in each row is hello *lun*.</span></span> <span data-ttu-id="b236f-136">如需詳細資訊，請參閱 `man lsscsi` 。</span><span class="sxs-lookup"><span data-stu-id="b236f-136">See `man lsscsi` for more information.</span></span>
3. <span data-ttu-id="b236f-137">在 hello 提示字元中輸入下列命令 toocreate hello 您的裝置：</span><span class="sxs-lookup"><span data-stu-id="b236f-137">At hello prompt, type hello following command toocreate your device:</span></span>
   
    ```bash
    sudo fdisk /dev/sdc
    ```

4. <span data-ttu-id="b236f-138">出現提示時，輸入 **n**  toocreate 分割區。</span><span class="sxs-lookup"><span data-stu-id="b236f-138">When prompted, type **n** toocreate a partition.</span></span>

    ![建立裝置](./media/attach-disk/fdisknewpartition.png)

5. <span data-ttu-id="b236f-140">出現提示時，輸入**p** toomake hello 分割 hello 主要磁碟分割。</span><span class="sxs-lookup"><span data-stu-id="b236f-140">When prompted, type **p** toomake hello partition hello primary partition.</span></span> <span data-ttu-id="b236f-141">型別**1** toomake 它 hello 第一個資料分割，，然後輸入 hello 磁柱輸入 tooaccept hello 預設值。</span><span class="sxs-lookup"><span data-stu-id="b236f-141">Type **1** toomake it hello first partition, and then type enter tooaccept hello default value for hello cylinder.</span></span> <span data-ttu-id="b236f-142">在某些系統，可先顯示 hello hello 預設值並 hello 最後的磁區，而不是 hello 磁柱。</span><span class="sxs-lookup"><span data-stu-id="b236f-142">On some systems, it can show hello default values of hello first and hello last sectors, instead of hello cylinder.</span></span> <span data-ttu-id="b236f-143">您可以選擇 tooaccept 這些預設值。</span><span class="sxs-lookup"><span data-stu-id="b236f-143">You can choose tooaccept these defaults.</span></span>

    ![建立磁碟分割](./media/attach-disk/fdisknewpartdetails.png)


6. <span data-ttu-id="b236f-145">型別**p** toosee hello 詳細 hello 磁碟分割。</span><span class="sxs-lookup"><span data-stu-id="b236f-145">Type **p** toosee hello details about hello disk that is being partitioned.</span></span>

    ![列出磁碟資訊](./media/attach-disk/fdiskpartitiondetails.png)


7. <span data-ttu-id="b236f-147">型別**w** toowrite hello hello 磁碟設定。</span><span class="sxs-lookup"><span data-stu-id="b236f-147">Type **w** toowrite hello settings for hello disk.</span></span>

    ![寫入 hello 磁碟上的變更](./media/attach-disk/fdiskwritedisk.png)

8. <span data-ttu-id="b236f-149">現在您可以在 hello 新磁碟分割上建立 hello 檔案系統。</span><span class="sxs-lookup"><span data-stu-id="b236f-149">Now you can create hello file system on hello new partition.</span></span> <span data-ttu-id="b236f-150">附加 hello 分割區編號 toohello 裝置識別碼 (在下列範例中的 hello `/dev/sdc1`)。</span><span class="sxs-lookup"><span data-stu-id="b236f-150">Append hello partition number toohello device ID (in hello following example `/dev/sdc1`).</span></span> <span data-ttu-id="b236f-151">hello 下列範例會建立 ext4 磁碟分割上 /dev/sdc1:</span><span class="sxs-lookup"><span data-stu-id="b236f-151">hello following example creates an ext4 partition on /dev/sdc1:</span></span>
   
    ```bash
    sudo mkfs -t ext4 /dev/sdc1
    ```
   
    ![建立檔案系統](./media/attach-disk/mkfsext4.png)
   
   > [!NOTE]
   > <span data-ttu-id="b236f-153">SuSE Linux Enterprise 11 系統針對 ext4 檔案系統只支援唯讀存取。</span><span class="sxs-lookup"><span data-stu-id="b236f-153">SuSE Linux Enterprise 11 systems only support read-only access for ext4 file systems.</span></span> <span data-ttu-id="b236f-154">如需這些系統，建議 tooformat hello 新的檔案系統為 ext3，而不是 ext4。</span><span class="sxs-lookup"><span data-stu-id="b236f-154">For these systems, it is recommended tooformat hello new file system as ext3 rather than ext4.</span></span>

9. <span data-ttu-id="b236f-155">讓目錄 toomount hello 新的檔案系統，如下所示：</span><span class="sxs-lookup"><span data-stu-id="b236f-155">Make a directory toomount hello new file system, as follows:</span></span>
   
    ```bash
    sudo mkdir /datadrive
    ```

10. <span data-ttu-id="b236f-156">最後您掛接 hello 磁碟機，如下所示：</span><span class="sxs-lookup"><span data-stu-id="b236f-156">Finally you can mount hello drive, as follows:</span></span>
   
    ```bash
    sudo mount /dev/sdc1 /datadrive
    ```
   
    <span data-ttu-id="b236f-157">hello 資料磁碟現在已準備好 toouse 為**/datadrive**。</span><span class="sxs-lookup"><span data-stu-id="b236f-157">hello data disk is now ready toouse as **/datadrive**.</span></span>
   
    ![建立 hello 目錄及掛接 hello 磁碟](./media/attach-disk/mkdirandmount.png)

11. <span data-ttu-id="b236f-159">加入 hello 新磁碟機太/等/fstab:</span><span class="sxs-lookup"><span data-stu-id="b236f-159">Add hello new drive too/etc/fstab:</span></span>
   
    <span data-ttu-id="b236f-160">重新開機，它必須加入 toohello /etc/fstab 檔案之後，會自動掛接 tooensure hello 磁碟機。</span><span class="sxs-lookup"><span data-stu-id="b236f-160">tooensure hello drive is remounted automatically after a reboot it must be added toohello /etc/fstab file.</span></span> <span data-ttu-id="b236f-161">此外，強烈建議 /etc/fstab toorefer toohello 磁碟機，而不是只有 hello 裝置名稱 (也就是 /dev/sdc1) 中使用該 hello UUID （全域唯一識別碼）。</span><span class="sxs-lookup"><span data-stu-id="b236f-161">In addition, it is highly recommended that hello UUID (Universally Unique IDentifier) is used in /etc/fstab toorefer toohello drive rather than just hello device name (i.e. /dev/sdc1).</span></span> <span data-ttu-id="b236f-162">使用 hello UUID 可避免 hello 正在掛接的 tooa 如果 hello OS 開機期間偵測到磁碟錯誤，而且任何剩餘的資料磁碟，然後在其中指派那些裝置識別碼指定的位置不正確的磁碟。</span><span class="sxs-lookup"><span data-stu-id="b236f-162">Using hello UUID avoids hello incorrect disk being mounted tooa given location if hello OS detects a disk error during boot and any remaining data disks then being assigned those device IDs.</span></span> <span data-ttu-id="b236f-163">toofind hello UUID hello 新磁碟機，您可以使用 hello **blkid**公用程式：</span><span class="sxs-lookup"><span data-stu-id="b236f-163">toofind hello UUID of hello new drive, you can use hello **blkid** utility:</span></span>
   
    ```bash
    sudo -i blkid
    ```
   
    <span data-ttu-id="b236f-164">hello 輸出看起來類似下列範例的 toohello:</span><span class="sxs-lookup"><span data-stu-id="b236f-164">hello output looks similar toohello following example:</span></span>
   
    ```bash
    /dev/sda1: UUID="11111111-1b1b-1c1c-1d1d-1e1e1e1e1e1e" TYPE="ext4"
    /dev/sdb1: UUID="22222222-2b2b-2c2c-2d2d-2e2e2e2e2e2e" TYPE="ext4"
    /dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
    ```

    > [!NOTE]
    > <span data-ttu-id="b236f-165">不當編輯 hello **/etc/hosts fstab**檔案可能會導致系統無法重新啟動。</span><span class="sxs-lookup"><span data-stu-id="b236f-165">Improperly editing hello **/etc/fstab** file could result in an unbootable system.</span></span> <span data-ttu-id="b236f-166">如果不確定，請參閱 toohello 發佈文件，以取得 tooproperly 如何編輯此檔案的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="b236f-166">If unsure, refer toohello distribution's documentation for information on how tooproperly edit this file.</span></span> <span data-ttu-id="b236f-167">也建議在編輯之前建立的 hello /etc/fstab 檔案的備份。</span><span class="sxs-lookup"><span data-stu-id="b236f-167">It is also recommended that a backup of hello /etc/fstab file is created before editing.</span></span>

    <span data-ttu-id="b236f-168">接下來，開啟 hello **/etc/hosts fstab**文字編輯器中的檔案：</span><span class="sxs-lookup"><span data-stu-id="b236f-168">Next, open hello **/etc/fstab** file in a text editor:</span></span>

    ```bash
    sudo vi /etc/fstab
    ```

    <span data-ttu-id="b236f-169">在此範例中，我們使用 hello UUID 值 hello 新**/開發/sdc1** hello 先前步驟中，與 hello 掛接點中所建立的裝置**/datadrive**。</span><span class="sxs-lookup"><span data-stu-id="b236f-169">In this example, we use hello UUID value for hello new **/dev/sdc1** device that was created in hello previous steps, and hello mountpoint **/datadrive**.</span></span> <span data-ttu-id="b236f-170">加入下列行 toohello 結尾 hello hello **/etc/hosts fstab**檔案：</span><span class="sxs-lookup"><span data-stu-id="b236f-170">Add hello following line toohello end of hello **/etc/fstab** file:</span></span>

    ```sh
    UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,nofail   1   2
    ```

    <span data-ttu-id="b236f-171">或者，在 SuSE Linux 為基礎的系統上，您可能需要 toouse 稍有不同的格式：</span><span class="sxs-lookup"><span data-stu-id="b236f-171">Or, on systems based on SuSE Linux you may need toouse a slightly different format:</span></span>

    ```sh
    /dev/disk/by-uuid/33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext3   defaults,nofail   1   2
    ```

    > [!NOTE]
    > <span data-ttu-id="b236f-172">hello`nofail`選項可確保即使 hello 檔案系統已損毀或不存在 hello 磁碟，這是在開機時，VM 啟動該 hello。</span><span class="sxs-lookup"><span data-stu-id="b236f-172">hello `nofail` option ensures that hello VM starts even if hello filesystem is corrupt or hello disk does not exist at boot time.</span></span> <span data-ttu-id="b236f-173">如果沒有這個選項，您可能會遇到行為中所述[無法 SSH tooLinux VM 到期 tooFSTAB 錯誤](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/)。</span><span class="sxs-lookup"><span data-stu-id="b236f-173">Without this option, you may encounter behavior as described in [Cannot SSH tooLinux VM due tooFSTAB errors](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/).</span></span>

    <span data-ttu-id="b236f-174">您現在可以測試 hello 檔案系統已裝載卸載，並再重新掛載 hello 檔案系統，也就利用正常 hello 範例掛接點`/datadrive`建立 hello 中稍早步驟：</span><span class="sxs-lookup"><span data-stu-id="b236f-174">You can now test that hello file system is mounted properly by unmounting and then remounting hello file system, i.e. using hello example mount point `/datadrive` created in hello earlier steps:</span></span>

    ```bash
    sudo umount /datadrive
    sudo mount /datadrive
    ```

    <span data-ttu-id="b236f-175">如果 hello`mount`命令會產生錯誤，請檢查檔 hello /etc/hosts fstab 正確語法。</span><span class="sxs-lookup"><span data-stu-id="b236f-175">If hello `mount` command produces an error, check hello /etc/fstab file for correct syntax.</span></span> <span data-ttu-id="b236f-176">如果還有建立其他資料磁碟機或磁碟分割，也請分別在 /etc/fstab 中分別輸入它們。</span><span class="sxs-lookup"><span data-stu-id="b236f-176">If additional data drives or partitions are created, enter them into /etc/fstab separately as well.</span></span>

    <span data-ttu-id="b236f-177">請使用這個命令可寫入 hello 磁碟機：</span><span class="sxs-lookup"><span data-stu-id="b236f-177">Make hello drive writable by using this command:</span></span>

    ```bash
    sudo chmod go+w /datadrive
    ```

    > [!NOTE]
    > <span data-ttu-id="b236f-178">接著移除資料磁碟，而不編輯 fstab 可能會導致 hello VM toofail tooboot。</span><span class="sxs-lookup"><span data-stu-id="b236f-178">Subsequently removing a data disk without editing fstab could cause hello VM toofail tooboot.</span></span> <span data-ttu-id="b236f-179">如果這是常見的發生次數，多數散發提供任一 hello`nofail`及/或`nobootwait`fstab 選項，可讓系統 tooboot，即使 hello 磁碟失敗 toomount 在開機時。</span><span class="sxs-lookup"><span data-stu-id="b236f-179">If this is a common occurrence, most distributions provide either hello `nofail` and/or `nobootwait` fstab options that allow a system tooboot even if hello disk fails toomount at boot time.</span></span> <span data-ttu-id="b236f-180">請查閱散發套件的文件，以取得這些參數的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="b236f-180">Consult your distribution's documentation for more information on these parameters.</span></span>

### <a name="trimunmap-support-for-linux-in-azure"></a><span data-ttu-id="b236f-181">Azure 中 Linux 的 TRIM/UNMAP 支援</span><span class="sxs-lookup"><span data-stu-id="b236f-181">TRIM/UNMAP support for Linux in Azure</span></span>
<span data-ttu-id="b236f-182">某些 Linux 核心支援 TRIM/UNMAP 作業 toodiscard hello 磁碟上未使用的區塊。</span><span class="sxs-lookup"><span data-stu-id="b236f-182">Some Linux kernels support TRIM/UNMAP operations toodiscard unused blocks on hello disk.</span></span> <span data-ttu-id="b236f-183">這些運算全都是主要適用於標準儲存體 tooinform 刪除頁面的 Azure 不再有效，以及可以捨棄。</span><span class="sxs-lookup"><span data-stu-id="b236f-183">These operations are primarily useful in standard storage tooinform Azure that deleted pages are no longer valid and can be discarded.</span></span> <span data-ttu-id="b236f-184">如果您建立大型檔案，然後再將它們刪除，捨棄頁面可以節省成本。</span><span class="sxs-lookup"><span data-stu-id="b236f-184">Discarding pages can save cost if you create large files and then delete them.</span></span>

<span data-ttu-id="b236f-185">有兩種 tooenable TRIM 支援在 Linux VM 中。</span><span class="sxs-lookup"><span data-stu-id="b236f-185">There are two ways tooenable TRIM support in your Linux VM.</span></span> <span data-ttu-id="b236f-186">像往常一樣，參閱您的發佈 hello 建議的方法包括：</span><span class="sxs-lookup"><span data-stu-id="b236f-186">As usual, consult your distribution for hello recommended approach:</span></span>

* <span data-ttu-id="b236f-187">使用 hello`discard`掛接中的選項`/etc/fstab`，例如：</span><span class="sxs-lookup"><span data-stu-id="b236f-187">Use hello `discard` mount option in `/etc/fstab`, for example:</span></span>

    ```sh
    UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,discard   1   2
    ```

* <span data-ttu-id="b236f-188">在某些情況下 hello`discard`選項可能會影響效能。</span><span class="sxs-lookup"><span data-stu-id="b236f-188">In some cases hello `discard` option may have performance implications.</span></span> <span data-ttu-id="b236f-189">或者，您可以在其中執行 hello`fstrim`命令手動從 hello 命令列，或將它加入 tooyour crontab toorun 定期：</span><span class="sxs-lookup"><span data-stu-id="b236f-189">Alternatively, you can run hello `fstrim` command manually from hello command line, or add it tooyour crontab toorun regularly:</span></span>
  
    <span data-ttu-id="b236f-190">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="b236f-190">**Ubuntu**</span></span>
  
    ```bash
    sudo apt-get install util-linux
    sudo fstrim /datadrive
    ```
  
    <span data-ttu-id="b236f-191">**RHEL/CentOS**</span><span class="sxs-lookup"><span data-stu-id="b236f-191">**RHEL/CentOS**</span></span>
  
    ```bash
    sudo yum install util-linux
    sudo fstrim /datadrive
    ```

## <a name="troubleshooting"></a><span data-ttu-id="b236f-192">疑難排解</span><span class="sxs-lookup"><span data-stu-id="b236f-192">Troubleshooting</span></span>
[!INCLUDE [virtual-machines-linux-lunzero](../../../../includes/virtual-machines-linux-lunzero.md)]

## <a name="next-steps"></a><span data-ttu-id="b236f-193">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b236f-193">Next Steps</span></span>
<span data-ttu-id="b236f-194">閱讀更多關於使用 Linux VM hello 下列文章中：</span><span class="sxs-lookup"><span data-stu-id="b236f-194">You can read more about using your Linux VM in hello following articles:</span></span>

* <span data-ttu-id="b236f-195">[如何 toolog tooa 執行 Linux 的虛擬機器上][Logon]</span><span class="sxs-lookup"><span data-stu-id="b236f-195">[How toolog on tooa virtual machine running Linux][Logon]</span></span>
* [<span data-ttu-id="b236f-196">如何 toodetach 來自 Linux 虛擬機器的磁碟</span><span class="sxs-lookup"><span data-stu-id="b236f-196">How toodetach a disk from a Linux virtual machine</span></span>](detach-disk.md)
* [<span data-ttu-id="b236f-197">使用 Azure CLI hello 與 hello 傳統部署模型</span><span class="sxs-lookup"><span data-stu-id="b236f-197">Using hello Azure CLI with hello Classic deployment model</span></span>](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)
* [<span data-ttu-id="b236f-198">在 Azure 中的 Linux VM 上設定 RAID</span><span class="sxs-lookup"><span data-stu-id="b236f-198">Configure RAID on a Linux VM in Azure</span></span>](../configure-raid.md)
* [<span data-ttu-id="b236f-199">設定 Azure 中 Linux VM 的 LVM</span><span class="sxs-lookup"><span data-stu-id="b236f-199">Configure LVM on a Linux VM in Azure</span></span>](../configure-lvm.md)

<!--Link references-->
[Agent]:../agent-user-guide.md
[Logon]:../mac-create-ssh-keys.md
