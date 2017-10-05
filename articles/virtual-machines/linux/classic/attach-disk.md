---
title: "將磁碟附加至 Azure 中的 Linux VM | Microsoft Docs"
description: "了解如何使用傳統部署模型將資料磁碟連接至 Linux VM，並初始化磁碟，使其可供使用"
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
ms.openlocfilehash: 017ba7197e11c2b222082833d5acabb9e542b762
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-attach-a-data-disk-to-a-linux-virtual-machine"></a><span data-ttu-id="1fd34-103">如何將資料磁碟連接至 Linux 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="1fd34-103">How to Attach a Data Disk to a Linux Virtual Machine</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="1fd34-104">Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="1fd34-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="1fd34-105">本文涵蓋之內容包括使用傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="1fd34-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="1fd34-106">Microsoft 建議讓大部分的新部署使用資源管理員模式。</span><span class="sxs-lookup"><span data-stu-id="1fd34-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="1fd34-107">參閱如何[使用 Resource Manager 部署模型連接資料磁碟](../add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="1fd34-107">See how to [attach a data disk using the Resource Manager deployment model](../add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="1fd34-108">您可以將空的磁碟和含有資料的磁碟連接到 Azure VM。</span><span class="sxs-lookup"><span data-stu-id="1fd34-108">You can attach both empty disks and disks that contain data to your Azure VMs.</span></span> <span data-ttu-id="1fd34-109">這兩種類型的磁碟都是位於 Azure 儲存體帳戶中的 .vhd 檔案。</span><span class="sxs-lookup"><span data-stu-id="1fd34-109">Both types of disks are .vhd files that reside in an Azure storage account.</span></span> <span data-ttu-id="1fd34-110">就像將任何磁碟新增到 Linux 機器一樣，連接磁碟之後，您必須將磁碟初始化並格式化，它才可供使用。</span><span class="sxs-lookup"><span data-stu-id="1fd34-110">As with adding any disk to a Linux machine, after you attach the disk you need to initialize and format it so it's ready for use.</span></span> <span data-ttu-id="1fd34-111">本文將會詳細說明連接空的磁碟和連接含有資料的磁碟到 VM，以及初始化和格式化新磁碟的方法。</span><span class="sxs-lookup"><span data-stu-id="1fd34-111">This article details attaching both empty disks and disks already containing data to your VMs, as well as how to then initialize and format a new disk.</span></span>

> [!NOTE]
> <span data-ttu-id="1fd34-112">最好使用一或多個不同的磁碟來儲存虛擬機器的資料。</span><span class="sxs-lookup"><span data-stu-id="1fd34-112">It's a best practice to use one or more separate disks to store a virtual machine's data.</span></span> <span data-ttu-id="1fd34-113">當您建立 Azure 虛擬機器時，它會有作業系統磁碟和暫存磁碟。</span><span class="sxs-lookup"><span data-stu-id="1fd34-113">When you create an Azure virtual machine, it has an operating system disk and a temporary disk.</span></span> <span data-ttu-id="1fd34-114">**請勿使用暫存磁碟來儲存持續資料。**</span><span class="sxs-lookup"><span data-stu-id="1fd34-114">**Do not use the temporary disk to store persistent data.**</span></span> <span data-ttu-id="1fd34-115">顧名思義，它只提供暫存儲存空間。</span><span class="sxs-lookup"><span data-stu-id="1fd34-115">As the name implies, it provides temporary storage only.</span></span> <span data-ttu-id="1fd34-116">它並不提供備援或備份，因為它不在 Azure 儲存體內。</span><span class="sxs-lookup"><span data-stu-id="1fd34-116">It offers no redundancy or backup because it doesn't reside in Azure storage.</span></span>
> <span data-ttu-id="1fd34-117">暫存磁碟通常是由 Azure Linux 代理程式管理，並自動掛接到 **/mnt/resource** (或 Ubuntu 映像中的**/mnt**)。</span><span class="sxs-lookup"><span data-stu-id="1fd34-117">The temporary disk is typically managed by the Azure Linux Agent and automatically mounted to **/mnt/resource** (or **/mnt** on Ubuntu images).</span></span> <span data-ttu-id="1fd34-118">另一方面，Linux 核心可能會將資料磁碟命名為 `/dev/sdc`之類的名稱，而您必須分割、格式化及掛接此資源。</span><span class="sxs-lookup"><span data-stu-id="1fd34-118">On the other hand, a data disk might be named by the Linux kernel something like `/dev/sdc`, and you need to partition, format, and mount this resource.</span></span> <span data-ttu-id="1fd34-119">如需詳細資訊，請參閱 [Azure Linux 代理程式使用者指南][Agent]。</span><span class="sxs-lookup"><span data-stu-id="1fd34-119">See the [Azure Linux Agent User Guide][Agent] for details.</span></span>
> 
> 

[!INCLUDE [howto-attach-disk-windows-linux](../../../../includes/howto-attach-disk-linux.md)]

## <a name="initialize-a-new-data-disk-in-linux"></a><span data-ttu-id="1fd34-120">在 Linux 中初始化新的資料磁碟</span><span class="sxs-lookup"><span data-stu-id="1fd34-120">Initialize a new data disk in Linux</span></span>
1. <span data-ttu-id="1fd34-121">SSH 連線到您的 VM。</span><span class="sxs-lookup"><span data-stu-id="1fd34-121">SSH to your VM.</span></span> <span data-ttu-id="1fd34-122">如需詳細資訊，請參閱[如何登入執行 Linux 的虛擬機器][Logon]。</span><span class="sxs-lookup"><span data-stu-id="1fd34-122">For more information, see [How to log on to a virtual machine running Linux][Logon].</span></span>
2. <span data-ttu-id="1fd34-123">接下來您需要尋找資料磁碟的裝置識別碼以進行初始化。</span><span class="sxs-lookup"><span data-stu-id="1fd34-123">Next you need to find the device identifier for the data disk to initialize.</span></span> <span data-ttu-id="1fd34-124">作法有二：</span><span class="sxs-lookup"><span data-stu-id="1fd34-124">There are two ways to do that:</span></span>
   
    <span data-ttu-id="1fd34-125">a) Grep SCSI 裝置中的記錄檔，如以下命令︰</span><span class="sxs-lookup"><span data-stu-id="1fd34-125">a) Grep for SCSI devices in the logs, such as in the following command:</span></span>
   
    ```bash
    sudo grep SCSI /var/log/messages
    ```
   
    <span data-ttu-id="1fd34-126">針對最新的 Ubuntu 散發套件，您可能需要使用 `sudo grep SCSI /var/log/syslog`，因為預設可能會停用記錄到 `/var/log/messages` 的功能。</span><span class="sxs-lookup"><span data-stu-id="1fd34-126">For recent Ubuntu distributions, you may need to use `sudo grep SCSI /var/log/syslog` because logging to `/var/log/messages` might be disabled by default.</span></span>
   
    <span data-ttu-id="1fd34-127">在出現的訊息中，您可以找到最後一個新增之資料磁碟的識別碼。</span><span class="sxs-lookup"><span data-stu-id="1fd34-127">You can find the identifier of the last data disk that was added in the messages that are displayed.</span></span>
   
    ![取得磁碟訊息](./media/attach-disk/scsidisklog.png)
   
    <span data-ttu-id="1fd34-129">或</span><span class="sxs-lookup"><span data-stu-id="1fd34-129">OR</span></span>
   
    <span data-ttu-id="1fd34-130">b) 使用 `lsscsi` 命令來找出裝置識別碼。</span><span class="sxs-lookup"><span data-stu-id="1fd34-130">b) Use the `lsscsi` command to find out the device id.</span></span> <span data-ttu-id="1fd34-131">您可透過 `yum install lsscsi` (Red Hat 式散發) 或 `apt-get install lsscsi`(Debian 式散發) 來安裝 `lsscsi`。</span><span class="sxs-lookup"><span data-stu-id="1fd34-131">`lsscsi` can be installed by either `yum install lsscsi` (on Red Hat based distributions) or `apt-get install lsscsi` (on Debian based distributions).</span></span> <span data-ttu-id="1fd34-132">您可以透過磁碟的 *LUN* (亦稱為 **邏輯單元編號**) 找到您所需的磁碟。</span><span class="sxs-lookup"><span data-stu-id="1fd34-132">You can find the disk you are looking for by its *lun* or **logical unit number**.</span></span> <span data-ttu-id="1fd34-133">例如，您可從 `azure vm disk list <virtual-machine>` 輕易看到所附加磁碟的 *lun*，如下所示：</span><span class="sxs-lookup"><span data-stu-id="1fd34-133">For example, the *lun* for the disks you attached can be easily seen from `azure vm disk list <virtual-machine>` as:</span></span>

    ```azurecli
    azure vm disk list myVM
    ```

    <span data-ttu-id="1fd34-134">輸出大致如下：</span><span class="sxs-lookup"><span data-stu-id="1fd34-134">The output is similar to the following:</span></span>

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
   
    <span data-ttu-id="1fd34-135">將此資料與相同範例虛擬機器的 `lsscsi` 輸出做比較：</span><span class="sxs-lookup"><span data-stu-id="1fd34-135">Compare this data with the output of `lsscsi` for the same sample virtual machine:</span></span>
   
    ```bash
    [1:0:0:0]    cd/dvd  Msft     Virtual CD/ROM   1.0   /dev/sr0
    [2:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sda
    [3:0:1:0]    disk    Msft     Virtual Disk     1.0   /dev/sdb
    [5:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sdc
    ```
   
    <span data-ttu-id="1fd34-136">在每個資料列的 Tuple 中，最後一個數字即為 *LUN*。</span><span class="sxs-lookup"><span data-stu-id="1fd34-136">The last number in the tuple in each row is the *lun*.</span></span> <span data-ttu-id="1fd34-137">如需詳細資訊，請參閱 `man lsscsi` 。</span><span class="sxs-lookup"><span data-stu-id="1fd34-137">See `man lsscsi` for more information.</span></span>
