


<span data-ttu-id="8be22-101">可用性設定組可協助您的虛擬機器在停機期間 (例如維護期間) 仍然保持可用狀態。</span><span class="sxs-lookup"><span data-stu-id="8be22-101">An availability set helps keep your virtual machines available during downtime, such as during maintenance.</span></span> <span data-ttu-id="8be22-102">將兩個以上類似設定的虛擬機器放置於可用性集合建立 hello 需要備援 toomaintain 可用性 hello 應用程式或服務執行您的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="8be22-102">Placing two or more similarly configured virtual machines in an availability set creates hello redundancy needed toomaintain availability of hello applications or services that your virtual machine runs.</span></span> <span data-ttu-id="8be22-103">如需有關其運作方式的詳細資訊，請參閱[管理虛擬機器可用性 hello][Manage hello availability of virtual machines]。</span><span class="sxs-lookup"><span data-stu-id="8be22-103">For details about how this works, see [Manage hello availability of virtual machines][Manage hello availability of virtual machines].</span></span>

<span data-ttu-id="8be22-104">它是最佳的作法 toouse 可用性設定組和負載平衡端點 toohelp 確保您的應用程式永遠可用且持續執行有效率。</span><span class="sxs-lookup"><span data-stu-id="8be22-104">It's a best practice toouse both availability sets and load-balancing endpoints toohelp ensure that your application is always available and running efficiently.</span></span> <span data-ttu-id="8be22-105">如需負載平衡端點的詳細資訊，請參閱 [Azure 基礎結構服務的負載平衡][Load balancing for Azure infrastructure services]。</span><span class="sxs-lookup"><span data-stu-id="8be22-105">For details about load-balanced endpoints, see [Load balancing for Azure infrastructure services][Load balancing for Azure infrastructure services].</span></span>

<span data-ttu-id="8be22-106">您可以使用下列兩個選項的其中之一，將傳統虛擬機器加入可用性設定組：</span><span class="sxs-lookup"><span data-stu-id="8be22-106">You can add classic virtual machines into an availability set by using one of two options:</span></span>

* <span data-ttu-id="8be22-107">[選項 1： 建立虛擬機器和可用性設定組 hello 在相同時間][Option 1: Create a virtual machine and an availability set at hello same time]。</span><span class="sxs-lookup"><span data-stu-id="8be22-107">[Option 1: Create a virtual machine and an availability set at hello same time][Option 1: Create a virtual machine and an availability set at hello same time].</span></span> <span data-ttu-id="8be22-108">然後，加入新的虛擬機器 toohello 建立這些虛擬機器時設定。</span><span class="sxs-lookup"><span data-stu-id="8be22-108">Then, add new virtual machines toohello set when you create those virtual machines.</span></span>
* <span data-ttu-id="8be22-109">[選項 2： 將現有的虛擬機器 tooan 可用性集][Option 2: Add an existing virtual machine tooan availability set]。</span><span class="sxs-lookup"><span data-stu-id="8be22-109">[Option 2: Add an existing virtual machine tooan availability set][Option 2: Add an existing virtual machine tooan availability set].</span></span>

> [!NOTE]
> <span data-ttu-id="8be22-110">在 hello 傳統模型中，虛擬機器中所要 tooput hello 相同可用性設定組必須屬於 toohello 相同雲端服務。</span><span class="sxs-lookup"><span data-stu-id="8be22-110">In hello classic model, virtual machines that you want tooput in hello same availability set must belong toohello same cloud service.</span></span>
> 
> 

## <span data-ttu-id="8be22-111"><a id="createset"></a>選項 1： 建立虛擬機器和可用性設定組 hello 在相同時間</span><span class="sxs-lookup"><span data-stu-id="8be22-111"><a id="createset"> </a>Option 1: Create a virtual machine and an availability set at hello same time</span></span>
<span data-ttu-id="8be22-112">您可以使用任一 hello Azure 入口網站或 Azure PowerShell 命令 toodo 這。</span><span class="sxs-lookup"><span data-stu-id="8be22-112">You can use either hello Azure portal or Azure PowerShell commands toodo this.</span></span>

<span data-ttu-id="8be22-113">toouse hello Azure 入口網站：</span><span class="sxs-lookup"><span data-stu-id="8be22-113">toouse hello Azure portal:</span></span>

