


<span data-ttu-id="03a5f-101">可用性設定組可協助您的虛擬機器在停機期間 (例如維護期間) 仍然保持可用狀態。</span><span class="sxs-lookup"><span data-stu-id="03a5f-101">An availability set helps keep your virtual machines available during downtime, such as during maintenance.</span></span> <span data-ttu-id="03a5f-102">在可用性設定組中置入二或多個類似設定的虛擬機器，將可針對虛擬機器所執行的應用程式或服務，建立維護其可用性所需的備援。</span><span class="sxs-lookup"><span data-stu-id="03a5f-102">Placing two or more similarly configured virtual machines in an availability set creates the redundancy needed to maintain availability of the applications or services that your virtual machine runs.</span></span> <span data-ttu-id="03a5f-103">如需其運作方式的詳細資訊，請參閱[管理虛擬機器的可用性][Manage the availability of virtual machines]。</span><span class="sxs-lookup"><span data-stu-id="03a5f-103">For details about how this works, see [Manage the availability of virtual machines][Manage the availability of virtual machines].</span></span>

<span data-ttu-id="03a5f-104">同時使用可用性設定組和負載平衡端點，是協助確保您的應用程式一直可用並有效率執行的最佳做法。</span><span class="sxs-lookup"><span data-stu-id="03a5f-104">It's a best practice to use both availability sets and load-balancing endpoints to help ensure that your application is always available and running efficiently.</span></span> <span data-ttu-id="03a5f-105">如需負載平衡端點的詳細資訊，請參閱 [Azure 基礎結構服務的負載平衡][Load balancing for Azure infrastructure services]。</span><span class="sxs-lookup"><span data-stu-id="03a5f-105">For details about load-balanced endpoints, see [Load balancing for Azure infrastructure services][Load balancing for Azure infrastructure services].</span></span>

<span data-ttu-id="03a5f-106">您可以使用下列兩個選項的其中之一，將傳統虛擬機器加入可用性設定組：</span><span class="sxs-lookup"><span data-stu-id="03a5f-106">You can add classic virtual machines into an availability set by using one of two options:</span></span>

* <span data-ttu-id="03a5f-107">[選項 1︰同時建立虛擬機器和可用性設定組][Option 1: Create a virtual machine and an availability set at the same time]。</span><span class="sxs-lookup"><span data-stu-id="03a5f-107">[Option 1: Create a virtual machine and an availability set at the same time][Option 1: Create a virtual machine and an availability set at the same time].</span></span> <span data-ttu-id="03a5f-108">然後，將新的虛擬機器加入您在建立這些虛擬機器時的設定組。</span><span class="sxs-lookup"><span data-stu-id="03a5f-108">Then, add new virtual machines to the set when you create those virtual machines.</span></span>
* <span data-ttu-id="03a5f-109">[選項 2︰將現有的虛擬機器新增至可用性設定組][Option 2: Add an existing virtual machine to an availability set]。</span><span class="sxs-lookup"><span data-stu-id="03a5f-109">[Option 2: Add an existing virtual machine to an availability set][Option 2: Add an existing virtual machine to an availability set].</span></span>

> [!NOTE]
> <span data-ttu-id="03a5f-110">在傳統模型中，您要放入相同可用性設定組的虛擬機器必須隸屬於相同的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="03a5f-110">In the classic model, virtual machines that you want to put in the same availability set must belong to the same cloud service.</span></span>
> 
> 

## <span data-ttu-id="03a5f-111"><a id="createset"> </a>選項 1︰同時建立虛擬機器和可用性設定組</span><span class="sxs-lookup"><span data-stu-id="03a5f-111"><a id="createset"> </a>Option 1: Create a virtual machine and an availability set at the same time</span></span>
<span data-ttu-id="03a5f-112">您可以使用 Azure 入口網站或 Azure PowerShell 命令來執行此作業。</span><span class="sxs-lookup"><span data-stu-id="03a5f-112">You can use either the Azure portal or Azure PowerShell commands to do this.</span></span>

<span data-ttu-id="03a5f-113">使用 Azure 入口網站：</span><span class="sxs-lookup"><span data-stu-id="03a5f-113">To use the Azure portal:</span></span>