3. <span data-ttu-id="1fd34-138">出現提示時，輸入下列命令來建立裝置：</span><span class="sxs-lookup"><span data-stu-id="1fd34-138">At the prompt, type the following command to create your device:</span></span>
   
    ```bash
    sudo fdisk /dev/sdc
    ```

4. <span data-ttu-id="1fd34-139">出現提示時，輸入 **n** 建立磁碟分割。</span><span class="sxs-lookup"><span data-stu-id="1fd34-139">When prompted, type **n** to create a partition.</span></span>

    ![建立裝置](./media/attach-disk/fdisknewpartition.png)

5. <span data-ttu-id="1fd34-141">出現提示時，輸入 **p** 以將磁碟分割設為主要磁碟分割。</span><span class="sxs-lookup"><span data-stu-id="1fd34-141">When prompted, type **p** to make the partition the primary partition.</span></span> <span data-ttu-id="1fd34-142">輸入 **1** 以將它設為第一個磁碟分割，然後按 Enter 來接受預設的磁柱值。</span><span class="sxs-lookup"><span data-stu-id="1fd34-142">Type **1** to make it the first partition, and then type enter to accept the default value for the cylinder.</span></span> <span data-ttu-id="1fd34-143">在某些系統上，它可能會顯示第一個和最後一個磁區的預設值，而不是圓柱圖。</span><span class="sxs-lookup"><span data-stu-id="1fd34-143">On some systems, it can show the default values of the first and the last sectors, instead of the cylinder.</span></span> <span data-ttu-id="1fd34-144">您可以選擇接受這些預設值。</span><span class="sxs-lookup"><span data-stu-id="1fd34-144">You can choose to accept these defaults.</span></span>

    ![建立磁碟分割](./media/attach-disk/fdisknewpartdetails.png)


