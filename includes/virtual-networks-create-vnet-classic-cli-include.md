## <a name="how-toocreate-a-classic-vnet-using-azure-cli"></a><span data-ttu-id="a6ec6-101">如何使用 Azure CLI 傳統 VNet toocreate</span><span class="sxs-lookup"><span data-stu-id="a6ec6-101">How toocreate a classic VNet using Azure CLI</span></span>
<span data-ttu-id="a6ec6-102">您可以使用 hello Azure CLI toomanage hello 命令提示字元，從任何執行 Windows、 Linux 或是 OSX 電腦從您的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="a6ec6-102">You can use hello Azure CLI toomanage your Azure resources from hello command prompt from any computer running Windows, Linux, or OSX.</span></span> <span data-ttu-id="a6ec6-103">toocreate VNet 使用 hello Azure CLI，請遵循下列 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="a6ec6-103">toocreate a VNet by using hello Azure CLI, follow hello steps below.</span></span>

1. <span data-ttu-id="a6ec6-104">如果您從未使用過 Azure CLI，請參閱[安裝及設定 hello Azure CLI](../articles/cli-install-nodejs.md)依照 hello 向上 toohello 點，選取您的 Azure 帳戶和訂用帳戶的指示進行。</span><span class="sxs-lookup"><span data-stu-id="a6ec6-104">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../articles/cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="a6ec6-105">執行 hello **azure 網路 vnet 建立**命令 toocreate VNet 和子網路，如下所示。</span><span class="sxs-lookup"><span data-stu-id="a6ec6-105">Run hello **azure network vnet create** command toocreate a VNet and a subnet, as shown below.</span></span> <span data-ttu-id="a6ec6-106">之後再 hello 輸出所示的 hello 清單說明使用 hello 參數。</span><span class="sxs-lookup"><span data-stu-id="a6ec6-106">hello list shown after hello output explains hello parameters used.</span></span>
   
            azure network vnet create --vnet TestVNet -e 192.168.0.0 -i 16 -n FrontEnd -p 192.168.1.0 -r 24 -l "Central US"
   
    <span data-ttu-id="a6ec6-107">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="a6ec6-107">Expected output:</span></span>
   
            info:    Executing command network vnet create
            + Looking up network configuration
            + Looking up locations
            + Setting network configuration
            info:    network vnet create command OK
   
   * <span data-ttu-id="a6ec6-108">**--vnet**。</span><span class="sxs-lookup"><span data-stu-id="a6ec6-108">**--vnet**.</span></span> <span data-ttu-id="a6ec6-109">建立 hello VNet toobe 的名稱。</span><span class="sxs-lookup"><span data-stu-id="a6ec6-109">Name of hello VNet toobe created.</span></span> <span data-ttu-id="a6ec6-110">在本文案例中為 *TestVNet*</span><span class="sxs-lookup"><span data-stu-id="a6ec6-110">For our scenario, *TestVNet*</span></span>
   * <span data-ttu-id="a6ec6-111">**-e (或 --address-space)**。</span><span class="sxs-lookup"><span data-stu-id="a6ec6-111">**-e (or --address-space)**.</span></span> <span data-ttu-id="a6ec6-112">VNet 位址空間。</span><span class="sxs-lookup"><span data-stu-id="a6ec6-112">VNet address space.</span></span> <span data-ttu-id="a6ec6-113">在本文案例中為 *192.168.0.0*</span><span class="sxs-lookup"><span data-stu-id="a6ec6-113">For our scenario, *192.168.0.0*</span></span>
   * <span data-ttu-id="a6ec6-114">**-i (或 -cidr)**。</span><span class="sxs-lookup"><span data-stu-id="a6ec6-114">**-i (or -cidr)**.</span></span> <span data-ttu-id="a6ec6-115">CIDR 格式的網路遮罩。</span><span class="sxs-lookup"><span data-stu-id="a6ec6-115">Network mask in CIDR format.</span></span> <span data-ttu-id="a6ec6-116">在本文案例中為 *16*。</span><span class="sxs-lookup"><span data-stu-id="a6ec6-116">For our scenario, *16*.</span></span>
   * <span data-ttu-id="a6ec6-117">**-n (或 --subnet-name**)。</span><span class="sxs-lookup"><span data-stu-id="a6ec6-117">**-n (or --subnet-name**).</span></span> <span data-ttu-id="a6ec6-118">Hello 第一個子網路的名稱。</span><span class="sxs-lookup"><span data-stu-id="a6ec6-118">Name of hello first subnet.</span></span> <span data-ttu-id="a6ec6-119">在本文案例中為 *FrontEnd*。</span><span class="sxs-lookup"><span data-stu-id="a6ec6-119">For our scenario, *FrontEnd*.</span></span>
   * <span data-ttu-id="a6ec6-120">**-p (或 --subnet-start-ip)**。</span><span class="sxs-lookup"><span data-stu-id="a6ec6-120">**-p (or --subnet-start-ip)**.</span></span> <span data-ttu-id="a6ec6-121">子網路的起始 IP 位址或子網路位址空間。</span><span class="sxs-lookup"><span data-stu-id="a6ec6-121">Starting IP address for subnet, or subnet address space.</span></span> <span data-ttu-id="a6ec6-122">在本文案例中為 *192.168.1.0*。</span><span class="sxs-lookup"><span data-stu-id="a6ec6-122">For our scenario, *192.168.1.0*.</span></span>
   * <span data-ttu-id="a6ec6-123">**-r (或 --subnet-cidr)**。</span><span class="sxs-lookup"><span data-stu-id="a6ec6-123">**-r (or --subnet-cidr)**.</span></span> <span data-ttu-id="a6ec6-124">CIDR 格式的子網路網路遮罩。</span><span class="sxs-lookup"><span data-stu-id="a6ec6-124">Network mask in CIDR format for subnet.</span></span> <span data-ttu-id="a6ec6-125">在本文案例中為 *24*。</span><span class="sxs-lookup"><span data-stu-id="a6ec6-125">For our scenario, *24*.</span></span>
   * <span data-ttu-id="a6ec6-126">**-l (或 --location)**。</span><span class="sxs-lookup"><span data-stu-id="a6ec6-126">**-l (or --location)**.</span></span> <span data-ttu-id="a6ec6-127">將會建立 hello VNet 的 azure 區域。</span><span class="sxs-lookup"><span data-stu-id="a6ec6-127">Azure region where hello VNet will be created.</span></span> <span data-ttu-id="a6ec6-128">在本文案例中為「美國中部」 。</span><span class="sxs-lookup"><span data-stu-id="a6ec6-128">For our scenario, *Central US*.</span></span>
