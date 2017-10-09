
<span data-ttu-id="8f853-101">如需有關磁碟的詳細資訊，請參閱[關於虛擬機器的磁碟和 VHD](../articles/virtual-machines/linux/about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="8f853-101">For more information about disks, see [About Disks and VHDs for Virtual Machines](../articles/virtual-machines/linux/about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<a id="attachempty"></a>

## <a name="attach-an-empty-disk"></a><span data-ttu-id="8f853-102">連接空的磁碟</span><span class="sxs-lookup"><span data-stu-id="8f853-102">Attach an empty disk</span></span>
1. <span data-ttu-id="8f853-103">開啟 Azure CLI 1.0 和[連接 tooyour Azure 訂用帳戶](../articles/xplat-cli-connect.md)。</span><span class="sxs-lookup"><span data-stu-id="8f853-103">Open Azure CLI 1.0 and [connect tooyour Azure subscription](../articles/xplat-cli-connect.md).</span></span> <span data-ttu-id="8f853-104">確定處於 Azure 服務管理模式 (`azure config mode asm`)。</span><span class="sxs-lookup"><span data-stu-id="8f853-104">Make sure you are in Azure Service Management mode (`azure config mode asm`).</span></span>
2. <span data-ttu-id="8f853-105">輸入`azure vm disk attach-new`toocreate 並附加新的磁碟，hello 下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="8f853-105">Enter `azure vm disk attach-new` toocreate and attach a new disk as shown in hello following example.</span></span> <span data-ttu-id="8f853-106">取代*myVM* hello 同名的 Linux 虛擬機器，並指定 hello hello 磁碟大小以 gb 為單位是*100 GB*在此範例中：</span><span class="sxs-lookup"><span data-stu-id="8f853-106">Replace *myVM* with hello name of your Linux Virtual Machine and specify hello size of hello disk in GB, which is *100GB* in this example:</span></span>

    ```azurecli
    azure vm disk attach-new myVM 100
    ```

3. <span data-ttu-id="8f853-107">Hello 資料磁碟會建立並附加之後，它會列在 hello 輸出`azure vm disk list <virtual-machine-name>`hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="8f853-107">After hello data disk is created and attached, it's listed in hello output of `azure vm disk list <virtual-machine-name>` as shown in hello following example:</span></span>
   
    ```azurecli
    azure vm disk list TestVM
    ```

    <span data-ttu-id="8f853-108">hello 輸出是 toohello 類似下列範例程式碼：</span><span class="sxs-lookup"><span data-stu-id="8f853-108">hello output is similar toohello following example:</span></span>

    ```bash
    info:    Executing command vm disk list
   
   * Fetching disk images
   * Getting virtual machines
   * Getting VM disks
     data:    Lun  Size(GB)  Blob-Name                         OS
     data:    ---  --------  --------------------------------  -----
     data:         30        myVM-2645b8030676c8f8.vhd  Linux
     data:    0    100       myVM-76f7ee1ef0f6dddc.vhd
     info:    vm disk list command OK
    ```

<a id="attachexisting"></a>

## <a name="attach-an-existing-disk"></a><span data-ttu-id="8f853-109">連接現有磁碟</span><span class="sxs-lookup"><span data-stu-id="8f853-109">Attach an existing disk</span></span>
<span data-ttu-id="8f853-110">連接現有磁碟要求您在儲存體帳戶中需要有可用的 .vhd。</span><span class="sxs-lookup"><span data-stu-id="8f853-110">Attaching an existing disk requires that you have a .vhd available in a storage account.</span></span>

1. <span data-ttu-id="8f853-111">開啟 Azure CLI 1.0 和[連接 tooyour Azure 訂用帳戶](../articles/xplat-cli-connect.md)。</span><span class="sxs-lookup"><span data-stu-id="8f853-111">Open Azure CLI 1.0 and [connect tooyour Azure subscription](../articles/xplat-cli-connect.md).</span></span> <span data-ttu-id="8f853-112">確定處於 Azure 服務管理模式 (`azure config mode asm`)。</span><span class="sxs-lookup"><span data-stu-id="8f853-112">Make sure you are in Azure Service Management mode (`azure config mode asm`).</span></span>
2. <span data-ttu-id="8f853-113">檢查是否 hello tooattach 已經是您想要的 VHD 上傳 tooyour Azure 訂用帳戶：</span><span class="sxs-lookup"><span data-stu-id="8f853-113">Check if hello VHD you want tooattach is already uploaded tooyour Azure subscription:</span></span>
   
    ```azurecli
    azure vm disk list
    ```

    <span data-ttu-id="8f853-114">hello 輸出是 toohello 類似下列範例程式碼：</span><span class="sxs-lookup"><span data-stu-id="8f853-114">hello output is similar toohello following example:</span></span>

    ```azurecli
     info:    Executing command vm disk list
   
   * Fetching disk images
     data:    Name                                          OS
     data:    --------------------------------------------  -----
     data:    myTestVhd                                     Linux
     data:    TestVM-ubuntuVMasm-0-201508060029150744  Linux
     data:    TestVM-ubuntuVMasm-0-201508060040530369
     info:    vm disk list command OK
    ```

3. <span data-ttu-id="8f853-115">如果找不到 hello 磁碟 toouse，可能會使用上傳本機的 VHD tooyour 訂用帳戶`azure vm disk create`或`azure vm disk upload`。</span><span class="sxs-lookup"><span data-stu-id="8f853-115">If you don't find hello disk that you want toouse, you may upload a local VHD tooyour subscription by using `azure vm disk create` or `azure vm disk upload`.</span></span> <span data-ttu-id="8f853-116">舉例來說，`disk create`會如 hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="8f853-116">An example of `disk create` would be as in hello following example:</span></span>
   
    ```azurecli
    azure vm disk create myVhd .\TempDisk\test.VHD -l "East US" -o Linux
    ```

    <span data-ttu-id="8f853-117">hello 輸出是 toohello 類似下列範例程式碼：</span><span class="sxs-lookup"><span data-stu-id="8f853-117">hello output is similar toohello following example:</span></span>

    ```azurecli
    info:    Executing command vm disk create
    + Retrieving storage accounts
    info:    VHD size : 10 GB
    info:    Uploading 10485760.5 KB
    Requested:100.0% Completed:100.0% Running:   0 Time:   25s Speed:    82 KB/s
    info:    Finishing computing MD5 hash, 16% is complete.
    info:    https://mystorageaccount.blob.core.windows.net/disks/myVHD.vhd was
    uploaded successfully
    info:    vm disk create command OK
    ```
   
   <span data-ttu-id="8f853-118">您也可以使用`azure vm disk upload`tooupload VHD tooa 特定儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="8f853-118">You may also use `azure vm disk upload` tooupload a VHD tooa specific storage account.</span></span> <span data-ttu-id="8f853-119">閱讀有關 hello 命令 toomanage 您 Azure 虛擬機器的資料磁碟[在這裡](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)。</span><span class="sxs-lookup"><span data-stu-id="8f853-119">Read more about hello commands toomanage your Azure virtual machine data disks [over here](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span>

4. <span data-ttu-id="8f853-120">現在您附加 hello 預期 VHD tooyour 虛擬機器：</span><span class="sxs-lookup"><span data-stu-id="8f853-120">Now you attach hello desired VHD tooyour virtual machine:</span></span>
   
    ```azurecli
    azure vm disk attach myVM myVhd
    ```
   
   <span data-ttu-id="8f853-121">請確定 tooreplace *myVM* hello 名稱，為您的虛擬機器和*myVHD*與您想要的 VHD。</span><span class="sxs-lookup"><span data-stu-id="8f853-121">Make sure tooreplace *myVM* with hello name of your virtual machine, and *myVHD* with your desired VHD.</span></span>

5. <span data-ttu-id="8f853-122">您可以確認 hello 磁碟是虛擬機器附加的 toohello `azure vm disk list <virtual-machine-name>`:</span><span class="sxs-lookup"><span data-stu-id="8f853-122">You can verify hello disk is attached toohello virtual machine with `azure vm disk list <virtual-machine-name>`:</span></span>
   
    ```azurecli
    azure vm disk list myVM
    ```

    <span data-ttu-id="8f853-123">hello 輸出是 toohello 類似下列範例程式碼：</span><span class="sxs-lookup"><span data-stu-id="8f853-123">hello output is similar toohello following example:</span></span>

    ```azurecli
     info:    Executing command vm disk list
   
   * Fetching disk images
   * Getting virtual machines
   * Getting VM disks
     data:    Lun  Size(GB)  Blob-Name                         OS
     data:    ---  --------  --------------------------------  -----
     data:         30        TestVM-2645b8030676c8f8.vhd  Linux
     data:    1    10        test.VHD
     data:    0    100        TestVM-76f7ee1ef0f6dddc.vhd
     info:    vm disk list command OK
    ```

> [!NOTE]
> <span data-ttu-id="8f853-124">新增資料磁碟之後，您將需要 toolog toohello 虛擬機器上的，並因此 hello 虛擬機器可以使用 hello 磁碟儲存體初始化 hello 磁碟 （請參閱下列 hello 步驟的詳細資訊 toodo 如何初始化 hello 磁碟上）。</span><span class="sxs-lookup"><span data-stu-id="8f853-124">After you add a data disk, you'll need toolog on toohello virtual machine and initialize hello disk so hello virtual machine can use hello disk for storage (see hello following steps for more information on how toodo initialize hello disk).</span></span>
> 
> 