6. <span data-ttu-id="1fd34-146">輸入 **p** 查看目前分割之磁碟的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="1fd34-146">Type **p** to see the details about the disk that is being partitioned.</span></span>

    ![列出磁碟資訊](./media/attach-disk/fdiskpartitiondetails.png)


7. <span data-ttu-id="1fd34-148">輸入 **w** 寫入磁碟的設定。</span><span class="sxs-lookup"><span data-stu-id="1fd34-148">Type **w** to write the settings for the disk.</span></span>

    ![寫入磁碟變更](./media/attach-disk/fdiskwritedisk.png)

8. <span data-ttu-id="1fd34-150">您現在可以在新的磁碟分割上建立檔案系統。</span><span class="sxs-lookup"><span data-stu-id="1fd34-150">Now you can create the file system on the new partition.</span></span> <span data-ttu-id="1fd34-151">在裝置識別碼後加上磁碟分割編號 (在以下範例中為 `/dev/sdc1`)。</span><span class="sxs-lookup"><span data-stu-id="1fd34-151">Append the partition number to the device ID (in the following example `/dev/sdc1`).</span></span> <span data-ttu-id="1fd34-152">以下範例會在 /dev/sdc1 上建立 ext4 磁碟分割：</span><span class="sxs-lookup"><span data-stu-id="1fd34-152">The following example creates an ext4 partition on /dev/sdc1:</span></span>
   
    ```bash
    sudo mkfs -t ext4 /dev/sdc1
    ```
   
    ![建立檔案系統](./media/attach-disk/mkfsext4.png)
   
   > [!NOTE]
   > <span data-ttu-id="1fd34-154">SuSE Linux Enterprise 11 系統針對 ext4 檔案系統只支援唯讀存取。</span><span class="sxs-lookup"><span data-stu-id="1fd34-154">SuSE Linux Enterprise 11 systems only support read-only access for ext4 file systems.</span></span> <span data-ttu-id="1fd34-155">針對這些系統，建議您將新檔案系統格式化為 ext3，而非 ext4。</span><span class="sxs-lookup"><span data-stu-id="1fd34-155">For these systems, it is recommended to format the new file system as ext3 rather than ext4.</span></span>

