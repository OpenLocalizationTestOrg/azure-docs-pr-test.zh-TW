1. <span data-ttu-id="a3edc-101">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="a3edc-101">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="a3edc-102">從開始 hello 左上方，按一下**新增 > 計算 > Windows Server 2016 Datacenter**。</span><span class="sxs-lookup"><span data-stu-id="a3edc-102">Starting in hello upper left, click **New > Compute > Windows Server 2016 Datacenter**.</span></span>

    ![瀏覽 toohello hello 入口網站中的 Azure VM 映像](./media/virtual-machines-common-portal-create-fqdn/marketplace-new.png)

3. <span data-ttu-id="a3edc-104">在 Windows Server 2016 Datacenter hello，選取 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="a3edc-104">On hello Windows Server 2016 Datacenter, select hello Classic deployment model.</span></span> <span data-ttu-id="a3edc-105">按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="a3edc-105">Click Create.</span></span>

    ![顯示可用在 hello 入口網站中的 hello Azure VM 映像的螢幕擷取畫面](./media/virtual-machines-common-portal-create-fqdn/deployment-classic-model.png)

## <a name="1-basics-blade"></a><span data-ttu-id="a3edc-107">1.基本概念刀鋒視窗</span><span class="sxs-lookup"><span data-stu-id="a3edc-107">1. Basics blade</span></span>

<span data-ttu-id="a3edc-108">刀鋒視窗中的基本概念 hello 要求 hello 虛擬機器的系統管理資訊。</span><span class="sxs-lookup"><span data-stu-id="a3edc-108">hello Basics blade requests administrative information for hello virtual machine.</span></span>

1. <span data-ttu-id="a3edc-109">輸入**名稱**hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a3edc-109">Enter a **Name** for hello virtual machine.</span></span> <span data-ttu-id="a3edc-110">在 hello 範例_HeroVM_ hello hello 虛擬機器名稱。</span><span class="sxs-lookup"><span data-stu-id="a3edc-110">In hello example, _HeroVM_ is hello name of hello virtual machine.</span></span> <span data-ttu-id="a3edc-111">hello 名稱必須是 1 到 15 個字元，而且它不能包含特殊字元。</span><span class="sxs-lookup"><span data-stu-id="a3edc-111">hello name must be 1-15 characters long and it cannot contain special characters.</span></span>

2. <span data-ttu-id="a3edc-112">輸入**使用者名**和強式**密碼**所使用的 toocreate hello VM 上的本機帳戶。</span><span class="sxs-lookup"><span data-stu-id="a3edc-112">Enter a **User name** and a strong **Password** that are used toocreate a local account on hello VM.</span></span> <span data-ttu-id="a3edc-113">hello 使用本機帳戶是在 tooand toosign 管理 hello VM。</span><span class="sxs-lookup"><span data-stu-id="a3edc-113">hello local account is used toosign in tooand manage hello VM.</span></span> <span data-ttu-id="a3edc-114">在 hello 範例_azureuser_是 hello 的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="a3edc-114">In hello example, _azureuser_ is hello user name.</span></span>

 <span data-ttu-id="a3edc-115">hello 密碼必須介於 8 123 個字元並符合個 hello 四個下列複雜性需求的三種： 一個小寫字元、 一個大寫字元、 一個數字和一個特殊字元。</span><span class="sxs-lookup"><span data-stu-id="a3edc-115">hello password must be 8-123 characters long and meet three out of hello four following complexity requirements: one lower case character, one upper case character, one number, and one special character.</span></span> <span data-ttu-id="a3edc-116">進一步了解 [使用者名稱和密碼需求](../articles/virtual-machines/windows/faq.md)。</span><span class="sxs-lookup"><span data-stu-id="a3edc-116">See more about [username and password requirements](../articles/virtual-machines/windows/faq.md).</span></span>

3. <span data-ttu-id="a3edc-117">hello**訂用帳戶**是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="a3edc-117">hello **Subscription** is optional.</span></span> <span data-ttu-id="a3edc-118">一個常見的設定是「隨用隨付」。</span><span class="sxs-lookup"><span data-stu-id="a3edc-118">One common setting is "Pay-As-You-Go".</span></span>

4. <span data-ttu-id="a3edc-119">選取現有**資源群組**或新的型別 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="a3edc-119">Select an existing **Resource group** or type hello name for a new one.</span></span> <span data-ttu-id="a3edc-120">在 hello 範例_HeroVMRG_ hello hello 資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="a3edc-120">In hello example, _HeroVMRG_ is hello name of hello resource group.</span></span>

5. <span data-ttu-id="a3edc-121">選取 Azure 資料中心**位置**想 hello VM toorun。</span><span class="sxs-lookup"><span data-stu-id="a3edc-121">Select an Azure datacenter **Location** where you want hello VM toorun.</span></span> <span data-ttu-id="a3edc-122">在 hello 範例**美國東部**hello 位置。</span><span class="sxs-lookup"><span data-stu-id="a3edc-122">In hello example, **East US** is hello location.</span></span>

