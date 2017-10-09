<span data-ttu-id="8226a-101">hello 可用性群組接聽程式是 hello SQL Server 可用性群組接聽的 IP 位址和網路名稱。</span><span class="sxs-lookup"><span data-stu-id="8226a-101">hello availability group listener is an IP address and network name that hello SQL Server availability group listens on.</span></span> <span data-ttu-id="8226a-102">toocreate hello 可用性群組接聽程式，請勿 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="8226a-102">toocreate hello availability group listener, do hello following:</span></span>

1. <span data-ttu-id="8226a-103"><a name="getnet"></a>收到 hello hello 叢集網路資源名稱。</span><span class="sxs-lookup"><span data-stu-id="8226a-103"><a name="getnet"></a>Get hello name of hello cluster network resource.</span></span>

    <span data-ttu-id="8226a-104">a.</span><span class="sxs-lookup"><span data-stu-id="8226a-104">a.</span></span> <span data-ttu-id="8226a-105">使用 RDP tooconnect toohello 裝載 hello 主要複本的 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="8226a-105">Use RDP tooconnect toohello Azure virtual machine that hosts hello primary replica.</span></span> 

    <span data-ttu-id="8226a-106">b.</span><span class="sxs-lookup"><span data-stu-id="8226a-106">b.</span></span> <span data-ttu-id="8226a-107">開始容錯移轉叢集管理員。</span><span class="sxs-lookup"><span data-stu-id="8226a-107">Open Failover Cluster Manager.</span></span>

    <span data-ttu-id="8226a-108">c.</span><span class="sxs-lookup"><span data-stu-id="8226a-108">c.</span></span> <span data-ttu-id="8226a-109">選取 hello**網路**節點，然後注意 hello 叢集網路名稱。</span><span class="sxs-lookup"><span data-stu-id="8226a-109">Select hello **Networks** node, and note hello cluster network name.</span></span> <span data-ttu-id="8226a-110">使用此名稱在 hello `$ClusterNetworkName` hello PowerShell 指令碼中的變數。</span><span class="sxs-lookup"><span data-stu-id="8226a-110">Use this name in hello `$ClusterNetworkName` variable in hello PowerShell script.</span></span> <span data-ttu-id="8226a-111">下列影像 hello 叢集網路名稱是在 hello**叢集網路 1**:</span><span class="sxs-lookup"><span data-stu-id="8226a-111">In hello following image hello cluster network name is **Cluster Network 1**:</span></span>

   ![叢集網路名稱](./media/virtual-machines-ag-listener-configure/90-clusternetworkname.png)

2. <span data-ttu-id="8226a-113"><a name="addcap"></a>加入 hello 用戶端存取點。</span><span class="sxs-lookup"><span data-stu-id="8226a-113"><a name="addcap"></a>Add hello client access point.</span></span>  
    <span data-ttu-id="8226a-114">hello 用戶端存取點是應用程式使用 tooconnect toohello 資料庫可用性群組中的 hello 網路名稱。</span><span class="sxs-lookup"><span data-stu-id="8226a-114">hello client access point is hello network name that applications use tooconnect toohello databases in an availability group.</span></span> <span data-ttu-id="8226a-115">在 [容錯移轉叢集管理員] 中建立 hello 用戶端存取點。</span><span class="sxs-lookup"><span data-stu-id="8226a-115">Create hello client access point in Failover Cluster Manager.</span></span>

    <span data-ttu-id="8226a-116">a.</span><span class="sxs-lookup"><span data-stu-id="8226a-116">a.</span></span> <span data-ttu-id="8226a-117">展開 hello 叢集名稱，然後按一下**角色**。</span><span class="sxs-lookup"><span data-stu-id="8226a-117">Expand hello cluster name, and then click **Roles**.</span></span>

    <span data-ttu-id="8226a-118">b.</span><span class="sxs-lookup"><span data-stu-id="8226a-118">b.</span></span> <span data-ttu-id="8226a-119">在 hello**角色**窗格中，以滑鼠右鍵按一下 hello 可用性群組名稱，然後再選取**加入資源** > **用戶端存取點**。</span><span class="sxs-lookup"><span data-stu-id="8226a-119">In hello **Roles** pane, right-click hello availability group name, and then select **Add Resource** > **Client Access Point**.</span></span>

   ![用戶端存取點](./media/virtual-machines-ag-listener-configure/92-addclientaccesspoint.png)

    <span data-ttu-id="8226a-121">c.</span><span class="sxs-lookup"><span data-stu-id="8226a-121">c.</span></span> <span data-ttu-id="8226a-122">在 hello**名稱**方塊中，建立新的接聽程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="8226a-122">In hello **Name** box, create a name for this new listener.</span></span> 
   <span data-ttu-id="8226a-123">hello hello 新的接聽程式名稱是應用程式使用 tooconnect toodatabases hello SQL Server 可用性群組中的 hello 網路名稱。</span><span class="sxs-lookup"><span data-stu-id="8226a-123">hello name for hello new listener is hello network name that applications use tooconnect toodatabases in hello SQL Server availability group.</span></span>
   
    <span data-ttu-id="8226a-124">d.</span><span class="sxs-lookup"><span data-stu-id="8226a-124">d.</span></span> <span data-ttu-id="8226a-125">toofinish 建立 hello 接聽程式，按一下**下一步**兩次，然後按一下**完成**。</span><span class="sxs-lookup"><span data-stu-id="8226a-125">toofinish creating hello listener, click **Next** twice, and then click **Finish**.</span></span> <span data-ttu-id="8226a-126">請勿讓 hello 接聽程式或資源上線此時。</span><span class="sxs-lookup"><span data-stu-id="8226a-126">Do not bring hello listener or resource online at this point.</span></span>