9. <span data-ttu-id="1fd34-156">建立目錄以掛接新的檔案系統，如下所示：</span><span class="sxs-lookup"><span data-stu-id="1fd34-156">Make a directory to mount the new file system, as follows:</span></span>
   
    ```bash
    sudo mkdir /datadrive
    ```

10. <span data-ttu-id="1fd34-157">最後您可以掛接磁碟機，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="1fd34-157">Finally you can mount the drive, as follows:</span></span>
   
    ```bash
    sudo mount /dev/sdc1 /datadrive
    ```
   
    <span data-ttu-id="1fd34-158">資料磁碟現在可以當做 **/datadrive**來使用。</span><span class="sxs-lookup"><span data-stu-id="1fd34-158">The data disk is now ready to use as **/datadrive**.</span></span>
   
    ![建立目錄和掛接磁碟](./media/attach-disk/mkdirandmount.png)

11. <span data-ttu-id="1fd34-160">將新的磁碟機新增至 /etc/fstab：</span><span class="sxs-lookup"><span data-stu-id="1fd34-160">Add the new drive to /etc/fstab:</span></span>
   
    <span data-ttu-id="1fd34-161">為了確保重新開機之後自動重新掛接磁碟機，必須將磁碟機新增至 /etc/fstab 檔案。</span><span class="sxs-lookup"><span data-stu-id="1fd34-161">To ensure the drive is remounted automatically after a reboot it must be added to the /etc/fstab file.</span></span> <span data-ttu-id="1fd34-162">此外，強烈建議在 /et/fstab 中使用全域唯一識別碼 (Universally Unique IDentifier, UUID) 來參考磁碟機，而不只是裝置名稱 (例如，/dev/sdc1)。</span><span class="sxs-lookup"><span data-stu-id="1fd34-162">In addition, it is highly recommended that the UUID (Universally Unique IDentifier) is used in /etc/fstab to refer to the drive rather than just the device name (i.e. /dev/sdc1).</span></span> <span data-ttu-id="1fd34-163">使用 UUID 可避免當作業系統在開機期間偵測到磁碟錯誤時，將不正確的磁碟掛接到指定的位置，又接著將這些裝置識別碼指派給任何其餘的資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="1fd34-163">Using the UUID avoids the incorrect disk being mounted to a given location if the OS detects a disk error during boot and any remaining data disks then being assigned those device IDs.</span></span> <span data-ttu-id="1fd34-164">若要尋找新磁碟機的 UUID，您可以使用 **blkid** 公用程式：</span><span class="sxs-lookup"><span data-stu-id="1fd34-164">To find the UUID of the new drive, you can use the **blkid** utility:</span></span>
   
    ```bash
    sudo -i blkid
    ```
   
    <span data-ttu-id="1fd34-165">輸出大致如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="1fd34-165">The output looks similar to the following example:</span></span>
   
    ```bash
    /dev/sda1: UUID="11111111-1b1b-1c1c-1d1d-1e1e1e1e1e1e" TYPE="ext4"
    /dev/sdb1: UUID="22222222-2b2b-2c2c-2d2d-2e2e2e2e2e2e" TYPE="ext4"
    /dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
    ```

    > [!NOTE]
    > <span data-ttu-id="1fd34-166">不當編輯 **/etc/fstab** 檔案會導致系統無法開機。</span><span class="sxs-lookup"><span data-stu-id="1fd34-166">Improperly editing the **/etc/fstab** file could result in an unbootable system.</span></span> <span data-ttu-id="1fd34-167">如果不確定，請參閱散發套件的文件，以取得如何適當編輯此檔案的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="1fd34-167">If unsure, refer to the distribution's documentation for information on how to properly edit this file.</span></span> <span data-ttu-id="1fd34-168">在編輯之前，也建議先備份 /etc/fstab 檔案。</span><span class="sxs-lookup"><span data-stu-id="1fd34-168">It is also recommended that a backup of the /etc/fstab file is created before editing.</span></span>

    <span data-ttu-id="1fd34-169">接下來，在文字編輯器中開啟 **/etc/fstab** 檔案：</span><span class="sxs-lookup"><span data-stu-id="1fd34-169">Next, open the **/etc/fstab** file in a text editor:</span></span>

    ```bash
    sudo vi /etc/fstab
    ```

    <span data-ttu-id="1fd34-170">在此範例中，我們會使用先前步驟所建立之新的 **/dev/sdc1** 裝置的 UUID 值，並使用掛接點 **/datadrive**。</span><span class="sxs-lookup"><span data-stu-id="1fd34-170">In this example, we use the UUID value for the new **/dev/sdc1** device that was created in the previous steps, and the mountpoint **/datadrive**.</span></span> <span data-ttu-id="1fd34-171">在 **/etc/fstab** 檔案的結尾加入以下程式碼：</span><span class="sxs-lookup"><span data-stu-id="1fd34-171">Add the following line to the end of the **/etc/fstab** file:</span></span>

    ```sh
    UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,nofail   1   2
    ```

    <span data-ttu-id="1fd34-172">或者，在基於 SuSE Linux 的系統上，您可能需要使用稍微不同的格式：</span><span class="sxs-lookup"><span data-stu-id="1fd34-172">Or, on systems based on SuSE Linux you may need to use a slightly different format:</span></span>

    ```sh
    /dev/disk/by-uuid/33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext3   defaults,nofail   1   2
    ```

    > [!NOTE]
    > <span data-ttu-id="1fd34-173">`nofail` 選項可確保即使檔案系統已損毀或磁碟在開機時並不存在，仍然會啟動 VM。</span><span class="sxs-lookup"><span data-stu-id="1fd34-173">The `nofail` option ensures that the VM starts even if the filesystem is corrupt or the disk does not exist at boot time.</span></span> <span data-ttu-id="1fd34-174">若不使用此選項，您可能會遇到[因為 FSTAB 錯誤所以無法 SSH 到 Linux VM](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/) 中所述的行為。</span><span class="sxs-lookup"><span data-stu-id="1fd34-174">Without this option, you may encounter behavior as described in [Cannot SSH to Linux VM due to FSTAB errors](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/).</span></span>

    <span data-ttu-id="1fd34-175">您現在可以將檔案系統取消掛接後再重新掛接 (例如</span><span class="sxs-lookup"><span data-stu-id="1fd34-175">You can now test that the file system is mounted properly by unmounting and then remounting the file system, i.e.</span></span> <span data-ttu-id="1fd34-176">使用在先前步驟中建立的範例掛接點 `/datadrive`)，來測試是否已正確掛接檔案系統：</span><span class="sxs-lookup"><span data-stu-id="1fd34-176">using the example mount point `/datadrive` created in the earlier steps:</span></span>

    ```bash
    sudo umount /datadrive
    sudo mount /datadrive
    ```

    <span data-ttu-id="1fd34-177">如果 `mount` 命令發生錯誤，請檢查 /etc/fstab 檔案的語法是否正確。</span><span class="sxs-lookup"><span data-stu-id="1fd34-177">If the `mount` command produces an error, check the /etc/fstab file for correct syntax.</span></span> <span data-ttu-id="1fd34-178">如果還有建立其他資料磁碟機或磁碟分割，也請分別在 /etc/fstab 中分別輸入它們。</span><span class="sxs-lookup"><span data-stu-id="1fd34-178">If additional data drives or partitions are created, enter them into /etc/fstab separately as well.</span></span>

    <span data-ttu-id="1fd34-179">使用下列命令將磁碟機設為可寫入：</span><span class="sxs-lookup"><span data-stu-id="1fd34-179">Make the drive writable by using this command:</span></span>

    ```bash
    sudo chmod go+w /datadrive
    ```

    > [!NOTE]
    > <span data-ttu-id="1fd34-180">後續移除資料磁碟而不編輯 fstab，可能會造成 VM 無法開機。</span><span class="sxs-lookup"><span data-stu-id="1fd34-180">Subsequently removing a data disk without editing fstab could cause the VM to fail to boot.</span></span> <span data-ttu-id="1fd34-181">如果這是常見的情況，大多數散發套件都會提供 `nofail` 和/或 `nobootwait` fstab 選項，可讓系統在即使開機時無法掛接磁碟的情況下也能開機。</span><span class="sxs-lookup"><span data-stu-id="1fd34-181">If this is a common occurrence, most distributions provide either the `nofail` and/or `nobootwait` fstab options that allow a system to boot even if the disk fails to mount at boot time.</span></span> <span data-ttu-id="1fd34-182">請查閱散發套件的文件，以取得這些參數的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="1fd34-182">Consult your distribution's documentation for more information on these parameters.</span></span>