3. <span data-ttu-id="a6ec6-129">執行 hello **azure 網路 vnet 子網路建立**命令 toocreate 如下所示的子網路。</span><span class="sxs-lookup"><span data-stu-id="a6ec6-129">Run hello **azure network vnet subnet create** command toocreate a subnet as shown below.</span></span> <span data-ttu-id="a6ec6-130">之後再 hello 輸出所示的 hello 清單說明使用 hello 參數。</span><span class="sxs-lookup"><span data-stu-id="a6ec6-130">hello list shown after hello output explains hello parameters used.</span></span>
   
            azure network vnet subnet create -t TestVNet -n BackEnd -a 192.168.2.0/24
   
    <span data-ttu-id="a6ec6-131">以下是 hello 上述命令中的 hello 預期輸出：</span><span class="sxs-lookup"><span data-stu-id="a6ec6-131">Here is hello expected output for hello command above:</span></span>
   
            info:    Executing command network vnet subnet create
            + Looking up network configuration
            + Creating subnet "BackEnd"
            + Setting network configuration
            + Looking up hello subnet "BackEnd"
            + Looking up network configuration
            data:    Name                            : BackEnd
            data:    Address prefix                  : 192.168.2.0/24
            info:    network vnet subnet create command OK
   
   * <span data-ttu-id="a6ec6-132">**-t (或 --vnet-name)**。</span><span class="sxs-lookup"><span data-stu-id="a6ec6-132">**-t (or --vnet-name**.</span></span> <span data-ttu-id="a6ec6-133">Hello hello 子網路將會建立的 VNet 的名稱。</span><span class="sxs-lookup"><span data-stu-id="a6ec6-133">Name of hello VNet where hello subnet will be created.</span></span> <span data-ttu-id="a6ec6-134">在本文案例中為 *TestVNet*。</span><span class="sxs-lookup"><span data-stu-id="a6ec6-134">For our scenario, *TestVNet*.</span></span>
   * <span data-ttu-id="a6ec6-135">**-n (or --name)**。</span><span class="sxs-lookup"><span data-stu-id="a6ec6-135">**-n (or --name)**.</span></span> <span data-ttu-id="a6ec6-136">Hello 新的子網路的名稱。</span><span class="sxs-lookup"><span data-stu-id="a6ec6-136">Name of hello new subnet.</span></span> <span data-ttu-id="a6ec6-137">在本文案例中為 *BackEnd*。</span><span class="sxs-lookup"><span data-stu-id="a6ec6-137">For our scenario, *BackEnd*.</span></span>
   * <span data-ttu-id="a6ec6-138">**-a (或 --address-prefix)**。</span><span class="sxs-lookup"><span data-stu-id="a6ec6-138">**-a (or --address-prefix)**.</span></span> <span data-ttu-id="a6ec6-139">子網路 CIDR 區塊。</span><span class="sxs-lookup"><span data-stu-id="a6ec6-139">Subnet CIDR block.</span></span> <span data-ttu-id="a6ec6-140">在本文案例中為 *192.168.2.0/24*。</span><span class="sxs-lookup"><span data-stu-id="a6ec6-140">Four our scenario, *192.168.2.0/24*.</span></span>
4. <span data-ttu-id="a6ec6-141">執行 hello **azure 網路 vnet 顯示**命令 hello 新的 vnet tooview hello 屬性，如下所示。</span><span class="sxs-lookup"><span data-stu-id="a6ec6-141">Run hello **azure network vnet show** command tooview hello properties of hello new vnet, as shown below.</span></span>
   
            azure network vnet show
   
    <span data-ttu-id="a6ec6-142">以下是 hello 上述命令中的 hello 預期輸出：</span><span class="sxs-lookup"><span data-stu-id="a6ec6-142">Here is hello expected output for hello command above:</span></span>
   
            info:    Executing command network vnet show
            Virtual network name: TestVNet
            + Looking up hello virtual network sites
            data:    Name                            : TestVNet
            data:    Location                        : Central US
            data:    State                           : Created
            data:    Address space                   : 192.168.0.0/16
            data:    Subnets:
            data:      Name                          : FrontEnd
            data:      Address prefix                : 192.168.1.0/24
            data:
            data:      Name                          : BackEnd
            data:      Address prefix                : 192.168.2.0/24
            data:
            info:    network vnet show command OK