6. <span data-ttu-id="a3edc-123">當您完成之後時，按一下 [**下一步**toocontinue toohello 下一步] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="a3edc-123">When you are done, click **Next** toocontinue toohello next blade.</span></span>

    ![顯示 hello 設定 hello 設定 Azure VM 的基本概念 刀鋒視窗的螢幕擷取畫面](./media/virtual-machines-common-portal-create-fqdn/basics-blade-classic.png)

## <a name="2-size-blade"></a><span data-ttu-id="a3edc-125">2.大小刀鋒視窗</span><span class="sxs-lookup"><span data-stu-id="a3edc-125">2. Size blade</span></span>

<span data-ttu-id="a3edc-126">hello 大小刀鋒視窗可識別 hello VM，hello 設定詳細資料，並列出包含作業系統、 處理器數目、 磁碟儲存體類型及預估每月的使用成本的各種選項。</span><span class="sxs-lookup"><span data-stu-id="a3edc-126">hello Size blade identifies hello configuration details of hello VM, and lists various choices that include OS, number of processors, disk storage type, and estimated monthly usage costs.</span></span>  

<span data-ttu-id="a3edc-127">選擇 VM 大小，然後按一下**選取**toocontinue。</span><span class="sxs-lookup"><span data-stu-id="a3edc-127">Choose a VM size, and then click **Select** toocontinue.</span></span> <span data-ttu-id="a3edc-128">在此範例中， _DS1_\__V2 標準_是 hello 的 VM 大小。</span><span class="sxs-lookup"><span data-stu-id="a3edc-128">In this example, _DS1_\__V2 Standard_ is hello VM size.</span></span>

  ![顯示 hello Azure VM 大小，您可以選取的 hello 大小刀鋒視窗的螢幕擷取畫面](./media/virtual-machines-common-portal-create-fqdn/vm-size-classic.png)


## <a name="3-settings-blade"></a><span data-ttu-id="a3edc-130">3.設定刀鋒視窗</span><span class="sxs-lookup"><span data-stu-id="a3edc-130">3. Settings blade</span></span>

<span data-ttu-id="a3edc-131">hello 設定 刀鋒視窗會要求儲存體和網路的選項。</span><span class="sxs-lookup"><span data-stu-id="a3edc-131">hello Settings blade requests storage and network options.</span></span> <span data-ttu-id="a3edc-132">您可以接受 hello 預設設定。</span><span class="sxs-lookup"><span data-stu-id="a3edc-132">You can accept hello default settings.</span></span> <span data-ttu-id="a3edc-133">Azure 會視需要建立適當的項目。</span><span class="sxs-lookup"><span data-stu-id="a3edc-133">Azure creates appropriate entries where necessary.</span></span>

<span data-ttu-id="a3edc-134">如果您選取支援的虛擬機器大小，就能藉由選取 [磁碟類型] 中的 [進階 (SSD)]，嘗試使用 Azure 進階儲存體。</span><span class="sxs-lookup"><span data-stu-id="a3edc-134">If you selected a virtual machine size that supports it, you can try Azure Premium Storage by selecting Premium (SSD) in Disk type.</span></span>

<span data-ttu-id="a3edc-135">當您完成變更時，請按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="a3edc-135">When you're done making changes, click **OK**.</span></span>

## <a name="4-summary-blade"></a><span data-ttu-id="a3edc-136">4.摘要刀鋒視窗</span><span class="sxs-lookup"><span data-stu-id="a3edc-136">4. Summary blade</span></span>

<span data-ttu-id="a3edc-137">hello 摘要刀鋒視窗會列出 hello hello 先前刀鋒視窗中指定的設定。</span><span class="sxs-lookup"><span data-stu-id="a3edc-137">hello Summary blade lists hello settings specified in hello previous blades.</span></span> <span data-ttu-id="a3edc-138">按一下**確定**當您準備好 toomake hello 映像。</span><span class="sxs-lookup"><span data-stu-id="a3edc-138">Click **OK** when you're ready toomake hello image.</span></span>

 ![刀鋒視窗中摘要報表中，提供指定 hello 虛擬機器的設定](./media/virtual-machines-common-portal-create-fqdn/summary-blade-classic.png)

<span data-ttu-id="a3edc-140">Hello 入口網站建立 hello 虛擬機器之後，會列出下 hello 新虛擬機器**所有資源**，並顯示 hello 虛擬機器的並排顯示 hello 儀表板上。</span><span class="sxs-lookup"><span data-stu-id="a3edc-140">After hello virtual machine is created, hello portal lists hello new virtual machine under **All resources**, and displays a tile of hello virtual machine on hello dashboard.</span></span> <span data-ttu-id="a3edc-141">hello 對應雲端服務和儲存體帳戶也會建立並列出。</span><span class="sxs-lookup"><span data-stu-id="a3edc-141">hello corresponding cloud service and storage account also are created and listed.</span></span> <span data-ttu-id="a3edc-142">Hello 虛擬機器和雲端服務會自動啟動，而其狀態會列為**執行**。</span><span class="sxs-lookup"><span data-stu-id="a3edc-142">Both hello virtual machine and cloud service are started automatically and their status is listed as **Running**.</span></span>

 ![設定 VM 代理程式 」 和 「 hello hello 虛擬機器端點](./media/virtual-machines-common-portal-create-fqdn/portal-with-new-vm.png)