### <a name="trimunmap-support-for-linux-in-azure"></a><span data-ttu-id="1fd34-183">Azure 中 Linux 的 TRIM/UNMAP 支援</span><span class="sxs-lookup"><span data-stu-id="1fd34-183">TRIM/UNMAP support for Linux in Azure</span></span>
<span data-ttu-id="1fd34-184">有些 Linux 核心會支援 TRIM/UNMAP 作業以捨棄磁碟上未使用的區塊。</span><span class="sxs-lookup"><span data-stu-id="1fd34-184">Some Linux kernels support TRIM/UNMAP operations to discard unused blocks on the disk.</span></span> <span data-ttu-id="1fd34-185">這些作業主要是在標準儲存體中相當實用，可用來通知 Azure 已刪除的頁面已不再有效而可予以捨棄。</span><span class="sxs-lookup"><span data-stu-id="1fd34-185">These operations are primarily useful in standard storage to inform Azure that deleted pages are no longer valid and can be discarded.</span></span> <span data-ttu-id="1fd34-186">如果您建立大型檔案，然後再將它們刪除，捨棄頁面可以節省成本。</span><span class="sxs-lookup"><span data-stu-id="1fd34-186">Discarding pages can save cost if you create large files and then delete them.</span></span>

<span data-ttu-id="1fd34-187">有兩種方式可在 Linux VM 中啟用 TRIM 支援。</span><span class="sxs-lookup"><span data-stu-id="1fd34-187">There are two ways to enable TRIM support in your Linux VM.</span></span> <span data-ttu-id="1fd34-188">像往常一樣，請參閱您的散發套件以了解建議的方法︰</span><span class="sxs-lookup"><span data-stu-id="1fd34-188">As usual, consult your distribution for the recommended approach:</span></span>

