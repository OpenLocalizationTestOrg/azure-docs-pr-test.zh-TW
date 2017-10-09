

![獨立雲端服務中的虛擬機器](./media/virtual-machines-common-classic-connect-vms/CloudServiceExample.png)

<span data-ttu-id="f06da-102">如果您將虛擬機器放在虛擬網路中，您可以決定多少的雲端服務，您想要針對 toouse 負載平衡和可用性集。</span><span class="sxs-lookup"><span data-stu-id="f06da-102">If you place your virtual machines in a virtual network, you can decide how many cloud services you want toouse for load balancing and availability sets.</span></span> <span data-ttu-id="f06da-103">此外，您可以將組織 hello 虛擬機器在 hello 的子網路上相同方式與您內部網路，而且連線 hello 虛擬網路 tooyour 內部部署網路。</span><span class="sxs-lookup"><span data-stu-id="f06da-103">Additionally, you can organize hello virtual machines on subnets in hello same way as your on-premises network and connect hello virtual network tooyour on-premises network.</span></span> <span data-ttu-id="f06da-104">以下是範例：</span><span class="sxs-lookup"><span data-stu-id="f06da-104">Here's an example:</span></span>

![虛擬網路中的虛擬機器](./media/virtual-machines-common-classic-connect-vms/VirtualNetworkExample.png)

<span data-ttu-id="f06da-106">虛擬網路是建議的方式 tooconnect Azure 虛擬機器中的 hello。</span><span class="sxs-lookup"><span data-stu-id="f06da-106">Virtual networks are hello recommended way tooconnect virtual machines in Azure.</span></span> <span data-ttu-id="f06da-107">hello 最佳作法是 tooconfigure 個別的雲端服務中的應用程式的每一層。</span><span class="sxs-lookup"><span data-stu-id="f06da-107">hello best practice is tooconfigure each tier of your application in a separate cloud service.</span></span> <span data-ttu-id="f06da-108">不過，您可能需要 toocombine 部分虛擬機器從 hello 到不同的應用程式層相同雲端服務 tooremain hello 最大值為 200 的雲端服務，每個訂用帳戶內。</span><span class="sxs-lookup"><span data-stu-id="f06da-108">However, you may need toocombine some virtual machines from different application tiers into hello same cloud service tooremain within hello maximum of 200 cloud services per subscription.</span></span> <span data-ttu-id="f06da-109">tooreview 這和其他限制，請參閱[Azure 訂用帳戶和服務限制、 配額和條件約束](../articles/azure-subscription-service-limits.md)。</span><span class="sxs-lookup"><span data-stu-id="f06da-109">tooreview this and other limits, see [Azure Subscription and Service Limits, Quotas, and Constraints](../articles/azure-subscription-service-limits.md).</span></span>

## <a name="connect-vms-in-a-virtual-network"></a><span data-ttu-id="f06da-110">連接虛擬網路中的 VM</span><span class="sxs-lookup"><span data-stu-id="f06da-110">Connect VMs in a virtual network</span></span>
<span data-ttu-id="f06da-111">tooconnect 虛擬網路中的虛擬機器：</span><span class="sxs-lookup"><span data-stu-id="f06da-111">tooconnect virtual machines in a virtual network:</span></span>

1. <span data-ttu-id="f06da-112">建立 hello 虛擬網路中 hello [Azure 入口網站](../articles/virtual-network/virtual-networks-create-vnet-classic-pportal.md)並指定 '傳統部署'。</span><span class="sxs-lookup"><span data-stu-id="f06da-112">Create hello virtual network in hello [Azure portal](../articles/virtual-network/virtual-networks-create-vnet-classic-pportal.md) and specify 'classic deployment'.</span></span>
2. <span data-ttu-id="f06da-113">建立用於部署 tooreflect 的雲端服務的 hello 組您的設計為可用性設定組和負載平衡。</span><span class="sxs-lookup"><span data-stu-id="f06da-113">Create hello set of cloud services for your deployment tooreflect your design for availability sets and load balancing.</span></span> <span data-ttu-id="f06da-114">在 hello Azure 入口網站，按一下 **新增 > 計算 > 雲端服務**每個雲端服務。</span><span class="sxs-lookup"><span data-stu-id="f06da-114">In hello Azure portal, click **New > Compute > Cloud service** for each cloud service.</span></span>

  <span data-ttu-id="f06da-115">當您填寫 hello 雲端服務詳細資料，請選擇 hello 相同_資源群組_搭配 hello 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="f06da-115">As you fill out hello cloud service details, choose hello same _resource group_ used with hello virtual network.</span></span>

