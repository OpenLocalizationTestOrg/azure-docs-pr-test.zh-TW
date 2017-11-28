<span data-ttu-id="8817e-101">在此步驟中，您會在容錯移轉叢集管理員和 SQL Server Management Studio 中手動建立可用性群組接聽程式。</span><span class="sxs-lookup"><span data-stu-id="8817e-101">In this step, you manually create the availability group listener in Failover Cluster Manager and SQL Server Management Studio.</span></span>

1. <span data-ttu-id="8817e-102">從裝載主要複本的節點開啟容錯移轉叢集管理員。</span><span class="sxs-lookup"><span data-stu-id="8817e-102">Open Failover Cluster Manager from the node that hosts the primary replica.</span></span>

2. <span data-ttu-id="8817e-103">選取 [網路] 節點，然後記下叢集網路名稱。</span><span class="sxs-lookup"><span data-stu-id="8817e-103">Select the **Networks** node, and then note the cluster network name.</span></span> <span data-ttu-id="8817e-104">這個名稱會用於 PowerShell 指令碼中的 $ClusterNetworkName 變數。</span><span class="sxs-lookup"><span data-stu-id="8817e-104">This name is used in the $ClusterNetworkName variable in the PowerShell script.</span></span>

3. <span data-ttu-id="8817e-105">展開叢集名稱，然後按一下 [角色] 。</span><span class="sxs-lookup"><span data-stu-id="8817e-105">Expand the cluster name, and then click **Roles**.</span></span>

4. <span data-ttu-id="8817e-106">在 [角色] 窗格中，以滑鼠右鍵按一下可用性群組名稱，然後選取 [新增資源] > [用戶端存取點]。</span><span class="sxs-lookup"><span data-stu-id="8817e-106">In the **Roles** pane, right-click the availability group name, and then select **Add Resource** > **Client Access Point**.</span></span>
   
    ![新增可用性群組的用戶端存取點](./media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678769.gif)

5. <span data-ttu-id="8817e-108">在 [名稱] 方塊中，建立這個新接聽程式的名稱，按兩次 [下一步]，然後按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="8817e-108">In the **Name** box, create a name for this new listener, click **Next** twice, and then click **Finish**.</span></span>  
    <span data-ttu-id="8817e-109">目前請勿讓接聽程式或資源上線工作。</span><span class="sxs-lookup"><span data-stu-id="8817e-109">Do not bring the listener or resource online at this point.</span></span>

6. <span data-ttu-id="8817e-110">按一下 [資源] 索引標籤，然後展開您剛才建立的用戶端存取點。</span><span class="sxs-lookup"><span data-stu-id="8817e-110">Click the **Resources** tab, and then expand the client access point you just created.</span></span> 
    <span data-ttu-id="8817e-111">叢集中每個叢集網路的 IP 位址資源會顯示出來。</span><span class="sxs-lookup"><span data-stu-id="8817e-111">The IP address resource for each cluster network in your cluster is displayed.</span></span> <span data-ttu-id="8817e-112">如果這是僅限 Azure 的解決方案，只會顯示一個 IP 位址資源。</span><span class="sxs-lookup"><span data-stu-id="8817e-112">If this is an Azure-only solution, only one IP address resource is displayed.</span></span>

7. <span data-ttu-id="8817e-113">執行下列其中一個動作：</span><span class="sxs-lookup"><span data-stu-id="8817e-113">Do either of the following:</span></span>
   
   * <span data-ttu-id="8817e-114">若要設定混合式解決方案：</span><span class="sxs-lookup"><span data-stu-id="8817e-114">To configure a hybrid solution:</span></span>
     
        <span data-ttu-id="8817e-115">a.</span><span class="sxs-lookup"><span data-stu-id="8817e-115">a.</span></span> <span data-ttu-id="8817e-116">以滑鼠右鍵按一下對應至您內部部署子網路的 IP 位址資源，然後選取 [屬性]。</span><span class="sxs-lookup"><span data-stu-id="8817e-116">Right-click the IP address resource that corresponds to your on-premises subnet, and then select **Properties**.</span></span> <span data-ttu-id="8817e-117">記下 IP 位址名稱和網路名稱。</span><span class="sxs-lookup"><span data-stu-id="8817e-117">Note the IP address name and network name.</span></span>
   
        <span data-ttu-id="8817e-118">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="8817e-118">b.</span></span> <span data-ttu-id="8817e-119">選取 [靜態 IP 位址]、指派未使用的 IP 位址，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="8817e-119">Select **Static IP Address**, assign an unused IP address, and then click **OK**.</span></span>
 
   * <span data-ttu-id="8817e-120">若要設定僅限 Azure 的解決方案︰</span><span class="sxs-lookup"><span data-stu-id="8817e-120">To configure an Azure-only solution:</span></span>

        <span data-ttu-id="8817e-121">a.</span><span class="sxs-lookup"><span data-stu-id="8817e-121">a.</span></span> <span data-ttu-id="8817e-122">以滑鼠右鍵按一下對應至您 Azure 子網路的 IP 位址資源，然後選取 [屬性]。</span><span class="sxs-lookup"><span data-stu-id="8817e-122">Right-click the IP address resource that corresponds to your Azure subnet, and then select **Properties**.</span></span>
       
       > [!NOTE]
       > <span data-ttu-id="8817e-123">如果接聽程式稍後因為 DHCP 所選取的 IP 位址衝突而無法上線，您可以在此屬性視窗中設定有效的靜態 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="8817e-123">If the listener later fails to come online because of a conflicting IP address selected by DHCP, you can configure a valid static IP address in this properties window.</span></span>
       > 
       > 

       <span data-ttu-id="8817e-124">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="8817e-124">b.</span></span> <span data-ttu-id="8817e-125">在同一個 [IP 位址屬性] 視窗中，變更 [IP 位址名稱]。</span><span class="sxs-lookup"><span data-stu-id="8817e-125">In the same **IP Address** properties window, change the **IP Address Name**.</span></span>  
        <span data-ttu-id="8817e-126">此名稱使用於 PowerShell 指令碼的 $IPResourceName 變數。</span><span class="sxs-lookup"><span data-stu-id="8817e-126">This name is used in the $IPResourceName variable of the PowerShell script.</span></span> <span data-ttu-id="8817e-127">如果您的解決方案跨越多個 Azure 虛擬網路，請針對每個 IP 資源重複此步驟。</span><span class="sxs-lookup"><span data-stu-id="8817e-127">If your solution spans multiple Azure virtual networks, repeat this step for each IP resource.</span></span>