* <span data-ttu-id="1fd34-189">在 `/etc/fstab` 中使用 `discard` 掛接選項，例如：</span><span class="sxs-lookup"><span data-stu-id="1fd34-189">Use the `discard` mount option in `/etc/fstab`, for example:</span></span>

    ```sh
    UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,discard   1   2
    ```

* <span data-ttu-id="1fd34-190">在某些情況下，`discard` 選項可能會影響效能。</span><span class="sxs-lookup"><span data-stu-id="1fd34-190">In some cases the `discard` option may have performance implications.</span></span> <span data-ttu-id="1fd34-191">或者，您也可以從命令列手動執行 `fstrim` 命令，或將它新增到 crontab 來定期執行︰</span><span class="sxs-lookup"><span data-stu-id="1fd34-191">Alternatively, you can run the `fstrim` command manually from the command line, or add it to your crontab to run regularly:</span></span>
  
    <span data-ttu-id="1fd34-192">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="1fd34-192">**Ubuntu**</span></span>
  
    ```bash
    sudo apt-get install util-linux
    sudo fstrim /datadrive
    ```
  
    <span data-ttu-id="1fd34-193">**RHEL/CentOS**</span><span class="sxs-lookup"><span data-stu-id="1fd34-193">**RHEL/CentOS**</span></span>
  
    ```bash
    sudo yum install util-linux
    sudo fstrim /datadrive
    ```

