

![獨立雲端服務中的虛擬機器](./media/virtual-machines-common-classic-connect-vms/CloudServiceExample.png)

<span data-ttu-id="7d20b-102">如果您將虛擬機器放在虛擬網路，您可以決定要將多少雲端服務用於負載平衡和可用性集。</span><span class="sxs-lookup"><span data-stu-id="7d20b-102">If you place your virtual machines in a virtual network, you can decide how many cloud services you want to use for load balancing and availability sets.</span></span> <span data-ttu-id="7d20b-103">此外，您可以利用內部部署網路的相同方式，在子網路上組織虛擬機器，並將虛擬網路連線到內部部署網路。</span><span class="sxs-lookup"><span data-stu-id="7d20b-103">Additionally, you can organize the virtual machines on subnets in the same way as your on-premises network and connect the virtual network to your on-premises network.</span></span> <span data-ttu-id="7d20b-104">以下是範例：</span><span class="sxs-lookup"><span data-stu-id="7d20b-104">Here's an example:</span></span>

![虛擬網路中的虛擬機器](./media/virtual-machines-common-classic-connect-vms/VirtualNetworkExample.png)

<span data-ttu-id="7d20b-106">若要在 Azure 中連線虛擬機器，建議使用虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="7d20b-106">Virtual networks are the recommended way to connect virtual machines in Azure.</span></span> <span data-ttu-id="7d20b-107">最佳作法是在個別的雲端服務中設定應用程式的每一層。</span><span class="sxs-lookup"><span data-stu-id="7d20b-107">The best practice is to configure each tier of your application in a separate cloud service.</span></span> <span data-ttu-id="7d20b-108">不過，您可能需要將不同應用程式層的部分虛擬機器結合至相同的雲端服務，以維持在每個訂用帳戶最多有 200 項雲端服務的限制內。</span><span class="sxs-lookup"><span data-stu-id="7d20b-108">However, you may need to combine some virtual machines from different application tiers into the same cloud service to remain within the maximum of 200 cloud services per subscription.</span></span> <span data-ttu-id="7d20b-109">若要檢閱本限制和其他限制，請參閱 [Azure 訂用帳戶和服務限制、配額與條件約束](../articles/azure-subscription-service-limits.md)。</span><span class="sxs-lookup"><span data-stu-id="7d20b-109">To review this and other limits, see [Azure Subscription and Service Limits, Quotas, and Constraints](../articles/azure-subscription-service-limits.md).</span></span>

## <a name="connect-vms-in-a-virtual-network"></a><span data-ttu-id="7d20b-110">連接虛擬網路中的 VM</span><span class="sxs-lookup"><span data-stu-id="7d20b-110">Connect VMs in a virtual network</span></span>
<span data-ttu-id="7d20b-111">若要連線虛擬網路中的虛擬機器：</span><span class="sxs-lookup"><span data-stu-id="7d20b-111">To connect virtual machines in a virtual network:</span></span>

1. <span data-ttu-id="7d20b-112">在 [Azure 入口網站](../articles/virtual-network/virtual-networks-create-vnet-classic-pportal.md)中建立虛擬網路並指定「傳統部署」。</span><span class="sxs-lookup"><span data-stu-id="7d20b-112">Create the virtual network in the [Azure portal](../articles/virtual-network/virtual-networks-create-vnet-classic-pportal.md) and specify 'classic deployment'.</span></span>
2. <span data-ttu-id="7d20b-113">為部署一組建立雲端服務，以反映可用性設定組和負載平衡的設計。</span><span class="sxs-lookup"><span data-stu-id="7d20b-113">Create the set of cloud services for your deployment to reflect your design for availability sets and load balancing.</span></span> <span data-ttu-id="7d20b-114">在 Azure 入口網站中，針對每個雲端服務，按一下 [新增] > [計算] > [雲端服務]。</span><span class="sxs-lookup"><span data-stu-id="7d20b-114">In the Azure portal, click **New > Compute > Cloud service** for each cloud service.</span></span>

  <span data-ttu-id="7d20b-115">當您填寫雲端服務詳細資料時，請選擇搭配虛擬網路使用的相同「資源群組」。</span><span class="sxs-lookup"><span data-stu-id="7d20b-115">As you fill out the cloud service details, choose the same _resource group_ used with the virtual network.</span></span>

