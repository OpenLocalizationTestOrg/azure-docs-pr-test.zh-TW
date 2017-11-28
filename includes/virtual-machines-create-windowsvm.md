1. <span data-ttu-id="2aeac-101">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="2aeac-101">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="2aeac-102">從左上角開始，依序按一下 [新增] > [計算] > [Windows Server 2016 Datacenter]。</span><span class="sxs-lookup"><span data-stu-id="2aeac-102">Starting in the upper left, click **New > Compute > Windows Server 2016 Datacenter**.</span></span>

    ![瀏覽至入口網站中的 Azure VM 映像](./media/virtual-machines-common-portal-create-fqdn/marketplace-new.png)

3. <span data-ttu-id="2aeac-104">在 Windows Server 2016 Datacenter 中，選取傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="2aeac-104">On the Windows Server 2016 Datacenter, select the Classic deployment model.</span></span> <span data-ttu-id="2aeac-105">按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="2aeac-105">Click Create.</span></span>

    ![顯示在入口網站中可用 Azure VM 映像的螢幕擷取畫面](./media/virtual-machines-common-portal-create-fqdn/deployment-classic-model.png)

## <a name="1-basics-blade"></a><span data-ttu-id="2aeac-107">1.基本概念刀鋒視窗</span><span class="sxs-lookup"><span data-stu-id="2aeac-107">1. Basics blade</span></span>

<span data-ttu-id="2aeac-108">[基本] 刀鋒視窗需要虛擬機器的系統管理資訊。</span><span class="sxs-lookup"><span data-stu-id="2aeac-108">The Basics blade requests administrative information for the virtual machine.</span></span>

1. <span data-ttu-id="2aeac-109">輸入虛擬機器的**名稱**。</span><span class="sxs-lookup"><span data-stu-id="2aeac-109">Enter a **Name** for the virtual machine.</span></span> <span data-ttu-id="2aeac-110">在此範例中，HeroVM 是虛擬機器的名稱。</span><span class="sxs-lookup"><span data-stu-id="2aeac-110">In the example, _HeroVM_ is the name of the virtual machine.</span></span> <span data-ttu-id="2aeac-111">名稱必須為 1-15 個字元，不能包含特殊字元。</span><span class="sxs-lookup"><span data-stu-id="2aeac-111">The name must be 1-15 characters long and it cannot contain special characters.</span></span>

2. <span data-ttu-id="2aeac-112">輸入用來在 VM 上建立本機帳戶的**使用者名稱**和強式**密碼**。</span><span class="sxs-lookup"><span data-stu-id="2aeac-112">Enter a **User name** and a strong **Password** that are used to create a local account on the VM.</span></span> <span data-ttu-id="2aeac-113">此本機帳戶用來登入及管理 VM。</span><span class="sxs-lookup"><span data-stu-id="2aeac-113">The local account is used to sign in to and manage the VM.</span></span> <span data-ttu-id="2aeac-114">在此範例中，azureuser 是使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="2aeac-114">In the example, _azureuser_ is the user name.</span></span>

 <span data-ttu-id="2aeac-115">密碼長度必須是 8-123 個字元，且符合下列四個複雜性需求的其中三項：1 個小寫字元、1 個大寫字元、1 個數字和 1 個特殊字元。</span><span class="sxs-lookup"><span data-stu-id="2aeac-115">The password must be 8-123 characters long and meet three out of the four following complexity requirements: one lower case character, one upper case character, one number, and one special character.</span></span> <span data-ttu-id="2aeac-116">進一步了解 [使用者名稱和密碼需求](../articles/virtual-machines/windows/faq.md)。</span><span class="sxs-lookup"><span data-stu-id="2aeac-116">See more about [username and password requirements](../articles/virtual-machines/windows/faq.md).</span></span>

3. <span data-ttu-id="2aeac-117">[訂用帳戶] 是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="2aeac-117">The **Subscription** is optional.</span></span> <span data-ttu-id="2aeac-118">一個常見的設定是「隨用隨付」。</span><span class="sxs-lookup"><span data-stu-id="2aeac-118">One common setting is "Pay-As-You-Go".</span></span>

4. <span data-ttu-id="2aeac-119">選取現有的**資源群組**，或輸入新群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="2aeac-119">Select an existing **Resource group** or type the name for a new one.</span></span> <span data-ttu-id="2aeac-120">在此範例中，HeroVMRG 是資源群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="2aeac-120">In the example, _HeroVMRG_ is the name of the resource group.</span></span>

5. <span data-ttu-id="2aeac-121">選取您要執行 VM 的 Azure Datacenter **位置**。</span><span class="sxs-lookup"><span data-stu-id="2aeac-121">Select an Azure datacenter **Location** where you want the VM to run.</span></span> <span data-ttu-id="2aeac-122">在此範例中，East US 就是位置。</span><span class="sxs-lookup"><span data-stu-id="2aeac-122">In the example, **East US** is the location.</span></span>

