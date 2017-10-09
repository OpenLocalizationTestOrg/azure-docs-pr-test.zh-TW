<span data-ttu-id="0baed-101">在此步驟中，您可以手動建立容錯移轉叢集管理員和 SQL Server Management Studio 中的 hello 可用性群組接聽程式。</span><span class="sxs-lookup"><span data-stu-id="0baed-101">In this step, you manually create hello availability group listener in Failover Cluster Manager and SQL Server Management Studio.</span></span>

1. <span data-ttu-id="0baed-102">開啟 容錯移轉叢集管理員從裝載主要複本的 hello hello 節點。</span><span class="sxs-lookup"><span data-stu-id="0baed-102">Open Failover Cluster Manager from hello node that hosts hello primary replica.</span></span>

2. <span data-ttu-id="0baed-103">選取 hello**網路**節點，然後注意 hello 叢集網路名稱。</span><span class="sxs-lookup"><span data-stu-id="0baed-103">Select hello **Networks** node, and then note hello cluster network name.</span></span> <span data-ttu-id="0baed-104">Hello PowerShell 指令碼中的 hello $ClusterNetworkName 變數中，會使用此名稱。</span><span class="sxs-lookup"><span data-stu-id="0baed-104">This name is used in hello $ClusterNetworkName variable in hello PowerShell script.</span></span>

3. <span data-ttu-id="0baed-105">展開 hello 叢集名稱，然後按一下**角色**。</span><span class="sxs-lookup"><span data-stu-id="0baed-105">Expand hello cluster name, and then click **Roles**.</span></span>

4. <span data-ttu-id="0baed-106">在 hello**角色**窗格中，以滑鼠右鍵按一下 hello 可用性群組名稱，然後再選取**加入資源** > **用戶端存取點**。</span><span class="sxs-lookup"><span data-stu-id="0baed-106">In hello **Roles** pane, right-click hello availability group name, and then select **Add Resource** > **Client Access Point**.</span></span>
   
    ![新增可用性群組的用戶端存取點](./media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678769.gif)

5. <span data-ttu-id="0baed-108">在 hello**名稱**，建立新的接聽程式的名稱，按一下**下一步**兩次，然後按一下**完成**。</span><span class="sxs-lookup"><span data-stu-id="0baed-108">In hello **Name** box, create a name for this new listener, click **Next** twice, and then click **Finish**.</span></span>  
    <span data-ttu-id="0baed-109">請勿讓 hello 接聽程式或資源上線此時。</span><span class="sxs-lookup"><span data-stu-id="0baed-109">Do not bring hello listener or resource online at this point.</span></span>

6. <span data-ttu-id="0baed-110">按一下 hello**資源**索引標籤，然後再展開您剛才建立的 hello 用戶端存取點。</span><span class="sxs-lookup"><span data-stu-id="0baed-110">Click hello **Resources** tab, and then expand hello client access point you just created.</span></span> 
    <span data-ttu-id="0baed-111">會顯示 hello 叢集中的每個叢集網路的 IP 位址資源。</span><span class="sxs-lookup"><span data-stu-id="0baed-111">hello IP address resource for each cluster network in your cluster is displayed.</span></span> <span data-ttu-id="0baed-112">如果這是僅限 Azure 的解決方案，只會顯示一個 IP 位址資源。</span><span class="sxs-lookup"><span data-stu-id="0baed-112">If this is an Azure-only solution, only one IP address resource is displayed.</span></span>

7. <span data-ttu-id="0baed-113">執行 hello 下列其中一項：</span><span class="sxs-lookup"><span data-stu-id="0baed-113">Do either of hello following:</span></span>
   
   * <span data-ttu-id="0baed-114">tooconfigure 混合式解決方案：</span><span class="sxs-lookup"><span data-stu-id="0baed-114">tooconfigure a hybrid solution:</span></span>
     
        <span data-ttu-id="0baed-115">a.</span><span class="sxs-lookup"><span data-stu-id="0baed-115">a.</span></span> <span data-ttu-id="0baed-116">以滑鼠右鍵按一下 hello 對應 tooyour 在內部部署子網路，IP 位址資源，然後選取**屬性**。</span><span class="sxs-lookup"><span data-stu-id="0baed-116">Right-click hello IP address resource that corresponds tooyour on-premises subnet, and then select **Properties**.</span></span> <span data-ttu-id="0baed-117">請注意 hello IP 位址名稱和網路名稱。</span><span class="sxs-lookup"><span data-stu-id="0baed-117">Note hello IP address name and network name.</span></span>
   
        <span data-ttu-id="0baed-118">b.</span><span class="sxs-lookup"><span data-stu-id="0baed-118">b.</span></span> <span data-ttu-id="0baed-119">選取 靜態 IP 位址、指派未使用的 IP 位址，然後按一下確定。</span><span class="sxs-lookup"><span data-stu-id="0baed-119">Select **Static IP Address**, assign an unused IP address, and then click **OK**.</span></span>
 
   * <span data-ttu-id="0baed-120">tooconfigure 僅 Azure 」 的方案：</span><span class="sxs-lookup"><span data-stu-id="0baed-120">tooconfigure an Azure-only solution:</span></span>

        <span data-ttu-id="0baed-121">a.</span><span class="sxs-lookup"><span data-stu-id="0baed-121">a.</span></span> <span data-ttu-id="0baed-122">以滑鼠右鍵按一下 hello 對應 tooyour Azure 子網路，IP 位址資源，然後選取**屬性**。</span><span class="sxs-lookup"><span data-stu-id="0baed-122">Right-click hello IP address resource that corresponds tooyour Azure subnet, and then select **Properties**.</span></span>
       
       > [!NOTE]
       > <span data-ttu-id="0baed-123">如果稍後 hello 接聽程式會因為衝突的 IP 位址，DHCP 所選取的失敗 toocome 線上，您可以設定此屬性 視窗中的有效靜態 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="0baed-123">If hello listener later fails toocome online because of a conflicting IP address selected by DHCP, you can configure a valid static IP address in this properties window.</span></span>
       > 
       > 

       <span data-ttu-id="0baed-124">b.</span><span class="sxs-lookup"><span data-stu-id="0baed-124">b.</span></span> <span data-ttu-id="0baed-125">在 hello 相同**IP 位址**屬性視窗中，變更 hello **IP 位址名稱**。</span><span class="sxs-lookup"><span data-stu-id="0baed-125">In hello same **IP Address** properties window, change hello **IP Address Name**.</span></span>  
        <span data-ttu-id="0baed-126">在 hello $IPResourceName 變數中的 hello PowerShell 指令碼會使用此名稱。</span><span class="sxs-lookup"><span data-stu-id="0baed-126">This name is used in hello $IPResourceName variable of hello PowerShell script.</span></span> <span data-ttu-id="0baed-127">如果您的解決方案跨越多個 Azure 虛擬網路，請針對每個 IP 資源重複此步驟。</span><span class="sxs-lookup"><span data-stu-id="0baed-127">If your solution spans multiple Azure virtual networks, repeat this step for each IP resource.</span></span>

