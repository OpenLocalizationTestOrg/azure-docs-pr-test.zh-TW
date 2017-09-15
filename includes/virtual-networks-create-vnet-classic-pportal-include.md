## <a name="how-to-create-a-classic-vnet-in-the-azure-portal"></a><span data-ttu-id="361eb-101">如何在 Azure 入口網站中建立傳統 VNet</span><span class="sxs-lookup"><span data-stu-id="361eb-101">How to create a classic VNet in the Azure portal</span></span>
<span data-ttu-id="361eb-102">若要根據上述案例建立傳統 VNet，請依照下列步驟執行。</span><span class="sxs-lookup"><span data-stu-id="361eb-102">To create a classic VNet based on the scenario above, follow the steps below.</span></span>

1. <span data-ttu-id="361eb-103">透過瀏覽器瀏覽至 http://portal.azure.com，並視需要使用您的 Azure 帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="361eb-103">From a browser, navigate to http://portal.azure.com and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="361eb-104">依序按一下 [新增]  >  [網路]  >  [虛擬網路]，注意 [選取部署模型] 清單是否已經顯示為 [傳統]，然後再按一下 [建立]，如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="361eb-104">Click **NEW** > **Networking** > **Virtual network**, notice that the **Select a deployment model** list already shows **Classic**, and then click **Create**, as seen in the figure below.</span></span>
   
    ![在 Azure 入口網站中建立 VNet](./media/virtual-networks-create-vnet-classic-pportal-include/vnet-create-pportal-figure1.gif)
3. <span data-ttu-id="361eb-106">在 [虛擬網路] 刀鋒視窗上，鍵入 VNet 的**名稱**，然後再按一下 [位址空間]。</span><span class="sxs-lookup"><span data-stu-id="361eb-106">On the **Virtual network** blade, type the **Name** of the VNet, and then click **Address space**.</span></span> <span data-ttu-id="361eb-107">設定 VNet 和其第一個子網路的位址空間設定，然後按一下 [ **確定**]。</span><span class="sxs-lookup"><span data-stu-id="361eb-107">Configure your address space settings for the VNet and its first subnet, then click **OK**.</span></span> <span data-ttu-id="361eb-108">下圖顯示我們案例的 CIDR 區塊設定。</span><span class="sxs-lookup"><span data-stu-id="361eb-108">The figure below shows the CIDR block settings for our scenario.</span></span>
   
    ![位址空間刀鋒視窗](./media/virtual-networks-create-vnet-classic-pportal-include/vnet-create-pportal-figure2.png)
4. <span data-ttu-id="361eb-110">按一下 [資源群組]，選取要新增 VNet 的資源群組，或按一下 [建立新的資源群組]，將 VNet 新增到新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="361eb-110">Click **Resource Group** and select a resource group to add the VNet to, or click **Create new resource group** to add the VNet to a new resource group.</span></span> <span data-ttu-id="361eb-111">下圖顯示新資源群組 **TestRG**的資源群組設定 。</span><span class="sxs-lookup"><span data-stu-id="361eb-111">The figure below shows the resource group settings for a new resource group called **TestRG**.</span></span> <span data-ttu-id="361eb-112">如需資源群組的詳細資訊，請造訪 [Azure 資源管理員概觀](../articles/azure-resource-manager/resource-group-overview.md#resource-groups)。</span><span class="sxs-lookup"><span data-stu-id="361eb-112">For more information about resource groups, visit [Azure Resource Manager Overview](../articles/azure-resource-manager/resource-group-overview.md#resource-groups).</span></span>
   
    ![建立資源群組刀鋒視窗](./media/virtual-networks-create-vnet-classic-pportal-include/vnet-create-pportal-figure3.png)
5. <span data-ttu-id="361eb-114">如有必要，變更 VNet 的**訂用帳戶**和**位置**設定。</span><span class="sxs-lookup"><span data-stu-id="361eb-114">If necessary, change the **Subscription** and **Location** settings for your VNet.</span></span> 
6. <span data-ttu-id="361eb-115">如果您不想在**「開始面板」**上看到 VNet 圖格，請停用 [釘選到「開始面板」]。</span><span class="sxs-lookup"><span data-stu-id="361eb-115">If you do not want to see the VNet as a tile in the **Startboard**, disable **Pin to Startboard**.</span></span> 
7. <span data-ttu-id="361eb-116">按一下 [建立]，並注意名為 [建立虛擬網路] 的圖格，如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="361eb-116">Click **Create** and notice the tile named **Creating Virtual network** as shown in the figure below.</span></span>
   
    ![在入口網站中建立 VNet](./media/virtual-networks-create-vnet-classic-pportal-include/vnet-create-pportal-figure4.png)
8. <span data-ttu-id="361eb-118">等候建立 VNet，然後在看到下方的磚之後，按一下以新增更多子網路。</span><span class="sxs-lookup"><span data-stu-id="361eb-118">Wait for the VNet to be created, and when you see the tile below, click it to add more subnets.</span></span>
   
    ![在入口網站中建立 VNet](./media/virtual-networks-create-vnet-classic-pportal-include/vnet-create-pportal-figure5.png)
9. <span data-ttu-id="361eb-120">您應該會看到 VNet 的 [ **組態** ]，如下所示。</span><span class="sxs-lookup"><span data-stu-id="361eb-120">You should see the **Configuration** for your VNet as shown below.</span></span> 
   
    ![在入口網站中建立 VNet](./media/virtual-networks-create-vnet-classic-pportal-include/vnet-create-pportal-figure6.png)
10. <span data-ttu-id="361eb-122">依序按一下 [子網路]  >  [新增]，然後鍵入 [名稱]，並指定您子網路的 [位址範圍 (CIDR 區塊)]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="361eb-122">Click **Subnets** > **Add**, then type a **Name** and specify an **Address range (CIDR block)** for your subnet, and then click **OK**.</span></span> <span data-ttu-id="361eb-123">下圖顯示我們目前案例的設定。</span><span class="sxs-lookup"><span data-stu-id="361eb-123">The figure below shows the settings for our current scenario.</span></span>
    
    ![在 Azure 入口網站中建立 VNet](./media/virtual-networks-create-vnet-classic-pportal-include/vnet-create-pportal-figure7.gif)

