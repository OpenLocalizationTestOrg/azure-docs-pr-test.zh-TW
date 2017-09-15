### <a name="open-tcp-ports-in-the-windows-firewall-for-the-default-instance-of-the-database-engine"></a><span data-ttu-id="4bce8-101">在 Windows 防火牆中為 Database Engine 的預設執行個體開啟 TCP 連接埠</span><span class="sxs-lookup"><span data-stu-id="4bce8-101">Open TCP ports in the Windows firewall for the default instance of the Database Engine</span></span>
1. <span data-ttu-id="4bce8-102">使用遠端桌面連線到虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="4bce8-102">Connect to the virtual machine with Remote Desktop.</span></span> <span data-ttu-id="4bce8-103">如需連線到 VM 的詳細指示，請參閱[使用遠端桌面開啟 SQL VM](../articles/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision.md#open-the-vm-with-remote-desktop)。</span><span class="sxs-lookup"><span data-stu-id="4bce8-103">For detailed instructions on connecting to the VM, see [Open a SQL VM with Remote Desktop](../articles/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision.md#open-the-vm-with-remote-desktop).</span></span>
2. <span data-ttu-id="4bce8-104">登入後，在 [開始] 畫面中輸入 **WF.msc**，然後按 ENTER 鍵。</span><span class="sxs-lookup"><span data-stu-id="4bce8-104">Once logged in, at the Start screen, type **WF.msc**, and then hit ENTER.</span></span>
   
    ![啟動防火牆程式](./media/virtual-machines-sql-server-connection-steps/12Open-WF.png)
3. <span data-ttu-id="4bce8-106">在 [具有進階安全性的 Windows 防火牆] 的左窗格中，以滑鼠右鍵按一下 [輸入規則]，然後在動作窗格中按一下 [新增規則]。</span><span class="sxs-lookup"><span data-stu-id="4bce8-106">In the **Windows Firewall with Advanced Security**, in the left pane, right-click **Inbound Rules**, and then click **New Rule** in the action pane.</span></span>
   
    ![新增規則](./media/virtual-machines-sql-server-connection-steps/13New-FW-Rule.png)
4. <span data-ttu-id="4bce8-108">在 [新增輸入規則精靈] 對話方塊的 [規則類型] 下方， 選取 [連接埠]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="4bce8-108">In the **New Inbound Rule Wizard** dialog box, under **Rule Type**, select **Port**, and then click **Next**.</span></span>
5. <span data-ttu-id="4bce8-109">在 [通訊協定及連接埠] 對話方塊中，使用預設的 [TCP]。</span><span class="sxs-lookup"><span data-stu-id="4bce8-109">In the **Protocol and Ports** dialog, use the default **TCP**.</span></span> <span data-ttu-id="4bce8-110">接著在 [特定本機連接埠] 方塊中，輸入 Database Engine 執行個體的連接埠號碼 (預設執行個體的連接埠號碼 **1433**，或您在端點步驟中選擇的私人連接埠號碼)。</span><span class="sxs-lookup"><span data-stu-id="4bce8-110">In the **Specific local ports** box, then type the port number of the instance of the Database Engine (**1433** for the default instance or your choice for the private port in the endpoint step).</span></span>
   
    ![TCP 連接埠 1433](./media/virtual-machines-sql-server-connection-steps/14Port-1433.png)
6. <span data-ttu-id="4bce8-112">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="4bce8-112">Click **Next**.</span></span>
7. <span data-ttu-id="4bce8-113">在 [動作] 對話方塊中選取 [允許連線]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="4bce8-113">In the **Action** dialog box, select **Allow the connection**, and then click **Next**.</span></span>
   
    <span data-ttu-id="4bce8-114">**安全性注意事項：**選取 [僅允許安全連線] 可提供額外的安全性。</span><span class="sxs-lookup"><span data-stu-id="4bce8-114">**Security Note:** Selecting **Allow the connection if it is secure** can provide additional security.</span></span> <span data-ttu-id="4bce8-115">如果您想要在環境中設定額外的安全性選項，請選取此選項。</span><span class="sxs-lookup"><span data-stu-id="4bce8-115">Select this option if you want to configure additional security options in your environment.</span></span>
   
    ![允許連線](./media/virtual-machines-sql-server-connection-steps/15Allow-Connection.png)
8. <span data-ttu-id="4bce8-117">在 [設定檔] 對話方塊中，依序選取 [公用]、[私人]，然後 [網域]。</span><span class="sxs-lookup"><span data-stu-id="4bce8-117">In the **Profile** dialog box, select **Public**, **Private**, and **Domain**.</span></span> <span data-ttu-id="4bce8-118">然後按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="4bce8-118">Then click **Next**.</span></span>
   
    <span data-ttu-id="4bce8-119">**安全性注意事項：**選取 [公用] 可允許透過網際網路存取。</span><span class="sxs-lookup"><span data-stu-id="4bce8-119">**Security Note:**  Selecting **Public** allows access over the internet.</span></span> <span data-ttu-id="4bce8-120">請盡可能選取較具有限制性的設定檔。</span><span class="sxs-lookup"><span data-stu-id="4bce8-120">Whenever possible, select a more restrictive profile.</span></span>
   
    ![公用設定檔](./media/virtual-machines-sql-server-connection-steps/16Public-Private-Domain-Profile.png)
9. <span data-ttu-id="4bce8-122">在 [名稱] 對話方塊中輸入此規則的名稱和描述，然後按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="4bce8-122">In the **Name** dialog box, type a name and description for this rule, and then click **Finish**.</span></span>
   
    ![規則名稱](./media/virtual-machines-sql-server-connection-steps/17Rule-Name.png)

<span data-ttu-id="4bce8-124">視需要為其他元件開啟額外的連接埠。</span><span class="sxs-lookup"><span data-stu-id="4bce8-124">Open additional ports for other components as needed.</span></span> <span data-ttu-id="4bce8-125">如需詳細資訊，請參閱 [設定 Windows 防火牆以允許 SQL Server 存取](http://msdn.microsoft.com/library/cc646023.aspx)。</span><span class="sxs-lookup"><span data-stu-id="4bce8-125">For more information, see [Configuring the Windows Firewall to Allow SQL Server Access](http://msdn.microsoft.com/library/cc646023.aspx).</span></span>

### <a name="configure-sql-server-to-listen-on-the-tcp-protocol"></a><span data-ttu-id="4bce8-126">設定 SQL Server 以接聽 TCP 通訊協定</span><span class="sxs-lookup"><span data-stu-id="4bce8-126">Configure SQL Server to listen on the TCP protocol</span></span>

[!INCLUDE [Enable TCP](virtual-machines-sql-server-connection-tcp-protocol.md)]

### <a name="configure-sql-server-for-mixed-mode-authentication"></a><span data-ttu-id="4bce8-127">設定 SQL Server 以進行混合模式驗證</span><span class="sxs-lookup"><span data-stu-id="4bce8-127">Configure SQL Server for mixed mode authentication</span></span>
<span data-ttu-id="4bce8-128">SQL Server Database Engine 須有網域環境才能使用 Windows 驗證。</span><span class="sxs-lookup"><span data-stu-id="4bce8-128">The SQL Server Database Engine cannot use Windows Authentication without domain environment.</span></span> <span data-ttu-id="4bce8-129">若要從另一部電腦連接 Database Engine，請設定 SQL Server 以進行混合模式驗證。</span><span class="sxs-lookup"><span data-stu-id="4bce8-129">To connect to the Database Engine from another computer, configure SQL Server for mixed mode authentication.</span></span> <span data-ttu-id="4bce8-130">混合模式驗證可允許 SQL Server 驗證和 Windows 驗證。</span><span class="sxs-lookup"><span data-stu-id="4bce8-130">Mixed mode authentication allows both SQL Server Authentication and Windows Authentication.</span></span>

> [!NOTE]
> <span data-ttu-id="4bce8-131">如果您已經設定具有已設定網域環境的 Azure 虛擬網路，可能就不需要設定混合模式驗證。</span><span class="sxs-lookup"><span data-stu-id="4bce8-131">Configuring mixed mode authentication might not be necessary if you have configured an Azure Virtual Network with a configured domain environment.</span></span>
> 
> 

1. <span data-ttu-id="4bce8-132">連接到虛擬機器時，在 [開始] 頁面上輸入 **SQL Server Management Studio** ，然後按一下選取的圖示。</span><span class="sxs-lookup"><span data-stu-id="4bce8-132">While connected to the virtual machine, on the Start page, type **SQL Server Management Studio** and click the selected icon.</span></span>
   
    <span data-ttu-id="4bce8-133">當您首次開啟 Management Studio 時，它必須建立使用者 Management Studio 環境。</span><span class="sxs-lookup"><span data-stu-id="4bce8-133">The first time you open Management Studio it must create the users Management Studio environment.</span></span> <span data-ttu-id="4bce8-134">這可能需要花費幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="4bce8-134">This may take a few moments.</span></span>
2. <span data-ttu-id="4bce8-135">Management Studio 會出現 [連接到伺服器] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="4bce8-135">Management Studio presents the **Connect to Server** dialog box.</span></span> <span data-ttu-id="4bce8-136">在 [伺服器名稱] 方塊中，輸入虛擬機器的名稱，以使用 [物件總管] 連接到 Database Engine (除了虛擬機器名稱之外，您也可以使用 **(local)** 或單一句點做為 [伺服器名稱])。</span><span class="sxs-lookup"><span data-stu-id="4bce8-136">In the **Server name** box, type the name of the virtual machine to connect to the Database Engine  with the Object Explorer (Instead of the virtual machine name you can also use **(local)** or a single period as the **Server name**).</span></span> <span data-ttu-id="4bce8-137">選取 [Windows 驗證]，並保留 [使用者名稱] 方塊中的 **your_VM_name\your_local_administrator**。</span><span class="sxs-lookup"><span data-stu-id="4bce8-137">Select **Windows Authentication**, and leave ***your_VM_name*\your_local_administrator** in the **User name** box.</span></span> <span data-ttu-id="4bce8-138">按一下 [ **連接**]。</span><span class="sxs-lookup"><span data-stu-id="4bce8-138">Click **Connect**.</span></span>
   
    ![連線到伺服器](./media/virtual-machines-sql-server-connection-steps/19Connect-to-Server.png)
3. <span data-ttu-id="4bce8-140">在 SQL Server Management Studio 物件總管中，以滑鼠右鍵按一下 SQL Server 執行個體的名稱 (虛擬機器名稱)，然後按一下 [屬性] 。</span><span class="sxs-lookup"><span data-stu-id="4bce8-140">In SQL Server Management Studio Object Explorer, right-click the name of the instance of SQL Server (the virtual machine name), and then click **Properties**.</span></span>
   
    ![伺服器屬性](./media/virtual-machines-sql-server-connection-steps/20Server-Properties.png)
4. <span data-ttu-id="4bce8-142">在 [安全性] 頁面的 [伺服器驗證] 下方，選取 [SQL Server 及 Windows 驗證模式]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="4bce8-142">On the **Security** page, under **Server authentication**, select **SQL Server and Windows Authentication mode**, and then click **OK**.</span></span>
   
    ![選取驗證模式](./media/virtual-machines-sql-server-connection-steps/21Mixed-Mode.png)
5. <span data-ttu-id="4bce8-144">在 [SQL Server Management Studio] 對話方塊中，按一下 [確定]  以確認重新啟動 SQL Server 的需求。</span><span class="sxs-lookup"><span data-stu-id="4bce8-144">In the SQL Server Management Studio dialog box, click **OK** to acknowledge the requirement to restart SQL Server.</span></span>
6. <span data-ttu-id="4bce8-145">在物件總管中，以滑鼠右鍵按一下伺服器，然後按一下 [重新啟動]。</span><span class="sxs-lookup"><span data-stu-id="4bce8-145">In Object Explorer, right-click your server, and then click **Restart**.</span></span> <span data-ttu-id="4bce8-146">(如果 SQL Server Agent 處於執行狀態，您也必須將其重新啟動。)</span><span class="sxs-lookup"><span data-stu-id="4bce8-146">(If SQL Server Agent is running, it must also be restarted.)</span></span>
   
    ![重新啟動](./media/virtual-machines-sql-server-connection-steps/22Restart2.png)
7. <span data-ttu-id="4bce8-148">在 [SQL Server Management Studio] 對話方塊中，按一下 [ **是** ] 以同意重新啟動 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="4bce8-148">In the SQL Server Management Studio dialog box, click **Yes** to agree that you want to restart SQL Server.</span></span>

### <a name="create-sql-server-authentication-logins"></a><span data-ttu-id="4bce8-149">建立 SQL Server 驗證登入</span><span class="sxs-lookup"><span data-stu-id="4bce8-149">Create SQL Server authentication logins</span></span>
<span data-ttu-id="4bce8-150">若要從另一部電腦連接 Database Engine，您至少必須建立一個 SQL Server 驗證登入。</span><span class="sxs-lookup"><span data-stu-id="4bce8-150">To connect to the Database Engine from another computer, you must create at least one SQL Server authentication login.</span></span>

1. <span data-ttu-id="4bce8-151">在 SQL Server Management Studio 物件總管中，展開要建立新登入之伺服器執行個體的資料夾。</span><span class="sxs-lookup"><span data-stu-id="4bce8-151">In SQL Server Management Studio Object Explorer, expand the folder of the server instance in which you want to create the new login.</span></span>
2. <span data-ttu-id="4bce8-152">以滑鼠右鍵按一下 [安全性] 資料夾，指向 [新增]，然後選取 [登入...]。</span><span class="sxs-lookup"><span data-stu-id="4bce8-152">Right-click the **Security** folder, point to **New**, and select **Login...**.</span></span>
   
    ![新增登入](./media/virtual-machines-sql-server-connection-steps/23New-Login.png)
3. <span data-ttu-id="4bce8-154">在 [登入 - 新增] 對話方塊的 [一般] 頁面中，於 [登入名稱] 方塊輸入新使用者的名稱。</span><span class="sxs-lookup"><span data-stu-id="4bce8-154">In the **Login - New** dialog box, on the **General** page, enter the name of the new user in the **Login name** box.</span></span>
4. <span data-ttu-id="4bce8-155">選取 [SQL Server 驗證] 。</span><span class="sxs-lookup"><span data-stu-id="4bce8-155">Select **SQL Server authentication**.</span></span>
5. <span data-ttu-id="4bce8-156">在 [密碼]  方塊中，輸入新使用者的密碼。</span><span class="sxs-lookup"><span data-stu-id="4bce8-156">In the **Password** box, enter a password for the new user.</span></span> <span data-ttu-id="4bce8-157">在 [確認密碼]  方塊中再次輸入密碼。</span><span class="sxs-lookup"><span data-stu-id="4bce8-157">Enter that password again into the **Confirm Password** box.</span></span>
6. <span data-ttu-id="4bce8-158">選取所需的密碼強制選項 ([強制執行密碼原則]、[強制執行密碼逾期]，以及 [使用者必須在下次登入時變更密碼])。</span><span class="sxs-lookup"><span data-stu-id="4bce8-158">Select the password enforcement options required (**Enforce password policy**, **Enforce password expiration**, and **User must change password at next login**).</span></span> <span data-ttu-id="4bce8-159">如果您是自己使用此登入，就不需要在下次登入時變更密碼。</span><span class="sxs-lookup"><span data-stu-id="4bce8-159">If you are using this login for yourself, you do not need to require a password change at the next login.</span></span>
7. <span data-ttu-id="4bce8-160">在 [預設資料庫] 清單中選取登入的預設資料庫。</span><span class="sxs-lookup"><span data-stu-id="4bce8-160">From the **Default database** list, select a default database for the login.</span></span> <span data-ttu-id="4bce8-161">[master] 是此選項的預設值。</span><span class="sxs-lookup"><span data-stu-id="4bce8-161">**master** is the default for this option.</span></span> <span data-ttu-id="4bce8-162">如果您尚未建立使用者資料庫，請保留 [master] 的設定。</span><span class="sxs-lookup"><span data-stu-id="4bce8-162">If you have not yet created a user database, leave this set to **master**.</span></span>
   
    ![登入屬性](./media/virtual-machines-sql-server-connection-steps/24Test-Login.png)
8. <span data-ttu-id="4bce8-164">如果您正在建立第一個登入，也許會想要將此登入指定為 SQL Server 系統管理員。</span><span class="sxs-lookup"><span data-stu-id="4bce8-164">If this is the first login you are creating, you may want to designate this login as a SQL Server administrator.</span></span> <span data-ttu-id="4bce8-165">如果是的話，請在 [伺服器角色] 頁面中勾選 [系統管理員 (sysadmin)]。</span><span class="sxs-lookup"><span data-stu-id="4bce8-165">If so, on the **Server Roles** page, check **sysadmin**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="4bce8-166">系統管理員 (sysadmin) 固定伺服器角色的成員擁有 Database Engine 的完整控制權限。</span><span class="sxs-lookup"><span data-stu-id="4bce8-166">Members of the sysadmin fixed server role have complete control of the Database Engine.</span></span> <span data-ttu-id="4bce8-167">因此請謹慎限制此角色的成員資格。</span><span class="sxs-lookup"><span data-stu-id="4bce8-167">You should carefully restrict membership in this role.</span></span>
   > 
   > 
   
   ![系統管理員 (sysadmin)](./media/virtual-machines-sql-server-connection-steps/25sysadmin.png)
9. <span data-ttu-id="4bce8-169">按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="4bce8-169">Click OK.</span></span>

<span data-ttu-id="4bce8-170">如需 SQL Server 登入的詳細資訊，請參閱 [建立登入](http://msdn.microsoft.com/library/aa337562.aspx)。</span><span class="sxs-lookup"><span data-stu-id="4bce8-170">For more information about SQL Server logins, see [Create a Login](http://msdn.microsoft.com/library/aa337562.aspx).</span></span>