3. <span data-ttu-id="8226a-127"><a name="congroup"></a>設定 hello 可用性群組的 hello IP 資源。</span><span class="sxs-lookup"><span data-stu-id="8226a-127"><a name="congroup"></a>Configure hello IP resource for hello availability group.</span></span>

    <span data-ttu-id="8226a-128">a.</span><span class="sxs-lookup"><span data-stu-id="8226a-128">a.</span></span> <span data-ttu-id="8226a-129">按一下 hello**資源**索引標籤，然後再展開您建立 hello 用戶端存取點。</span><span class="sxs-lookup"><span data-stu-id="8226a-129">Click hello **Resources** tab, and then expand hello client access point you created.</span></span>  
    <span data-ttu-id="8226a-130">hello 用戶端存取點處於離線狀態。</span><span class="sxs-lookup"><span data-stu-id="8226a-130">hello client access point is offline.</span></span>

   ![用戶端存取點](./media/virtual-machines-ag-listener-configure/94-newclientaccesspoint.png) 

    <span data-ttu-id="8226a-132">b.</span><span class="sxs-lookup"><span data-stu-id="8226a-132">b.</span></span> <span data-ttu-id="8226a-133">Hello IP 資源，以滑鼠右鍵按一下，然後按一下屬性。</span><span class="sxs-lookup"><span data-stu-id="8226a-133">Right-click hello IP resource, and then click properties.</span></span> <span data-ttu-id="8226a-134">請注意 hello 名稱 hello IP 位址，並將它用於 hello `$IPResourceName` hello PowerShell 指令碼中的變數。</span><span class="sxs-lookup"><span data-stu-id="8226a-134">Note hello name of hello IP address, and use it in hello `$IPResourceName` variable in hello PowerShell script.</span></span>

    <span data-ttu-id="8226a-135">c.</span><span class="sxs-lookup"><span data-stu-id="8226a-135">c.</span></span> <span data-ttu-id="8226a-136">在 [IP 地址] 下，按一下 [靜態 IP 位址]。</span><span class="sxs-lookup"><span data-stu-id="8226a-136">Under **IP Address**, click **Static IP Address**.</span></span> <span data-ttu-id="8226a-137">與 hello 相同位址，使用 hello Azure 入口網站上設定 hello 負載平衡器位址時，請設定 hello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="8226a-137">Set hello IP address as hello same address that you used when you set hello load balancer address on hello Azure portal.</span></span>

   ![IP 資源](./media/virtual-machines-ag-listener-configure/96-ipresource.png) 

    <!-----------------------I don't see this option on server 2016
    1. Disable NetBIOS for this address and click **OK**. Repeat this step for each IP resource if your solution spans multiple Azure VNets. 
    ------------------------->