1. <span data-ttu-id="8be22-114">如果您尚未這樣做，請登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="8be22-114">If you haven't already done so, sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="8be22-115">在 hello 中樞功能表中，按一下  **+ 新增**，然後按一下**虛擬機器**。</span><span class="sxs-lookup"><span data-stu-id="8be22-115">On hello hub menu, click **+ New**, and then click **Virtual Machine**.</span></span>
   
    ![替代映像文字](./media/virtual-machines-common-classic-configure-availability/ChooseVMImage.png)
3. <span data-ttu-id="8be22-117">選取您想 toouse 的 hello Marketplace 虛擬機器映像。</span><span class="sxs-lookup"><span data-stu-id="8be22-117">Select hello Marketplace virtual machine image you wish toouse.</span></span> <span data-ttu-id="8be22-118">您可以選擇 toocreate Linux 或 Windows 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="8be22-118">You can choose toocreate a Linux or Windows virtual machine.</span></span>
4. <span data-ttu-id="8be22-119">Hello 所選虛擬機器，請確認該 hello 部署模型設定得**傳統**，然後按一下**建立**</span><span class="sxs-lookup"><span data-stu-id="8be22-119">For hello selected virtual machine, verify that hello deployment model is set too**Classic** and then click **Create**</span></span>
   
    ![替代映像文字](./media/virtual-machines-common-classic-configure-availability/ChooseClassicModel.png)
5. <span data-ttu-id="8be22-121">輸入虛擬機器名稱、使用者名稱和密碼 (Windows 機器) 或 SSH 公開金鑰 (Linux 機器)。</span><span class="sxs-lookup"><span data-stu-id="8be22-121">Enter a virtual machine name, user name and password (for Windows machines) or SSH public key (for Linux machines).</span></span> 
6. <span data-ttu-id="8be22-122">選擇 hello VM 大小，然後按一下**選取**toocontinue。</span><span class="sxs-lookup"><span data-stu-id="8be22-122">Choose hello VM size and then click **Select** toocontinue.</span></span>
7. <span data-ttu-id="8be22-123">選擇**選擇性組態 > 可用性設定組**，然後選取您想要 tooadd hello 虛擬機器的 hello 可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="8be22-123">Choose **Optional Configuration > Availability set**, and select hello availability set you wish tooadd hello virtual machine to.</span></span>
   
    ![替代映像文字](./media/virtual-machines-common-classic-configure-availability/ChooseAvailabilitySet.png) 
8. <span data-ttu-id="8be22-125">檢閱組態設定。</span><span class="sxs-lookup"><span data-stu-id="8be22-125">Review your configuration settings.</span></span> <span data-ttu-id="8be22-126">完成之後，請按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="8be22-126">When you're done, click **Create**.</span></span>
9. <span data-ttu-id="8be22-127">當 Azure 建立虛擬機器時，您可以追蹤在 hello 進度**虛擬機器**hello 中樞功能表中。</span><span class="sxs-lookup"><span data-stu-id="8be22-127">While Azure creates your virtual machine, you can track hello progress under **Virtual Machines** in hello hub menu.</span></span>

