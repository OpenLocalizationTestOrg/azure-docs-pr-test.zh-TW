<span data-ttu-id="443be-101">Azure 現在提供兩個偵錯功能的支援︰Azure 虛擬機器 Resource Manager 部署模型的主控台輸出和螢幕擷取畫面支援。</span><span class="sxs-lookup"><span data-stu-id="443be-101">Support for two debugging features is now available in Azure: Console Output and Screenshot support for Azure Virtual Machines Resource Manager deployment model.</span></span> 

<span data-ttu-id="443be-102">時攜帶您自己的映像 tooAzure 或甚至開機的 hello 平台映像，可能會因許多原因而虛擬機器進入非可開機的狀態。</span><span class="sxs-lookup"><span data-stu-id="443be-102">When bringing your own image tooAzure or even booting one of hello platform images, there can be many reasons why a Virtual Machine gets into a non-bootable state.</span></span> <span data-ttu-id="443be-103">這些功能可讓您 tooeasily 診斷和復原虛擬機器的開機失敗。</span><span class="sxs-lookup"><span data-stu-id="443be-103">These features enable you tooeasily diagnose and recover your Virtual Machines from boot failures.</span></span>

<span data-ttu-id="443be-104">適用於 Linux 虛擬機器中，您可以輕鬆地檢視 hello 輸出的主控台記錄檔，從 hello 入口網站：</span><span class="sxs-lookup"><span data-stu-id="443be-104">For Linux Virtual Machines, you can easily view hello output of your console log from hello Portal:</span></span>

![Azure 入口網站](./media/virtual-machines-common-boot-diagnostics/screenshot1.png)
 
<span data-ttu-id="443be-106">不過，針對 Windows 和 Linux 虛擬機器，Azure 也可讓您 toosee hello VM 從 hello hypervisor 的螢幕擷取畫面：</span><span class="sxs-lookup"><span data-stu-id="443be-106">However, for both Windows and Linux Virtual Machines, Azure also enables you toosee a screenshot of hello VM from hello hypervisor:</span></span>

![錯誤](./media/virtual-machines-common-boot-diagnostics/screenshot2.png)

<span data-ttu-id="443be-108">所有區域中的 Azure 虛擬機器都支援這兩項功能。</span><span class="sxs-lookup"><span data-stu-id="443be-108">Both of these features are supported for Azure Virtual Machines in all regions.</span></span> <span data-ttu-id="443be-109">請注意，螢幕擷取畫面，輸出可能會佔用 too10 分鐘 tooappear 儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="443be-109">Note, screenshots, and output can take up too10 minutes tooappear in your storage account.</span></span>

## <a name="common-boot-errors"></a><span data-ttu-id="443be-110">常見的開機錯誤</span><span class="sxs-lookup"><span data-stu-id="443be-110">Common boot errors</span></span>