3. <span data-ttu-id="7d20b-116">若要建立每個新的虛擬機器，請按一下 [新增] > [計算]，然後從 [精選 App] 中選取適當的 VM 映像。</span><span class="sxs-lookup"><span data-stu-id="7d20b-116">To create each new virtual machine, click **New > Compute**, then select the appropriate VM image from the **Featured apps**.</span></span>

  <span data-ttu-id="7d20b-117">在 VM 的 [基本概念] 刀鋒視窗中，選擇搭配虛擬網路使用的相同「資源群組」。</span><span class="sxs-lookup"><span data-stu-id="7d20b-117">In the VM **Basics** blade, choose the same _resource group_ used with the virtual network.</span></span>

  ![使用 VNet 時的 VM 基本概念刀鋒視窗](./media/virtual-machines-common-classic-connect-vms/CreateVM_Basics_VN.png)

4. <span data-ttu-id="7d20b-119">當您填寫 VM 的 [設定] 時，為 VM 選擇正確的「雲端服務」和「虛擬網路」。</span><span class="sxs-lookup"><span data-stu-id="7d20b-119">As you fill out the VM **Settings**, choose the correct _Cloud service_ or _virtual network_ for the VM.</span></span>

  <span data-ttu-id="7d20b-120">Azure 會根據您選取的項目來選取其他項目。</span><span class="sxs-lookup"><span data-stu-id="7d20b-120">Azure will select the other item based on your selection.</span></span>

  ![使用 VNet 時的 VM 設定刀鋒視窗](./media/virtual-machines-common-classic-connect-vms/CreateVM_Settings_VN.png)


## <a name="connect-vms-in-a-standalone-cloud-service"></a><span data-ttu-id="7d20b-122">連接獨立雲端服務中的 VM</span><span class="sxs-lookup"><span data-stu-id="7d20b-122">Connect VMs in a standalone cloud service</span></span>
<span data-ttu-id="7d20b-123">若要在獨立雲端服務中連接虛擬機器：</span><span class="sxs-lookup"><span data-stu-id="7d20b-123">To connect virtual machines in a standalone cloud service:</span></span>

1. <span data-ttu-id="7d20b-124">在 [Azure 入口網站](http://portal.azure.com)中建立雲端服務。</span><span class="sxs-lookup"><span data-stu-id="7d20b-124">Create the cloud service in the [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="7d20b-125">按一下 [新增] > [計算] > [雲端服務]。</span><span class="sxs-lookup"><span data-stu-id="7d20b-125">Click **New > Compute > Cloud service**.</span></span> <span data-ttu-id="7d20b-126">或者，當您建立第一部虛擬機器時，您可以為您的部署建立雲端服務。</span><span class="sxs-lookup"><span data-stu-id="7d20b-126">Or, you can create the cloud service for your deployment when you create your first virtual machine.</span></span>
2. <span data-ttu-id="7d20b-127">當您建立虛擬機器時，請選擇搭配雲端服務使用的相同資源群組。</span><span class="sxs-lookup"><span data-stu-id="7d20b-127">When you create the virtual machines, choose the same resource group used with the cloud service.</span></span>

  ![將虛擬機器加入至現有的雲端服務。](./media/virtual-machines-common-classic-connect-vms/CreateVM_Basics_SA.png)

3.  <span data-ttu-id="7d20b-129">當您填寫 VM 詳細資料時，請選擇在第一個步驟中建立的雲端服務名稱。</span><span class="sxs-lookup"><span data-stu-id="7d20b-129">As you fill out the VM details, choose the name of cloud service created in the first step.</span></span>

  ![選取虛擬機器的雲端服務](./media/virtual-machines-common-classic-connect-vms/CreateVM_Settings_SA.png)