## <a name="troubleshooting"></a><span data-ttu-id="1fd34-194">疑難排解</span><span class="sxs-lookup"><span data-stu-id="1fd34-194">Troubleshooting</span></span>
[!INCLUDE [virtual-machines-linux-lunzero](../../../../includes/virtual-machines-linux-lunzero.md)]

## <a name="next-steps"></a><span data-ttu-id="1fd34-195">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1fd34-195">Next Steps</span></span>
<span data-ttu-id="1fd34-196">您可以閱讀下列文章來進一步了解如何使用 Linux VM：</span><span class="sxs-lookup"><span data-stu-id="1fd34-196">You can read more about using your Linux VM in the following articles:</span></span>

* <span data-ttu-id="1fd34-197">[如何登入執行 Linux 的虛擬機器][Logon]</span><span class="sxs-lookup"><span data-stu-id="1fd34-197">[How to log on to a virtual machine running Linux][Logon]</span></span>
* [<span data-ttu-id="1fd34-198">如何從 Linux 虛擬機器卸離磁碟</span><span class="sxs-lookup"><span data-stu-id="1fd34-198">How to detach a disk from a Linux virtual machine</span></span>](detach-disk.md)
* [<span data-ttu-id="1fd34-199">搭配傳統部署模型使用 Azuer CLI</span><span class="sxs-lookup"><span data-stu-id="1fd34-199">Using the Azure CLI with the Classic deployment model</span></span>](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)
* [<span data-ttu-id="1fd34-200">在 Azure 中的 Linux VM 上設定 RAID</span><span class="sxs-lookup"><span data-stu-id="1fd34-200">Configure RAID on a Linux VM in Azure</span></span>](../configure-raid.md)
* [<span data-ttu-id="1fd34-201">設定 Azure 中 Linux VM 的 LVM</span><span class="sxs-lookup"><span data-stu-id="1fd34-201">Configure LVM on a Linux VM in Azure</span></span>](../configure-lvm.md)

<!--Link references-->
[Agent]:../agent-user-guide.md
[Logon]:../mac-create-ssh-keys.md
