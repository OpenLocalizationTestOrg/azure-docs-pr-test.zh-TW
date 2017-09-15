<span data-ttu-id="c5ac8-101">Azure 現在提供兩個偵錯功能的支援︰Azure 虛擬機器 Resource Manager 部署模型的主控台輸出和螢幕擷取畫面支援。</span><span class="sxs-lookup"><span data-stu-id="c5ac8-101">Support for two debugging features is now available in Azure: Console Output and Screenshot support for Azure Virtual Machines Resource Manager deployment model.</span></span> 

<span data-ttu-id="c5ac8-102">將自己的映像送至 Azure 或甚至啟動其中一個平台映像時，虛擬機器進入不可開機狀態的原因有很多。</span><span class="sxs-lookup"><span data-stu-id="c5ac8-102">When bringing your own image to Azure or even booting one of the platform images, there can be many reasons why a Virtual Machine gets into a non-bootable state.</span></span> <span data-ttu-id="c5ac8-103">這些功能可讓您輕鬆地診斷及復原開機失敗的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="c5ac8-103">These features enable you to easily diagnose and recover your Virtual Machines from boot failures.</span></span>

<span data-ttu-id="c5ac8-104">若為 Linux 虛擬機器，您可以從入口網站輕鬆地檢視主控台記錄的輸出︰</span><span class="sxs-lookup"><span data-stu-id="c5ac8-104">For Linux Virtual Machines, you can easily view the output of your console log from the Portal:</span></span>

![Azure 入口網站](./media/virtual-machines-common-boot-diagnostics/screenshot1.png)
 
<span data-ttu-id="c5ac8-106">不過，若為 Windows 和 Linux 虛擬機器，Azure 也可讓您從 Hypervisor 查看 VM 的螢幕擷取畫面︰</span><span class="sxs-lookup"><span data-stu-id="c5ac8-106">However, for both Windows and Linux Virtual Machines, Azure also enables you to see a screenshot of the VM from the hypervisor:</span></span>

![錯誤](./media/virtual-machines-common-boot-diagnostics/screenshot2.png)

<span data-ttu-id="c5ac8-108">所有區域中的 Azure 虛擬機器都支援這兩項功能。</span><span class="sxs-lookup"><span data-stu-id="c5ac8-108">Both of these features are supported for Azure Virtual Machines in all regions.</span></span> <span data-ttu-id="c5ac8-109">請注意，螢幕擷取畫面和輸出最多可能需要 10 分鐘的時間才會出現在您的儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="c5ac8-109">Note, screenshots, and output can take up to 10 minutes to appear in your storage account.</span></span>

## <a name="common-boot-errors"></a><span data-ttu-id="c5ac8-110">常見的開機錯誤</span><span class="sxs-lookup"><span data-stu-id="c5ac8-110">Common boot errors</span></span>