4. <span data-ttu-id="8226a-139"><a name = "dependencyGroup"></a>讓 hello SQL Server 可用性群組資源相依於 hello 用戶端存取點。</span><span class="sxs-lookup"><span data-stu-id="8226a-139"><a name = "dependencyGroup"></a>Make hello SQL Server availability group resource dependent on hello client access point.</span></span>

    <span data-ttu-id="8226a-140">a.</span><span class="sxs-lookup"><span data-stu-id="8226a-140">a.</span></span> <span data-ttu-id="8226a-141">在 [容錯移轉叢集管理員] 中，按一下 [角色]，然後按一下您的 [可用性群組]。</span><span class="sxs-lookup"><span data-stu-id="8226a-141">In Failover Cluster Manager, click **Roles**, and then click your availability group.</span></span>

    <span data-ttu-id="8226a-142">b.</span><span class="sxs-lookup"><span data-stu-id="8226a-142">b.</span></span> <span data-ttu-id="8226a-143">在 hello**資源**索引標籤，在**其他資源**hello 可用性資源群組中，以滑鼠右鍵按一下，然後按**屬性**。</span><span class="sxs-lookup"><span data-stu-id="8226a-143">On hello **Resources** tab, under **Other Resources**, right-click hello availability resource group, and then click **Properties**.</span></span> 

    <span data-ttu-id="8226a-144">c.</span><span class="sxs-lookup"><span data-stu-id="8226a-144">c.</span></span> <span data-ttu-id="8226a-145">Hello 相依性 索引標籤上新增 hello hello 用戶端存取點 （hello 接聽程式） 的資源名稱。</span><span class="sxs-lookup"><span data-stu-id="8226a-145">On hello dependencies tab, add hello name of hello client access point (hello listener) resource.</span></span>

   ![IP 資源](./media/virtual-machines-ag-listener-configure/97-propertiesdependencies.png) 

    <span data-ttu-id="8226a-147">d.</span><span class="sxs-lookup"><span data-stu-id="8226a-147">d.</span></span> <span data-ttu-id="8226a-148">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="8226a-148">Click **OK**.</span></span>

5. <span data-ttu-id="8226a-149"><a name="listname"></a>使 hello 用戶端存取點依存於 hello IP 位址資源。</span><span class="sxs-lookup"><span data-stu-id="8226a-149"><a name="listname"></a>Make hello client access point resource dependent on hello IP address.</span></span>

    <span data-ttu-id="8226a-150">a.</span><span class="sxs-lookup"><span data-stu-id="8226a-150">a.</span></span> <span data-ttu-id="8226a-151">在 [容錯移轉叢集管理員] 中，按一下 [角色]，然後按一下您的 [可用性群組]。</span><span class="sxs-lookup"><span data-stu-id="8226a-151">In Failover Cluster Manager, click **Roles**, and then click your availability group.</span></span> 

    <span data-ttu-id="8226a-152">b.</span><span class="sxs-lookup"><span data-stu-id="8226a-152">b.</span></span> <span data-ttu-id="8226a-153">在 hello**資源**索引標籤上，以滑鼠右鍵按一下 hello 用戶端存取點資源下的**伺服器名稱**，然後按一下**屬性**。</span><span class="sxs-lookup"><span data-stu-id="8226a-153">On hello **Resources** tab, right-click hello client access point resource under **Server Name**, and then click **Properties**.</span></span> 

   ![IP 資源](./media/virtual-machines-ag-listener-configure/98-dependencies.png) 

    <span data-ttu-id="8226a-155">c.</span><span class="sxs-lookup"><span data-stu-id="8226a-155">c.</span></span> <span data-ttu-id="8226a-156">按一下 hello**相依性** 索引標籤。請確認 hello IP 位址相依性。</span><span class="sxs-lookup"><span data-stu-id="8226a-156">Click hello **Dependencies** tab. Verify that hello IP address is a dependency.</span></span> <span data-ttu-id="8226a-157">如果不是，設定 hello IP 位址相依性。</span><span class="sxs-lookup"><span data-stu-id="8226a-157">If it is not, set a dependency on hello IP address.</span></span> <span data-ttu-id="8226a-158">如果有多個資源列出，請確認 hello IP 位址具有 OR、 not AND 相依性。</span><span class="sxs-lookup"><span data-stu-id="8226a-158">If there are multiple resources listed, verify that hello IP addresses have OR, not AND, dependencies.</span></span> <span data-ttu-id="8226a-159">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="8226a-159">Click **OK**.</span></span> 

   ![IP 資源](./media/virtual-machines-ag-listener-configure/98-propertiesdependencies.png) 

    <span data-ttu-id="8226a-161">d.</span><span class="sxs-lookup"><span data-stu-id="8226a-161">d.</span></span> <span data-ttu-id="8226a-162">Hello 接聽程式名稱，以滑鼠右鍵按一下，然後按一下**上線**。</span><span class="sxs-lookup"><span data-stu-id="8226a-162">Right-click hello listener name, and then click **Bring Online**.</span></span> 

    >[!TIP]
    ><span data-ttu-id="8226a-163">您可以驗證相依性已正確設定該 hello。</span><span class="sxs-lookup"><span data-stu-id="8226a-163">You can validate that hello dependencies are correctly configured.</span></span> <span data-ttu-id="8226a-164">在 [容錯移轉叢集管理員] 中，移 tooRoles、 hello 可用性群組上按一下滑鼠右鍵、 按一下**其他動作**，然後按一下**顯示相依性報告**。</span><span class="sxs-lookup"><span data-stu-id="8226a-164">In Failover Cluster Manager, go tooRoles, right-click hello availability group, click **More Actions**, and then click  **Show Dependency Report**.</span></span> <span data-ttu-id="8226a-165">Hello 相依性已正確設定，hello 可用性群組是依存於 hello 網路名稱，而 hello 網路名稱是取決於 hello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="8226a-165">When hello dependencies are correctly configured, hello availability group is dependent on hello network name, and hello network name is dependent on hello IP address.</span></span> 