6. <span data-ttu-id="2aeac-123">當您完成時，按 [下一步] 繼續下一個刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="2aeac-123">When you are done, click **Next** to continue to the next blade.</span></span>

    ![顯示用於設定 Azure VM 之 [基本概念] 刀鋒視窗上的設定的螢幕擷取畫面](./media/virtual-machines-common-portal-create-fqdn/basics-blade-classic.png)

## <a name="2-size-blade"></a><span data-ttu-id="2aeac-125">2.大小刀鋒視窗</span><span class="sxs-lookup"><span data-stu-id="2aeac-125">2. Size blade</span></span>

<span data-ttu-id="2aeac-126">[大小] 刀鋒視窗會識別 VM 的設定詳細資料，並列出各種選擇，包括作業系統、處理器數目、磁碟儲存體類型，以及估計的每月使用成本。</span><span class="sxs-lookup"><span data-stu-id="2aeac-126">The Size blade identifies the configuration details of the VM, and lists various choices that include OS, number of processors, disk storage type, and estimated monthly usage costs.</span></span>  

<span data-ttu-id="2aeac-127">選擇 VM 大小，然後按一下 [選取] 以繼續。</span><span class="sxs-lookup"><span data-stu-id="2aeac-127">Choose a VM size, and then click **Select** to continue.</span></span> <span data-ttu-id="2aeac-128">在此範例中，DS1\_V2 Standard 就是 VM 大小。</span><span class="sxs-lookup"><span data-stu-id="2aeac-128">In this example, _DS1_\__V2 Standard_ is the VM size.</span></span>

  ![顯示您可以選取之 Azure VM 大小的 [大小] 刀鋒視窗的螢幕擷取畫面](./media/virtual-machines-common-portal-create-fqdn/vm-size-classic.png)


## <a name="3-settings-blade"></a><span data-ttu-id="2aeac-130">3.設定刀鋒視窗</span><span class="sxs-lookup"><span data-stu-id="2aeac-130">3. Settings blade</span></span>

<span data-ttu-id="2aeac-131">[設定] 刀鋒視窗需要儲存體和網路選項。</span><span class="sxs-lookup"><span data-stu-id="2aeac-131">The Settings blade requests storage and network options.</span></span> <span data-ttu-id="2aeac-132">您可以接受預設設定。</span><span class="sxs-lookup"><span data-stu-id="2aeac-132">You can accept the default settings.</span></span> <span data-ttu-id="2aeac-133">Azure 會視需要建立適當的項目。</span><span class="sxs-lookup"><span data-stu-id="2aeac-133">Azure creates appropriate entries where necessary.</span></span>

<span data-ttu-id="2aeac-134">如果您選取支援的虛擬機器大小，就能藉由選取 [磁碟類型] 中的 [進階 (SSD)]，嘗試使用 Azure 進階儲存體。</span><span class="sxs-lookup"><span data-stu-id="2aeac-134">If you selected a virtual machine size that supports it, you can try Azure Premium Storage by selecting Premium (SSD) in Disk type.</span></span>

<span data-ttu-id="2aeac-135">當您完成變更時，請按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="2aeac-135">When you're done making changes, click **OK**.</span></span>

## <a name="4-summary-blade"></a><span data-ttu-id="2aeac-136">4.摘要刀鋒視窗</span><span class="sxs-lookup"><span data-stu-id="2aeac-136">4. Summary blade</span></span>

<span data-ttu-id="2aeac-137">[摘要] 刀鋒視窗會列出先前刀鋒視窗中所指定的設定。</span><span class="sxs-lookup"><span data-stu-id="2aeac-137">The Summary blade lists the settings specified in the previous blades.</span></span> <span data-ttu-id="2aeac-138">當您準備好製作映像時，按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="2aeac-138">Click **OK** when you're ready to make the image.</span></span>

 ![提供所指定虛擬機器設定的 [摘要] 刀鋒視窗報告](./media/virtual-machines-common-portal-create-fqdn/summary-blade-classic.png)

<span data-ttu-id="2aeac-140">建立虛擬機器後，入口網站會在 [所有資源] 底下列出新的虛擬機器，並在儀表板上顯示虛擬機器圖格。</span><span class="sxs-lookup"><span data-stu-id="2aeac-140">After the virtual machine is created, the portal lists the new virtual machine under **All resources**, and displays a tile of the virtual machine on the dashboard.</span></span> <span data-ttu-id="2aeac-141">同時也會建立並列出對應的雲端服務和儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="2aeac-141">The corresponding cloud service and storage account also are created and listed.</span></span> <span data-ttu-id="2aeac-142">虛擬機器和雲端服務都會自動啟動，而且它們的狀態會顯示為 [執行中] 。</span><span class="sxs-lookup"><span data-stu-id="2aeac-142">Both the virtual machine and cloud service are started automatically and their status is listed as **Running**.</span></span>

 ![設定 VM 代理程式和需擬機器端點](./media/virtual-machines-common-portal-create-fqdn/portal-with-new-vm.png)