- [<span data-ttu-id="c5ac8-111">0xC000000E</span><span class="sxs-lookup"><span data-stu-id="c5ac8-111">0xC000000E</span></span>](https://support.microsoft.com/help/4010129)
- [<span data-ttu-id="c5ac8-112">0xC000000F</span><span class="sxs-lookup"><span data-stu-id="c5ac8-112">0xC000000F</span></span>](https://support.microsoft.com/help/4010130)
- [<span data-ttu-id="c5ac8-113">0xC0000011</span><span class="sxs-lookup"><span data-stu-id="c5ac8-113">0xC0000011</span></span>](https://support.microsoft.com/help/4010134)
- [<span data-ttu-id="c5ac8-114">0xC0000034</span><span class="sxs-lookup"><span data-stu-id="c5ac8-114">0xC0000034</span></span>](https://support.microsoft.com/help/4010140)
- [<span data-ttu-id="c5ac8-115">0xC0000098</span><span class="sxs-lookup"><span data-stu-id="c5ac8-115">0xC0000098</span></span>](https://support.microsoft.com/help/4010137)
- [<span data-ttu-id="c5ac8-116">0xC00000BA</span><span class="sxs-lookup"><span data-stu-id="c5ac8-116">0xC00000BA</span></span>](https://support.microsoft.com/help/4010136)
- [<span data-ttu-id="c5ac8-117">0xC000014C</span><span class="sxs-lookup"><span data-stu-id="c5ac8-117">0xC000014C</span></span>](https://support.microsoft.com/help/4010141)
- [<span data-ttu-id="c5ac8-118">0xC0000221</span><span class="sxs-lookup"><span data-stu-id="c5ac8-118">0xC0000221</span></span>](https://support.microsoft.com/help/4010132)
- [<span data-ttu-id="c5ac8-119">0xC0000225</span><span class="sxs-lookup"><span data-stu-id="c5ac8-119">0xC0000225</span></span>](https://support.microsoft.com/help/4010138)
- [<span data-ttu-id="c5ac8-120">0xC0000359</span><span class="sxs-lookup"><span data-stu-id="c5ac8-120">0xC0000359</span></span>](https://support.microsoft.com/help/4010135)
- [<span data-ttu-id="c5ac8-121">0xC0000605</span><span class="sxs-lookup"><span data-stu-id="c5ac8-121">0xC0000605</span></span>](https://support.microsoft.com/help/4010131)
- [<span data-ttu-id="c5ac8-122">找不到作業系統</span><span class="sxs-lookup"><span data-stu-id="c5ac8-122">An operating system wasn't found</span></span>](https://support.microsoft.com/help/4010142)
- [<span data-ttu-id="c5ac8-123">開機失敗或 INACCESSIBLE_BOOT_DEVICE</span><span class="sxs-lookup"><span data-stu-id="c5ac8-123">Boot failure or INACCESSIBLE_BOOT_DEVICE</span></span>](https://support.microsoft.com/help/4010143)

## <a name="enable-diagnostics-on-a-new-virtual-machine"></a><span data-ttu-id="c5ac8-124">在新的虛擬機器上啟用診斷</span><span class="sxs-lookup"><span data-stu-id="c5ac8-124">Enable diagnostics on a new virtual machine</span></span>
1. <span data-ttu-id="c5ac8-125">從預覽入口網站建立新的虛擬機器時，從部署模型下拉式清單中選取 [Azure Resource Manager]︰</span><span class="sxs-lookup"><span data-stu-id="c5ac8-125">When creating a new Virtual Machine from the Preview Portal, select the **Azure Resource Manager** from the deployment model dropdown:</span></span>
 
    ![資源管理員](./media/virtual-machines-common-boot-diagnostics/screenshot3.jpg)

2. <span data-ttu-id="c5ac8-127">設定 [監視] 選項來選取您想要放置這些診斷檔案的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="c5ac8-127">Configure the Monitoring option to select the storage account where you would like to place these diagnostic files.</span></span>
 
    ![建立 VM](./media/virtual-machines-common-boot-diagnostics/screenshot4.jpg)

3. <span data-ttu-id="c5ac8-129">如果您正從 Azure Resource Manager 範本進行部署，請瀏覽至您的虛擬機器的資源並附加診斷設定檔區段。</span><span class="sxs-lookup"><span data-stu-id="c5ac8-129">If you are deploying from an Azure Resource Manager template, navigate to your Virtual Machine resource and append the diagnostics profile section.</span></span> <span data-ttu-id="c5ac8-130">請記得使用 “2015-06-15” API 版本標頭。</span><span class="sxs-lookup"><span data-stu-id="c5ac8-130">Remember to use the “2015-06-15” API version header.</span></span>

    ```json
    {
          "apiVersion": "2015-06-15",
          "type": "Microsoft.Compute/virtualMachines",
          … 
    ```

4. <span data-ttu-id="c5ac8-131">診斷設定檔可讓您選取想要放置這些記錄的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="c5ac8-131">The diagnostics profile enables you to select the storage account where you want to put these logs.</span></span>

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

<span data-ttu-id="c5ac8-132">若要在已啟用開機診斷的情況下部署範例虛擬機器，請在此查看我們的存放庫。</span><span class="sxs-lookup"><span data-stu-id="c5ac8-132">To deploy a sample Virtual Machine with boot diagnostics enabled, check out our repo here.</span></span>

## <a name="update-an-existing-virtual-machine"></a><span data-ttu-id="c5ac8-133">更新現有的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="c5ac8-133">Update an existing virtual machine</span></span> ##

<span data-ttu-id="c5ac8-134">若要透過入口網站啟用開機診斷，您也可以透過入口網站更新現有的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="c5ac8-134">To enable boot diagnostics through the Portal, you can also update an existing Virtual Machine through the Portal.</span></span> <span data-ttu-id="c5ac8-135">選取 [開機診斷] 選項和 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="c5ac8-135">Select the Boot Diagnostics option and Save.</span></span> <span data-ttu-id="c5ac8-136">重新啟動 VM 才會生效。</span><span class="sxs-lookup"><span data-stu-id="c5ac8-136">Restart the VM to take effect.</span></span>

![更新現有的 VM](./media/virtual-machines-common-boot-diagnostics/screenshot5.png)