6. <span data-ttu-id="8226a-166"><a name="setparam"></a>在 PowerShell 中設定 hello 叢集參數。</span><span class="sxs-lookup"><span data-stu-id="8226a-166"><a name="setparam"></a>Set hello cluster parameters in PowerShell.</span></span>
    
    <span data-ttu-id="8226a-167">a.</span><span class="sxs-lookup"><span data-stu-id="8226a-167">a.</span></span> <span data-ttu-id="8226a-168">複製下列 SQL Server 執行個體的 PowerShell 指令碼 tooone hello。</span><span class="sxs-lookup"><span data-stu-id="8226a-168">Copy hello following PowerShell script tooone of your SQL Server instances.</span></span> <span data-ttu-id="8226a-169">更新您的環境的 hello 變數。</span><span class="sxs-lookup"><span data-stu-id="8226a-169">Update hello variables for your environment.</span></span>     
    
    ```PowerShell
    $ClusterNetworkName = "<MyClusterNetworkName>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name)
    $IPResourceName = "<IPResourceName>" # hello IP Address resource name
    $ILBIP = “<n.n.n.n>” # hello IP Address of hello Internal Load Balancer (ILB). This is hello static IP address for hello load balancer you configured in hello Azure portal.
    [int]$ProbePort = <nnnnn>
    
    Import-Module FailoverClusters
    
    Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
    ```

    <span data-ttu-id="8226a-170">b.</span><span class="sxs-lookup"><span data-stu-id="8226a-170">b.</span></span> <span data-ttu-id="8226a-171">其中一個 hello 叢集節點上執行 hello PowerShell 指令碼，以設定 hello 叢集參數。</span><span class="sxs-lookup"><span data-stu-id="8226a-171">Set hello cluster parameters by running hello PowerShell script on one of hello cluster nodes.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="8226a-172">如果您的 SQL Server 執行個體位於不同的區域中，您需要 toorun hello PowerShell 指令碼兩次。</span><span class="sxs-lookup"><span data-stu-id="8226a-172">If your SQL Server instances are in separate regions, you need toorun hello PowerShell script twice.</span></span> <span data-ttu-id="8226a-173">hello 第一次，請使用 hello`$ILBIP`和`$ProbePort`hello 第一個區域中。</span><span class="sxs-lookup"><span data-stu-id="8226a-173">hello first time, use hello `$ILBIP` and `$ProbePort` from hello first region.</span></span> <span data-ttu-id="8226a-174">hello 第二次，請使用 hello`$ILBIP`和`$ProbePort`從 hello 第二個區域。</span><span class="sxs-lookup"><span data-stu-id="8226a-174">hello second time, use hello `$ILBIP` and `$ProbePort` from hello second region.</span></span> <span data-ttu-id="8226a-175">hello 叢集網路名稱和 hello 叢集 IP 資源名稱是 hello 相同。</span><span class="sxs-lookup"><span data-stu-id="8226a-175">hello cluster network name and hello cluster IP resource name are hello same.</span></span> 