- [<span data-ttu-id="443be-111">0xC000000E</span><span class="sxs-lookup"><span data-stu-id="443be-111">0xC000000E</span></span>](https://support.microsoft.com/help/4010129)
- [<span data-ttu-id="443be-112">0xC000000F</span><span class="sxs-lookup"><span data-stu-id="443be-112">0xC000000F</span></span>](https://support.microsoft.com/help/4010130)
- [<span data-ttu-id="443be-113">0xC0000011</span><span class="sxs-lookup"><span data-stu-id="443be-113">0xC0000011</span></span>](https://support.microsoft.com/help/4010134)
- [<span data-ttu-id="443be-114">0xC0000034</span><span class="sxs-lookup"><span data-stu-id="443be-114">0xC0000034</span></span>](https://support.microsoft.com/help/4010140)
- [<span data-ttu-id="443be-115">0xC0000098</span><span class="sxs-lookup"><span data-stu-id="443be-115">0xC0000098</span></span>](https://support.microsoft.com/help/4010137)
- [<span data-ttu-id="443be-116">0xC00000BA</span><span class="sxs-lookup"><span data-stu-id="443be-116">0xC00000BA</span></span>](https://support.microsoft.com/help/4010136)
- [<span data-ttu-id="443be-117">0xC000014C</span><span class="sxs-lookup"><span data-stu-id="443be-117">0xC000014C</span></span>](https://support.microsoft.com/help/4010141)
- [<span data-ttu-id="443be-118">0xC0000221</span><span class="sxs-lookup"><span data-stu-id="443be-118">0xC0000221</span></span>](https://support.microsoft.com/help/4010132)
- [<span data-ttu-id="443be-119">0xC0000225</span><span class="sxs-lookup"><span data-stu-id="443be-119">0xC0000225</span></span>](https://support.microsoft.com/help/4010138)
- [<span data-ttu-id="443be-120">0xC0000359</span><span class="sxs-lookup"><span data-stu-id="443be-120">0xC0000359</span></span>](https://support.microsoft.com/help/4010135)
- [<span data-ttu-id="443be-121">0xC0000605</span><span class="sxs-lookup"><span data-stu-id="443be-121">0xC0000605</span></span>](https://support.microsoft.com/help/4010131)
- [<span data-ttu-id="443be-122">找不到作業系統</span><span class="sxs-lookup"><span data-stu-id="443be-122">An operating system wasn't found</span></span>](https://support.microsoft.com/help/4010142)
- [<span data-ttu-id="443be-123">開機失敗或 INACCESSIBLE_BOOT_DEVICE</span><span class="sxs-lookup"><span data-stu-id="443be-123">Boot failure or INACCESSIBLE_BOOT_DEVICE</span></span>](https://support.microsoft.com/help/4010143)

## <a name="enable-diagnostics-on-a-new-virtual-machine"></a><span data-ttu-id="443be-124">在新的虛擬機器上啟用診斷</span><span class="sxs-lookup"><span data-stu-id="443be-124">Enable diagnostics on a new virtual machine</span></span>
1. <span data-ttu-id="443be-125">當從 hello 預覽入口網站中建立新的虛擬機器，選取 hello **Azure Resource Manager**從 hello 部署模型 下拉式清單：</span><span class="sxs-lookup"><span data-stu-id="443be-125">When creating a new Virtual Machine from hello Preview Portal, select hello **Azure Resource Manager** from hello deployment model dropdown:</span></span>
 
    ![Resource Manager](./media/virtual-machines-common-boot-diagnostics/screenshot3.jpg)

2. <span data-ttu-id="443be-127">這些診斷檔案設定 hello 監視選項 tooselect hello 儲存體帳戶 tooplace 的位置。</span><span class="sxs-lookup"><span data-stu-id="443be-127">Configure hello Monitoring option tooselect hello storage account where you would like tooplace these diagnostic files.</span></span>
 
    ![建立 VM](./media/virtual-machines-common-boot-diagnostics/screenshot4.jpg)

3. <span data-ttu-id="443be-129">如果您要部署的 Azure 資源管理員範本，請瀏覽 tooyour 虛擬機器的資源，並附加 hello 診斷設定檔區段。</span><span class="sxs-lookup"><span data-stu-id="443be-129">If you are deploying from an Azure Resource Manager template, navigate tooyour Virtual Machine resource and append hello diagnostics profile section.</span></span> <span data-ttu-id="443be-130">請記住 toouse hello"2015年-06-15"應用程式開發介面版本標頭。</span><span class="sxs-lookup"><span data-stu-id="443be-130">Remember toouse hello “2015-06-15” API version header.</span></span>

    ```json
    {
          "apiVersion": "2015-06-15",
          "type": "Microsoft.Compute/virtualMachines",
          … 
    ```

4. <span data-ttu-id="443be-131">hello 診斷設定檔可讓您 tooselect hello 儲存體帳戶，而您希望 tooput 這些記錄檔。</span><span class="sxs-lookup"><span data-stu-id="443be-131">hello diagnostics profile enables you tooselect hello storage account where you want tooput these logs.</span></span>

    ```json
            "diagnosticsProfile": {
                "bootDiagnostics": {
                "enabled": true,
                "storageUri": "[concat('http://', parameters('newStorageAccountName'), '.blob.core.windows.net')]"
                }
            }
            }
        }
    ```

<span data-ttu-id="443be-132">toodeploy 含開機診斷功能，簽出我們儲存機制，在此範例的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="443be-132">toodeploy a sample Virtual Machine with boot diagnostics enabled, check out our repo here.</span></span>

## <a name="update-an-existing-virtual-machine"></a><span data-ttu-id="443be-133">更新現有的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="443be-133">Update an existing virtual machine</span></span> ##

<span data-ttu-id="443be-134">tooenable 開機診斷，透過 hello 入口網站，您也可以更新現有的虛擬機器透過 hello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="443be-134">tooenable boot diagnostics through hello Portal, you can also update an existing Virtual Machine through hello Portal.</span></span> <span data-ttu-id="443be-135">選取 hello 開機診斷選項，並儲存。</span><span class="sxs-lookup"><span data-stu-id="443be-135">Select hello Boot Diagnostics option and Save.</span></span> <span data-ttu-id="443be-136">重新啟動 hello VM tootake 效果。</span><span class="sxs-lookup"><span data-stu-id="443be-136">Restart hello VM tootake effect.</span></span>

![更新現有的 VM](./media/virtual-machines-common-boot-diagnostics/screenshot5.png)