<span data-ttu-id="8be22-128">toouse Azure PowerShell 命令 toocreate Azure 虛擬機器並將它加入 tooa 新的或現有的可用性設定組，請參閱[使用 Azure PowerShell toocreate 並預先設定 Windows 型虛擬機器](../articles/virtual-machines/windows/classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="8be22-128">toouse Azure PowerShell commands toocreate an Azure virtual machine and add it tooa new or existing availability set, see [Use Azure PowerShell toocreate and preconfigure Windows-based virtual machines](../articles/virtual-machines/windows/classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span></span>

## <span data-ttu-id="8be22-129"><a id="addmachine"></a>選項 2： 加入現有的虛擬機器 tooan 可用性集</span><span class="sxs-lookup"><span data-stu-id="8be22-129"><a id="addmachine"> </a>Option 2: Add an existing virtual machine tooan availability set</span></span>
<span data-ttu-id="8be22-130">在 hello Azure 入口網站，您可以新增現有的傳統虛擬機器 tooan 現有的可用性設定組或建立一個新的。</span><span class="sxs-lookup"><span data-stu-id="8be22-130">In hello Azure portal, you can add existing classic virtual machines tooan existing availability set or create a new one for them.</span></span> <span data-ttu-id="8be22-131">(請記住 hello 中的虛擬機器 hello 相同可用性設定組必須屬於 toohello 相同雲端服務。)hello 步驟幾乎是 hello 相同。</span><span class="sxs-lookup"><span data-stu-id="8be22-131">(Keep in mind that hello virtual machines in hello same availability set must belong toohello same cloud service.) hello steps are almost hello same.</span></span> <span data-ttu-id="8be22-132">使用 Azure PowerShell，您可以加入 hello 虛擬機器 tooan 現有可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="8be22-132">With Azure PowerShell, you can add hello virtual machine tooan existing availability set.</span></span>

1. <span data-ttu-id="8be22-133">如果您尚未這樣做，登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="8be22-133">If you have not already done so, sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="8be22-134">在 hello 中樞功能表中，按一下 **虛擬機器 （傳統）**。</span><span class="sxs-lookup"><span data-stu-id="8be22-134">On hello Hub menu, click **Virtual Machines (classic)**.</span></span>
   
    ![替代映像文字](./media/virtual-machines-common-classic-configure-availability/ChooseClassicVM.png)
3. <span data-ttu-id="8be22-136">從 hello 的虛擬機器的清單，選取 hello 想 tooadd toohello 組的 hello 虛擬機器名稱。</span><span class="sxs-lookup"><span data-stu-id="8be22-136">From hello list of virtual machines, select hello name of hello virtual machine that you want tooadd toohello set.</span></span>
4. <span data-ttu-id="8be22-137">選擇**可用性設定組**hello 虛擬機器從**設定**。</span><span class="sxs-lookup"><span data-stu-id="8be22-137">Choose **Availability set** from hello virtual machine **Settings**.</span></span>
   
    ![替代映像文字](./media/virtual-machines-common-classic-configure-availability/AvailabilitySetSettings.png)
5. <span data-ttu-id="8be22-139">選取您想要 tooadd hello 虛擬機器的 hello 可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="8be22-139">Select hello availability set you wish tooadd hello virtual machine to.</span></span> <span data-ttu-id="8be22-140">hello 虛擬機器必須屬於 toohello 相同雲端服務為 hello 可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="8be22-140">hello virtual machine must belong toohello same cloud service as hello availability set.</span></span>
   
    ![替代映像文字](./media/virtual-machines-common-classic-configure-availability/AvailabilitySetPicker.png)
6. <span data-ttu-id="8be22-142">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="8be22-142">Click **Save**.</span></span>

<span data-ttu-id="8be22-143">toouse Azure PowerShell 命令，開啟管理員層級 Azure PowerShell 工作階段，然後執行下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="8be22-143">toouse Azure PowerShell commands, open an administrator-level Azure PowerShell session and run hello following command.</span></span> <span data-ttu-id="8be22-144">Hello 預留位置 (例如&lt;VmCloudServiceName&gt;)，取代 hello 引號，包括 hello < 和 > 字元內的所有內容，請以 hello 更正名稱。</span><span class="sxs-lookup"><span data-stu-id="8be22-144">For hello placeholders (such as &lt;VmCloudServiceName&gt;), replace everything within hello quotes, including hello < and > characters, with hello correct names.</span></span>

    Get-AzureVM -ServiceName "<VmCloudServiceName>" -Name "<VmName>" | Set-AzureAvailabilitySet -AvailabilitySetName "<AvSetName>" | Update-AzureVM

> [!NOTE]
> <span data-ttu-id="8be22-145">hello 虛擬機器可能必須重新啟動 toobe toofinish 將它加入 toohello 可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="8be22-145">hello virtual machine might have toobe restarted toofinish adding it toohello availability set.</span></span>
> 
> 

<!-- LINKS -->
[Option 1: Create a virtual machine and an availability set at hello same time]: #createset
[Option 2: Add an existing virtual machine tooan availability set]: #addmachine

[Load balancing for Azure infrastructure services]: ../articles/virtual-machines/virtual-machines-linux-load-balance.md
[Manage hello availability of virtual machines]:../articles/virtual-machines/linux/manage-availability.md

[Create a virtual machine running Windows]: ../articles/virtual-machines/virtual-machines-windows-hero-tutorial.md
[Virtual Network overview]: ../articles/virtual-network/virtual-networks-overview.md