1. <span data-ttu-id="03a5f-114">如果您尚未登入 [Azure 入口網站](https://portal.azure.com)，請先登入。</span><span class="sxs-lookup"><span data-stu-id="03a5f-114">If you haven't already done so, sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="03a5f-115">在 [中樞] 功能表上按一下 [+新增]，然後按一下 [虛擬機器]。</span><span class="sxs-lookup"><span data-stu-id="03a5f-115">On the hub menu, click **+ New**, and then click **Virtual Machine**.</span></span>
   
    ![替代映像文字](./media/virtual-machines-common-classic-configure-availability/ChooseVMImage.png)
3. <span data-ttu-id="03a5f-117">選取您想要使用的 Marketplace 虛擬機器映像。</span><span class="sxs-lookup"><span data-stu-id="03a5f-117">Select the Marketplace virtual machine image you wish to use.</span></span> <span data-ttu-id="03a5f-118">您可以選擇建立 Linux 或 Windows 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="03a5f-118">You can choose to create a Linux or Windows virtual machine.</span></span>
4. <span data-ttu-id="03a5f-119">確認所選虛擬機器的部署模型設為 [傳統]，然後按一下 [建立]</span><span class="sxs-lookup"><span data-stu-id="03a5f-119">For the selected virtual machine, verify that the deployment model is set to **Classic** and then click **Create**</span></span>
   
    ![替代映像文字](./media/virtual-machines-common-classic-configure-availability/ChooseClassicModel.png)
5. <span data-ttu-id="03a5f-121">輸入虛擬機器名稱、使用者名稱和密碼 (Windows 機器) 或 SSH 公開金鑰 (Linux 機器)。</span><span class="sxs-lookup"><span data-stu-id="03a5f-121">Enter a virtual machine name, user name and password (for Windows machines) or SSH public key (for Linux machines).</span></span> 
6. <span data-ttu-id="03a5f-122">選擇 VM 大小，然後按一下 [選取]  以繼續。</span><span class="sxs-lookup"><span data-stu-id="03a5f-122">Choose the VM size and then click **Select** to continue.</span></span>
7. <span data-ttu-id="03a5f-123">選擇 [選擇性組態] > [可用性設定組]，並選取您想要加入虛擬機器的可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="03a5f-123">Choose **Optional Configuration > Availability set**, and select the availability set you wish to add the virtual machine to.</span></span>
   
    ![替代映像文字](./media/virtual-machines-common-classic-configure-availability/ChooseAvailabilitySet.png) 
8. <span data-ttu-id="03a5f-125">檢閱組態設定。</span><span class="sxs-lookup"><span data-stu-id="03a5f-125">Review your configuration settings.</span></span> <span data-ttu-id="03a5f-126">完成之後，請按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="03a5f-126">When you're done, click **Create**.</span></span>
9. <span data-ttu-id="03a5f-127">當 Azure 建立虛擬機器時，您可以在 [中樞] 功能表的 [虛擬機器]  下追蹤進度。</span><span class="sxs-lookup"><span data-stu-id="03a5f-127">While Azure creates your virtual machine, you can track the progress under **Virtual Machines** in the hub menu.</span></span>

<span data-ttu-id="03a5f-128">若要使用 Azure PowerShell 命令建立 Azure 虛擬機器，並將它新增至新的或現有的可用性設定組，請參閱[使用 Azure PowerShell 建立和預先設定以 Windows 為基礎的虛擬機器](../articles/virtual-machines/windows/classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="03a5f-128">To use Azure PowerShell commands to create an Azure virtual machine and add it to a new or existing availability set, see [Use Azure PowerShell to create and preconfigure Windows-based virtual machines](../articles/virtual-machines/windows/classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span></span>

## <span data-ttu-id="03a5f-129"><a id="addmachine"> </a>選項 2︰將現有的虛擬機器新增至可用性設定組</span><span class="sxs-lookup"><span data-stu-id="03a5f-129"><a id="addmachine"> </a>Option 2: Add an existing virtual machine to an availability set</span></span>
<span data-ttu-id="03a5f-130">在 Azure 入口網站中，您可以將現有的傳統虛擬機器新增至現有的可用性設定組，或為其建立一個新的可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="03a5f-130">In the Azure portal, you can add existing classic virtual machines to an existing availability set or create a new one for them.</span></span> <span data-ttu-id="03a5f-131">(請注意，相同可用性設定組中的虛擬機器必須隸屬於相同的雲端服務。)步驟幾乎完全相同。</span><span class="sxs-lookup"><span data-stu-id="03a5f-131">(Keep in mind that the virtual machines in the same availability set must belong to the same cloud service.) The steps are almost the same.</span></span> <span data-ttu-id="03a5f-132">有了 Azure PowerShell，您可以將虛擬機器加入現有的可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="03a5f-132">With Azure PowerShell, you can add the virtual machine to an existing availability set.</span></span>

1. <span data-ttu-id="03a5f-133">如果您尚未登入 [Azure 入口網站](https://portal.azure.com)，請先登入。</span><span class="sxs-lookup"><span data-stu-id="03a5f-133">If you have not already done so, sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="03a5f-134">在 [中樞] 功能表上，按一下 [虛擬機器 (傳統)] 。</span><span class="sxs-lookup"><span data-stu-id="03a5f-134">On the Hub menu, click **Virtual Machines (classic)**.</span></span>
   
    ![替代映像文字](./media/virtual-machines-common-classic-configure-availability/ChooseClassicVM.png)
3. <span data-ttu-id="03a5f-136">從虛擬機器的清單中，選取您想要加入至集合的虛擬機器名稱。</span><span class="sxs-lookup"><span data-stu-id="03a5f-136">From the list of virtual machines, select the name of the virtual machine that you want to add to the set.</span></span>
4. <span data-ttu-id="03a5f-137">從虛擬機器的 [設定] 中選擇 [可用性設定組]。</span><span class="sxs-lookup"><span data-stu-id="03a5f-137">Choose **Availability set** from the virtual machine **Settings**.</span></span>
   
    ![替代映像文字](./media/virtual-machines-common-classic-configure-availability/AvailabilitySetSettings.png)
5. <span data-ttu-id="03a5f-139">選取您想要加入虛擬機器的可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="03a5f-139">Select the availability set you wish to add the virtual machine to.</span></span> <span data-ttu-id="03a5f-140">虛擬機器必須和可用性設定組隸屬於相同的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="03a5f-140">The virtual machine must belong to the same cloud service as the availability set.</span></span>
   
    ![替代映像文字](./media/virtual-machines-common-classic-configure-availability/AvailabilitySetPicker.png)
6. <span data-ttu-id="03a5f-142">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="03a5f-142">Click **Save**.</span></span>

<span data-ttu-id="03a5f-143">若要使用 Azure PowerShell 命令，請開啟系統管理員層級的 Azure PowerShell 工作階段並執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="03a5f-143">To use Azure PowerShell commands, open an administrator-level Azure PowerShell session and run the following command.</span></span> <span data-ttu-id="03a5f-144">在預留位置 (例如 &lt;VmCloudServiceName&gt;) 中，以正確的名稱取代括號中的所有內容，包括 < and > 字元。</span><span class="sxs-lookup"><span data-stu-id="03a5f-144">For the placeholders (such as &lt;VmCloudServiceName&gt;), replace everything within the quotes, including the < and > characters, with the correct names.</span></span>

    Get-AzureVM -ServiceName "<VmCloudServiceName>" -Name "<VmName>" | Set-AzureAvailabilitySet -AvailabilitySetName "<AvSetName>" | Update-AzureVM

> [!NOTE]
> <span data-ttu-id="03a5f-145">系統可能必須重新啟動虛擬機器，以結束將它加入至可用性集合的作業。</span><span class="sxs-lookup"><span data-stu-id="03a5f-145">The virtual machine might have to be restarted to finish adding it to the availability set.</span></span>
> 
> 

<!-- LINKS -->
[Option 1: Create a virtual machine and an availability set at the same time]: #createset
[Option 2: Add an existing virtual machine to an availability set]: #addmachine

[Load balancing for Azure infrastructure services]: ../articles/virtual-machines/virtual-machines-linux-load-balance.md
[Manage the availability of virtual machines]:../articles/virtual-machines/linux/manage-availability.md

[Create a virtual machine running Windows]: ../articles/virtual-machines/virtual-machines-windows-hero-tutorial.md
[Virtual Network overview]: ../articles/virtual-network/virtual-networks-overview.md

