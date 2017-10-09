## <a name="how-toocreate-a-classic-vnet-in-hello-azure-portal"></a><span data-ttu-id="326a6-101">如何 toocreate hello Azure 入口網站中的傳統 VNet</span><span class="sxs-lookup"><span data-stu-id="326a6-101">How toocreate a classic VNet in hello Azure portal</span></span>
<span data-ttu-id="326a6-102">toocreate 傳統 VNet 根據 hello 案例以上版本，請遵循下列 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="326a6-102">toocreate a classic VNet based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="326a6-103">從瀏覽器，瀏覽 toohttp://portal.azure.com，並視需要登入您的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="326a6-103">From a browser, navigate toohttp://portal.azure.com and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="326a6-104">按一下**新增** > **網路** > **虛擬網路**，請注意該 hello**選取部署模型**列出已顯示**傳統**，然後按一下**建立**、 hello 圖所示。</span><span class="sxs-lookup"><span data-stu-id="326a6-104">Click **NEW** > **Networking** > **Virtual network**, notice that hello **Select a deployment model** list already shows **Classic**, and then click **Create**, as seen in hello figure below.</span></span>
   
    ![在 Azure 入口網站中建立 VNet](./media/virtual-networks-create-vnet-classic-pportal-include/vnet-create-pportal-figure1.gif)
3. <span data-ttu-id="326a6-106">在 hello**虛擬網路**刀鋒視窗中，型別 hello**名稱**hello VNet，然後再按一下**位址空間**。</span><span class="sxs-lookup"><span data-stu-id="326a6-106">On hello **Virtual network** blade, type hello **Name** of hello VNet, and then click **Address space**.</span></span> <span data-ttu-id="326a6-107">設定 hello VNet 和其第一個子網路的位址空間設定，然後按一下 **確定**。</span><span class="sxs-lookup"><span data-stu-id="326a6-107">Configure your address space settings for hello VNet and its first subnet, then click **OK**.</span></span> <span data-ttu-id="326a6-108">hello 下圖顯示我們的案例中的 hello CIDR 區塊設定。</span><span class="sxs-lookup"><span data-stu-id="326a6-108">hello figure below shows hello CIDR block settings for our scenario.</span></span>
   
    ![位址空間刀鋒視窗](./media/virtual-networks-create-vnet-classic-pportal-include/vnet-create-pportal-figure2.png)
4. <span data-ttu-id="326a6-110">按一下**資源群組**，然後選取資源群組 tooadd hello VNet，或按一下**建立新的資源群組**tooadd hello VNet tooa 新資源群組。</span><span class="sxs-lookup"><span data-stu-id="326a6-110">Click **Resource Group** and select a resource group tooadd hello VNet to, or click **Create new resource group** tooadd hello VNet tooa new resource group.</span></span> <span data-ttu-id="326a6-111">hello 下圖顯示 hello 資源群組設定新的資源群組，稱為**TestRG**。</span><span class="sxs-lookup"><span data-stu-id="326a6-111">hello figure below shows hello resource group settings for a new resource group called **TestRG**.</span></span> <span data-ttu-id="326a6-112">如需資源群組的詳細資訊，請瀏覽 [Azure Resource Manager 概觀](../articles/azure-resource-manager/resource-group-overview.md#resource-groups)。</span><span class="sxs-lookup"><span data-stu-id="326a6-112">For more information about resource groups, visit [Azure Resource Manager Overview](../articles/azure-resource-manager/resource-group-overview.md#resource-groups).</span></span>
   
    ![建立資源群組刀鋒視窗](./media/virtual-networks-create-vnet-classic-pportal-include/vnet-create-pportal-figure3.png)
5. <span data-ttu-id="326a6-114">如有必要，變更 hello**訂用帳戶**和**位置**設定您的 VNet。</span><span class="sxs-lookup"><span data-stu-id="326a6-114">If necessary, change hello **Subscription** and **Location** settings for your VNet.</span></span> 
6. <span data-ttu-id="326a6-115">如果您不想 toosee hello VNet 當做一個磚中 hello**開始面板**，停用**Pin tooStartboard**。</span><span class="sxs-lookup"><span data-stu-id="326a6-115">If you do not want toosee hello VNet as a tile in hello **Startboard**, disable **Pin tooStartboard**.</span></span> 
7. <span data-ttu-id="326a6-116">按一下**建立**和名為注意事項 hello 磚**建立虛擬網路**hello 圖所示。</span><span class="sxs-lookup"><span data-stu-id="326a6-116">Click **Create** and notice hello tile named **Creating Virtual network** as shown in hello figure below.</span></span>
   
    ![在入口網站中建立 VNet](./media/virtual-networks-create-vnet-classic-pportal-include/vnet-create-pportal-figure4.png)
8. <span data-ttu-id="326a6-118">稍候 hello VNet toobe 建立，然後當您看到磚下方，按一下它 tooadd hello 更多子網路。</span><span class="sxs-lookup"><span data-stu-id="326a6-118">Wait for hello VNet toobe created, and when you see hello tile below, click it tooadd more subnets.</span></span>
   
    ![在入口網站中建立 VNet](./media/virtual-networks-create-vnet-classic-pportal-include/vnet-create-pportal-figure5.png)
9. <span data-ttu-id="326a6-120">您應該會看見 hello**組態**為您的 VNet，如下所示。</span><span class="sxs-lookup"><span data-stu-id="326a6-120">You should see hello **Configuration** for your VNet as shown below.</span></span> 
   
    ![在入口網站中建立 VNet](./media/virtual-networks-create-vnet-classic-pportal-include/vnet-create-pportal-figure6.png)
10. <span data-ttu-id="326a6-122">依序按一下 子網路  >  新增，然後鍵入 名稱，並指定您子網路的 位址範圍 (CIDR 區塊)，然後按一下確定。</span><span class="sxs-lookup"><span data-stu-id="326a6-122">Click **Subnets** > **Add**, then type a **Name** and specify an **Address range (CIDR block)** for your subnet, and then click **OK**.</span></span> <span data-ttu-id="326a6-123">hello 下圖顯示我們目前的案例中的 hello 設定。</span><span class="sxs-lookup"><span data-stu-id="326a6-123">hello figure below shows hello settings for our current scenario.</span></span>
    
    ![在 Azure 入口網站中建立 VNet](./media/virtual-networks-create-vnet-classic-pportal-include/vnet-create-pportal-figure7.gif)