3. <span data-ttu-id="f06da-116">toocreate 每個新虛擬機器，請按一下**新增 > 計算**，然後選取 hello 適當的 VM 映像從 hello**熱門應用程式**。</span><span class="sxs-lookup"><span data-stu-id="f06da-116">toocreate each new virtual machine, click **New > Compute**, then select hello appropriate VM image from hello **Featured apps**.</span></span>

  <span data-ttu-id="f06da-117">在 hello VM**基本概念**刀鋒視窗中，選擇 hello 相同_資源群組_搭配 hello 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="f06da-117">In hello VM **Basics** blade, choose hello same _resource group_ used with hello virtual network.</span></span>

  ![使用 VNet 時的 VM 基本概念刀鋒視窗](./media/virtual-machines-common-classic-connect-vms/CreateVM_Basics_VN.png)

4. <span data-ttu-id="f06da-119">當您填寫 hello VM**設定**，選擇正確的 hello_雲端服務_或_虛擬網路_hello VM。</span><span class="sxs-lookup"><span data-stu-id="f06da-119">As you fill out hello VM **Settings**, choose hello correct _Cloud service_ or _virtual network_ for hello VM.</span></span>

  <span data-ttu-id="f06da-120">Azure 將會選取 hello 其他項目會根據您選取。</span><span class="sxs-lookup"><span data-stu-id="f06da-120">Azure will select hello other item based on your selection.</span></span>

  ![使用 VNet 時的 VM 設定刀鋒視窗](./media/virtual-machines-common-classic-connect-vms/CreateVM_Settings_VN.png)


## <a name="connect-vms-in-a-standalone-cloud-service"></a><span data-ttu-id="f06da-122">連接獨立雲端服務中的 VM</span><span class="sxs-lookup"><span data-stu-id="f06da-122">Connect VMs in a standalone cloud service</span></span>
<span data-ttu-id="f06da-123">tooconnect 獨立雲端服務中的虛擬機器：</span><span class="sxs-lookup"><span data-stu-id="f06da-123">tooconnect virtual machines in a standalone cloud service:</span></span>

1. <span data-ttu-id="f06da-124">建立 hello 的雲端服務中 hello [Azure 入口網站](http://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="f06da-124">Create hello cloud service in hello [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="f06da-125">按一下 [新增] > [計算] > [雲端服務]。</span><span class="sxs-lookup"><span data-stu-id="f06da-125">Click **New > Compute > Cloud service**.</span></span> <span data-ttu-id="f06da-126">或者，當您建立您第一部虛擬機器時，您可以建立您的部署的 hello 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="f06da-126">Or, you can create hello cloud service for your deployment when you create your first virtual machine.</span></span>
2. <span data-ttu-id="f06da-127">當您建立 hello 虛擬機器時，請選擇的 hello 與 hello 雲端服務使用相同的資源群組。</span><span class="sxs-lookup"><span data-stu-id="f06da-127">When you create hello virtual machines, choose hello same resource group used with hello cloud service.</span></span>

  ![新增虛擬機器 tooan 現有雲端服務](./media/virtual-machines-common-classic-connect-vms/CreateVM_Basics_SA.png)

3.  <span data-ttu-id="f06da-129">當您填寫 hello VM 詳細資料時，選擇 hello hello 第一個步驟中建立的雲端服務名稱。</span><span class="sxs-lookup"><span data-stu-id="f06da-129">As you fill out hello VM details, choose hello name of cloud service created in hello first step.</span></span>

  ![選取虛擬機器的雲端服務](./media/virtual-machines-common-classic-connect-vms/CreateVM_Settings_SA.png)
