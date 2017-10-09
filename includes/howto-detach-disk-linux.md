<span data-ttu-id="9fea1-101">當您不再需要的資料磁碟附加的 tooa 虛擬機器 (VM) 時，您可以輕易地中斷。</span><span class="sxs-lookup"><span data-stu-id="9fea1-101">When you no longer need a data disk that's attached tooa virtual machine (VM), you can easily detach it.</span></span> <span data-ttu-id="9fea1-102">當您從中斷連接磁碟 hello VM 時，hello 磁碟不是從儲存體移除它。</span><span class="sxs-lookup"><span data-stu-id="9fea1-102">When you detach a disk from hello VM, hello disk is not removed it from storage.</span></span> <span data-ttu-id="9fea1-103">若要再次 toouse hello 現有資料 hello 磁碟上的，您可以將它重新附加 toohello 相同的 VM 或另一個。</span><span class="sxs-lookup"><span data-stu-id="9fea1-103">If you want toouse hello existing data on hello disk again, you can reattach it toohello same VM, or another one.</span></span>  

> [!NOTE]
> <span data-ttu-id="9fea1-104">Azure 中的 VM 使用不同類型的磁碟 - 作業系統磁碟、本機暫存磁碟，以及選擇性的資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="9fea1-104">A VM in Azure uses different types of disks - an operating system disk, a local temporary disk, and optional data disks.</span></span> <span data-ttu-id="9fea1-105">如需詳細資訊，請參閱[有關虛擬機器的磁碟和 VHD](../articles/virtual-machines/linux/about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="9fea1-105">For details, see [About Disks and VHDs for Virtual Machines](../articles/virtual-machines/linux/about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="9fea1-106">除非您也可以刪除 hello VM，您無法卸離作業系統磁碟。</span><span class="sxs-lookup"><span data-stu-id="9fea1-106">You cannot detach an operating system disk unless you also delete hello VM.</span></span>

## <a name="find-hello-disk"></a><span data-ttu-id="9fea1-107">找不到 hello 磁碟</span><span class="sxs-lookup"><span data-stu-id="9fea1-107">Find hello disk</span></span>
<span data-ttu-id="9fea1-108">您可以卸離來自 VM 的磁碟必須先 toofind 出 hello 識別碼 hello 磁碟 toobe 卸離的 LUN 編號。</span><span class="sxs-lookup"><span data-stu-id="9fea1-108">Before you can detach a disk from a VM you need toofind out hello LUN number, which is an identifier for hello disk toobe detached.</span></span> <span data-ttu-id="9fea1-109">toodo，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="9fea1-109">toodo that, follow these steps:</span></span>

1. <span data-ttu-id="9fea1-110">開啟 Azure CLI 和[連接 tooyour Azure 訂用帳戶](../articles/xplat-cli-connect.md)。</span><span class="sxs-lookup"><span data-stu-id="9fea1-110">Open Azure CLI and [connect tooyour Azure subscription](../articles/xplat-cli-connect.md).</span></span> <span data-ttu-id="9fea1-111">確定處於 Azure 服務管理模式 (`azure config mode asm`)。</span><span class="sxs-lookup"><span data-stu-id="9fea1-111">Make sure you are in Azure Service Management mode (`azure config mode asm`).</span></span>
2. <span data-ttu-id="9fea1-112">找出哪些磁碟在附加的 tooyour VM。</span><span class="sxs-lookup"><span data-stu-id="9fea1-112">Find out which disks are attached tooyour VM.</span></span> <span data-ttu-id="9fea1-113">hello 下列範例會列出 hello 名為 VM 磁碟`myVM`:</span><span class="sxs-lookup"><span data-stu-id="9fea1-113">hello following example lists disks for hello VM named `myVM`:</span></span>

    ```azurecli
    azure vm disk list myVM
    ```

    <span data-ttu-id="9fea1-114">hello 輸出是 toohello 類似下列範例程式碼：</span><span class="sxs-lookup"><span data-stu-id="9fea1-114">hello output is similar toohello following example:</span></span>

    ```azurecli
    * Fetching disk images
    * Getting virtual machines
    * Getting VM disks
      data:    Lun  Size(GB)  Blob-Name                         OS
      data:    ---  --------  --------------------------------  -----
      data:         30        ubuntuVM-2645b8030676c8f8.vhd  Linux
      data:    0    30        myDataDisk.vhd
      info:    vm disk list command OK
    ```

3. <span data-ttu-id="9fea1-115">請注意 hello LUN 或 hello**邏輯單元編號**想 toodetach hello 磁碟。</span><span class="sxs-lookup"><span data-stu-id="9fea1-115">Note hello LUN or hello **logical unit number** for hello disk that you want toodetach.</span></span>

## <a name="remove-operating-system-references-toohello-disk"></a><span data-ttu-id="9fea1-116">移除作業系統參考 toohello 磁碟</span><span class="sxs-lookup"><span data-stu-id="9fea1-116">Remove operating system references toohello disk</span></span>
<span data-ttu-id="9fea1-117">卸離 hello 磁碟中的 hello Linux 客體之前, 您應該確定 hello 磁碟上的所有磁碟分割不在使用中。</span><span class="sxs-lookup"><span data-stu-id="9fea1-117">Before detaching hello disk from hello Linux guest, you should make sure that all partitions on hello disk are not in use.</span></span> <span data-ttu-id="9fea1-118">請確定該 hello 作業系統不會嘗試 tooremount 它們之後重新開機。</span><span class="sxs-lookup"><span data-stu-id="9fea1-118">Ensure that hello operating system does not attempt tooremount them after a reboot.</span></span> <span data-ttu-id="9fea1-119">下列步驟復原可能時所建立的 hello 組態[附加](../articles/virtual-machines/linux/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)hello 磁碟。</span><span class="sxs-lookup"><span data-stu-id="9fea1-119">These steps undo hello configuration you likely created when [attaching](../articles/virtual-machines/linux/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) hello disk.</span></span>

1. <span data-ttu-id="9fea1-120">使用 hello`lsscsi`命令 toodiscover hello 磁碟識別碼。</span><span class="sxs-lookup"><span data-stu-id="9fea1-120">Use hello `lsscsi` command toodiscover hello disk identifier.</span></span> <span data-ttu-id="9fea1-121">您可透過 `yum install lsscsi` (Red Hat 式散發) 或 `apt-get install lsscsi`(Debian 式散發) 來安裝 `lsscsi`。</span><span class="sxs-lookup"><span data-stu-id="9fea1-121">`lsscsi` can be installed by either `yum install lsscsi` (on Red Hat based distributions) or `apt-get install lsscsi` (on Debian based distributions).</span></span> <span data-ttu-id="9fea1-122">您可以找到您要使用的 LUN 編號 hello 尋找 hello 磁碟識別碼。</span><span class="sxs-lookup"><span data-stu-id="9fea1-122">You can find hello disk identifier you are looking for by using hello LUN number.</span></span> <span data-ttu-id="9fea1-123">hello hello tuple 中每個資料列中的最後一個號碼為 hello LUN。</span><span class="sxs-lookup"><span data-stu-id="9fea1-123">hello last number in hello tuple in each row is hello LUN.</span></span> <span data-ttu-id="9fea1-124">在下列範例從 hello `lsscsi`，LUN 0 太對應  */開發/sdc*</span><span class="sxs-lookup"><span data-stu-id="9fea1-124">In hello following example from `lsscsi`, LUN 0 maps too*/dev/sdc*</span></span>

    ```bash
    [1:0:0:0]    cd/dvd  Msft     Virtual CD/ROM   1.0   /dev/sr0
    [2:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sda
    [3:0:1:0]    disk    Msft     Virtual Disk     1.0   /dev/sdb
    [5:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sdc
    ```

2. <span data-ttu-id="9fea1-125">使用`fdisk -l <disk>`toodiscover hello 磁碟分割與 hello 磁碟 toobe 卸離相關聯。</span><span class="sxs-lookup"><span data-stu-id="9fea1-125">Use `fdisk -l <disk>` toodiscover hello partitions associated with hello disk toobe detached.</span></span> <span data-ttu-id="9fea1-126">hello 下列範例顯示 hello 輸出`/dev/sdc`:</span><span class="sxs-lookup"><span data-stu-id="9fea1-126">hello following example shows hello output for `/dev/sdc`:</span></span>

    ```bash
    Disk /dev/sdc: 1098.4 GB, 1098437885952 bytes, 2145386496 sectors
    Units = sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disk label type: dos
    Disk identifier: 0x5a1d2a1a
    
        Device Boot      Start         End      Blocks   Id  System
    /dev/sdc1            2048  2145386495  1072692224   83  Linux
    ```

3. <span data-ttu-id="9fea1-127">取消掛接 hello 磁碟列出每個資料分割。</span><span class="sxs-lookup"><span data-stu-id="9fea1-127">Unmount each partition listed for hello disk.</span></span> <span data-ttu-id="9fea1-128">hello 下例取消掛接`/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="9fea1-128">hello following example unmounts `/dev/sdc1`:</span></span>

    ```bash
    sudo umount /dev/sdc1
    ```

4. <span data-ttu-id="9fea1-129">使用 hello`blkid`命令 toodiscovery hello Uuid 之所有資料分割。</span><span class="sxs-lookup"><span data-stu-id="9fea1-129">Use hello `blkid` command toodiscovery hello UUIDs for all partitions.</span></span> <span data-ttu-id="9fea1-130">hello 輸出是 toohello 類似下列範例程式碼：</span><span class="sxs-lookup"><span data-stu-id="9fea1-130">hello output is similar toohello following example:</span></span>

    ```bash
    /dev/sda1: UUID="11111111-1b1b-1c1c-1d1d-1e1e1e1e1e1e" TYPE="ext4"
    /dev/sdb1: UUID="22222222-2b2b-2c2c-2d2d-2e2e2e2e2e2e" TYPE="ext4"
    /dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
    ```

5. <span data-ttu-id="9fea1-131">移除項目在 hello **/etc/hosts fstab**與 hello 裝置路徑或 Uuid hello 磁碟 toobe 卸離的所有資料分割相關聯的檔案。</span><span class="sxs-lookup"><span data-stu-id="9fea1-131">Remove entries in hello **/etc/fstab** file associated with either hello device paths or UUIDs for all partitions for hello disk toobe detached.</span></span>  <span data-ttu-id="9fea1-132">此範例中的項目可能是︰</span><span class="sxs-lookup"><span data-stu-id="9fea1-132">Entries for this example might be:</span></span>

    ```sh  
   UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults   1   2
   ```

    <span data-ttu-id="9fea1-133">或</span><span class="sxs-lookup"><span data-stu-id="9fea1-133">or</span></span>
   
   ```sh   
   /dev/sdc1   /datadrive   ext4   defaults   1   2
   ```

## <a name="detach-hello-disk"></a><span data-ttu-id="9fea1-134">卸離 hello 磁碟</span><span class="sxs-lookup"><span data-stu-id="9fea1-134">Detach hello disk</span></span>
<span data-ttu-id="9fea1-135">您找出 hello LUN 數目 hello 磁碟和移除的 hello 作業系統參考之後，您便準備好 toodetach 它：</span><span class="sxs-lookup"><span data-stu-id="9fea1-135">After you find hello LUN number of hello disk and removed hello operating system references, you're ready toodetach it:</span></span>

1. <span data-ttu-id="9fea1-136">從卸離 hello 選取的磁碟 hello 虛擬機器執行 hello 命令`azure vm disk detach
   <virtual-machine-name> <LUN>`。</span><span class="sxs-lookup"><span data-stu-id="9fea1-136">Detach hello selected disk from hello virtual machine by running hello command `azure vm disk detach
<virtual-machine-name> <LUN>`.</span></span> <span data-ttu-id="9fea1-137">hello 下列範例會卸離 LUN `0` hello 名為 VM 從`myVM`:</span><span class="sxs-lookup"><span data-stu-id="9fea1-137">hello following example detaches LUN `0` from hello VM named `myVM`:</span></span>
   
    ```azurecli
    azure vm disk detach myVM 0
    ```

2. <span data-ttu-id="9fea1-138">您可以檢查是否 hello 磁碟已卸離執行`azure vm disk list`一次。</span><span class="sxs-lookup"><span data-stu-id="9fea1-138">You can check if hello disk got detached by running `azure vm disk list` again.</span></span> <span data-ttu-id="9fea1-139">下列範例會檢查 hello hello 名為 VM `myVM`:</span><span class="sxs-lookup"><span data-stu-id="9fea1-139">hello following example checks hello VM named `myVM`:</span></span>
   
    ```azurecli
    azure vm disk list myVM
    ```

    <span data-ttu-id="9fea1-140">hello 輸出類似 toohello 之後，範例中，會顯示 hello 資料磁碟已不再連接：</span><span class="sxs-lookup"><span data-stu-id="9fea1-140">hello output is similar toohello following example, which shows hello data disk is no longer attached:</span></span>

    ```azurecli
    info:    Executing command vm disk list
   
   * Fetching disk images
   * Getting virtual machines
   * Getting VM disks
     data:    Lun  Size(GB)  Blob-Name                         OS
     data:    ---  --------  --------------------------------  -----
     data:         30        ubuntuVM-2645b8030676c8f8.vhd  Linux
     info:    vm disk list command OK
    ```

<span data-ttu-id="9fea1-141">hello 卸離磁碟留在儲存體，但已不再附加的 tooa 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="9fea1-141">hello detached disk remains in storage but is no longer attached tooa virtual machine.</span></span>

