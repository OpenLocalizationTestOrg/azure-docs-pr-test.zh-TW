<span data-ttu-id="3a450-101">toocreate hello Resource Manager 部署模型使用 hello Azure 入口網站中的 VNet，請遵循下列 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="3a450-101">toocreate a VNet in hello Resource Manager deployment model by using hello Azure portal, follow hello steps below.</span></span> <span data-ttu-id="3a450-102">hello 螢幕擷取畫面會提供範例。</span><span class="sxs-lookup"><span data-stu-id="3a450-102">hello screenshots are provided as examples.</span></span> <span data-ttu-id="3a450-103">是以您自己的確定 tooreplace hello 值。</span><span class="sxs-lookup"><span data-stu-id="3a450-103">Be sure tooreplace hello values with your own.</span></span> <span data-ttu-id="3a450-104">如需有關使用虛擬網路的詳細資訊，請參閱 hello[虛擬網路概觀](../articles/virtual-network/virtual-networks-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="3a450-104">For more information about working with virtual networks, see hello [Virtual Network Overview](../articles/virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="3a450-105">從瀏覽器中，瀏覽 toohello [Azure 入口網站](http://portal.azure.com)且如有需要，使用您的 Azure 帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="3a450-105">From a browser, navigate toohello [Azure portal](http://portal.azure.com) and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="3a450-106">按一下頁面底部的 [新增] **+**來單一登入應用程式。</span><span class="sxs-lookup"><span data-stu-id="3a450-106">Click **+**.</span></span> <span data-ttu-id="3a450-107">在 hello**搜尋 hello marketplace**欄位中，輸入 「 虛擬網路 」。</span><span class="sxs-lookup"><span data-stu-id="3a450-107">In hello **Search hello marketplace** field, type "Virtual Network".</span></span> <span data-ttu-id="3a450-108">找出**虛擬網路**hello 傳回從清單中，按一下 tooopen hello**虛擬網路**頁面。</span><span class="sxs-lookup"><span data-stu-id="3a450-108">Locate **Virtual Network** from hello returned list and click tooopen hello **Virtual Network** page.</span></span>

  <span data-ttu-id="3a450-109">![找出虛擬網路資源頁面](./media/vpn-gateway-basic-p2s-vnet-rm-portal-include/newvnetportal700.png "找出虛擬網路資源頁面")</span><span class="sxs-lookup"><span data-stu-id="3a450-109">![Locate Virtual Network resource page](./media/vpn-gateway-basic-p2s-vnet-rm-portal-include/newvnetportal700.png "Locate virtual network resource page")</span></span>
3. <span data-ttu-id="3a450-110">Hello hello 虛擬網路 頁面上，從 hello 底端附近**選取部署模型**清單中，選取**資源管理員**，然後按一下**建立**。</span><span class="sxs-lookup"><span data-stu-id="3a450-110">Near hello bottom of hello Virtual Network page, from hello **Select a deployment model** list, select **Resource Manager**, and then click **Create**.</span></span>

  <span data-ttu-id="3a450-111">![選取資源管理員](./media/vpn-gateway-basic-p2s-vnet-rm-portal-include/resourcemanager250.png "選取資源管理員")</span><span class="sxs-lookup"><span data-stu-id="3a450-111">![Select Resource Manager](./media/vpn-gateway-basic-p2s-vnet-rm-portal-include/resourcemanager250.png "Select Resource Manager")</span></span>
4. <span data-ttu-id="3a450-112">在 hello**建立虛擬網路**頁面上，設定 hello VNet 設定。</span><span class="sxs-lookup"><span data-stu-id="3a450-112">On hello **Create virtual network** page, configure hello VNet settings.</span></span> <span data-ttu-id="3a450-113">當您填滿 hello 欄位中時，hello 紅色驚嘆號會變成綠色的核取記號時 hello hello 欄位中輸入的字元都有效。</span><span class="sxs-lookup"><span data-stu-id="3a450-113">When you fill in hello fields, hello red exclamation mark becomes a green check mark when hello characters entered in hello field are valid.</span></span> <span data-ttu-id="3a450-114">有些值可能會自動填入。</span><span class="sxs-lookup"><span data-stu-id="3a450-114">There may be values that are auto-filled.</span></span> <span data-ttu-id="3a450-115">如果是這樣，hello 值取代您自己。</span><span class="sxs-lookup"><span data-stu-id="3a450-115">If so, replace hello values with your own.</span></span> <span data-ttu-id="3a450-116">hello**建立虛擬網路**頁面看起來類似下列範例的 toohello:</span><span class="sxs-lookup"><span data-stu-id="3a450-116">hello **Create virtual network** page looks similar toohello following example:</span></span>

  <span data-ttu-id="3a450-117">![欄位驗證](./media/vpn-gateway-basic-p2s-vnet-rm-portal-include/createp2sgvnet.png "欄位驗證")</span><span class="sxs-lookup"><span data-stu-id="3a450-117">![Field validation](./media/vpn-gateway-basic-p2s-vnet-rm-portal-include/createp2sgvnet.png "Field validation")</span></span>
5. <span data-ttu-id="3a450-118">**名稱**： 輸入您的虛擬網路的 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="3a450-118">**Name**: Enter hello name for your Virtual Network.</span></span>
6. <span data-ttu-id="3a450-119">**位址空間**： 輸入 hello 位址空間。</span><span class="sxs-lookup"><span data-stu-id="3a450-119">**Address space**: Enter hello address space.</span></span> <span data-ttu-id="3a450-120">如果您有多個位址空間 tooadd，加入您的第一個位址空間。</span><span class="sxs-lookup"><span data-stu-id="3a450-120">If you have multiple address spaces tooadd, add your first address space.</span></span> <span data-ttu-id="3a450-121">您可以建立 hello VNet 後的更新版本中，加入其他位址空間。</span><span class="sxs-lookup"><span data-stu-id="3a450-121">You can add additional address spaces later, after creating hello VNet.</span></span>
7. <span data-ttu-id="3a450-122">**子網路名稱**： 新增 hello 子網路名稱和子網路位址範圍。</span><span class="sxs-lookup"><span data-stu-id="3a450-122">**Subnet name**: Add hello subnet name and subnet address range.</span></span> <span data-ttu-id="3a450-123">您可以建立 hello VNet 後的更新版本中，新增其他子網路。</span><span class="sxs-lookup"><span data-stu-id="3a450-123">You can add additional subnets later, after creating hello VNet.</span></span>
8. <span data-ttu-id="3a450-124">**訂用帳戶**： 確認該訂用帳戶所列的 hello 是 hello 正確。</span><span class="sxs-lookup"><span data-stu-id="3a450-124">**Subscription**: Verify that hello Subscription listed is hello correct one.</span></span> <span data-ttu-id="3a450-125">您可以使用 [hello] 下拉式清單來變更訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="3a450-125">You can change subscriptions by using hello drop-down.</span></span>
9. <span data-ttu-id="3a450-126">**資源群組**：選取現有資源群組，或輸入新資源群組的名稱以建立新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="3a450-126">**Resource group**: Select an existing resource group, or create a new one by typing a name for your new resource group.</span></span> <span data-ttu-id="3a450-127">如果您要建立新的群組，根據 tooyour 名稱 hello 資源群組已規劃的組態值。</span><span class="sxs-lookup"><span data-stu-id="3a450-127">If you are creating a new group, name hello resource group according tooyour planned configuration values.</span></span> <span data-ttu-id="3a450-128">如需資源群組的詳細資訊，請瀏覽 [Azure Resource Manager 概觀](../articles/azure-resource-manager/resource-group-overview.md#resource-groups)。</span><span class="sxs-lookup"><span data-stu-id="3a450-128">For more information about resource groups, visit [Azure Resource Manager Overview](../articles/azure-resource-manager/resource-group-overview.md#resource-groups).</span></span>
10. <span data-ttu-id="3a450-129">**位置**： 選取您的 VNet 的 hello 位置。</span><span class="sxs-lookup"><span data-stu-id="3a450-129">**Location**: Select hello location for your VNet.</span></span> <span data-ttu-id="3a450-130">hello 位置會決定您將部署 toothis VNet hello 資源所在的位置。</span><span class="sxs-lookup"><span data-stu-id="3a450-130">hello location determines where hello resources that you deploy toothis VNet will reside.</span></span>
11. <span data-ttu-id="3a450-131">選取**Pin toodashboard**如果您想 toobe 無法 toofind 輕鬆 hello 儀表板上，您的 VNet，然後按一下**建立**。</span><span class="sxs-lookup"><span data-stu-id="3a450-131">Select **Pin toodashboard** if you want toobe able toofind your VNet easily on hello dashboard, and then click **Create**.</span></span>

 <span data-ttu-id="3a450-132">![Pin toodashboard](./media/vpn-gateway-basic-p2s-vnet-rm-portal-include/pintodashboard150.png "pin toodashboard")</span><span class="sxs-lookup"><span data-stu-id="3a450-132">![Pin toodashboard](./media/vpn-gateway-basic-p2s-vnet-rm-portal-include/pintodashboard150.png "pin toodashboard")</span></span>
12. <span data-ttu-id="3a450-133">按一下後**建立**，您會看到磚儀表板上，將會反映您的 VNet hello 進度。</span><span class="sxs-lookup"><span data-stu-id="3a450-133">After clicking **Create**, you will see a tile on your dashboard that will reflect hello progress of your VNet.</span></span> <span data-ttu-id="3a450-134">hello hello 磚變更正在建立 VNet。</span><span class="sxs-lookup"><span data-stu-id="3a450-134">hello tile changes as hello VNet is being created.</span></span>

  <span data-ttu-id="3a450-135">![建立虛擬網路圖格](./media/vpn-gateway-basic-p2s-vnet-rm-portal-include/deploying150.png "建立虛擬網路圖格")</span><span class="sxs-lookup"><span data-stu-id="3a450-135">![Creating virtual network tile](./media/vpn-gateway-basic-p2s-vnet-rm-portal-include/deploying150.png "Creating virtual network tile")</span></span>