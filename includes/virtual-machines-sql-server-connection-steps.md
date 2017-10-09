### <a name="open-tcp-ports-in-hello-windows-firewall-for-hello-default-instance-of-hello-database-engine"></a><span data-ttu-id="b0a94-101">Hello hello 的 hello Database Engine 的預設執行個體的 Windows 防火牆中開啟 TCP 通訊埠</span><span class="sxs-lookup"><span data-stu-id="b0a94-101">Open TCP ports in hello Windows firewall for hello default instance of hello Database Engine</span></span>
1. <span data-ttu-id="b0a94-102">使用遠端桌面連線 toohello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="b0a94-102">Connect toohello virtual machine with Remote Desktop.</span></span> <span data-ttu-id="b0a94-103">連接 toohello VM 連接的詳細指示，請參閱[開啟遠端桌面的 SQL VM](../articles/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision.md#open-the-vm-with-remote-desktop)。</span><span class="sxs-lookup"><span data-stu-id="b0a94-103">For detailed instructions on connecting toohello VM, see [Open a SQL VM with Remote Desktop](../articles/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision.md#open-the-vm-with-remote-desktop).</span></span>
2. <span data-ttu-id="b0a94-104">一旦登入，在 hello 開始畫面，輸入**WF.msc**，然後按 enter 鍵。</span><span class="sxs-lookup"><span data-stu-id="b0a94-104">Once logged in, at hello Start screen, type **WF.msc**, and then hit ENTER.</span></span>
   
    ![啟動防火牆程式 hello](./media/virtual-machines-sql-server-connection-steps/12Open-WF.png)
3. <span data-ttu-id="b0a94-106">在 hello**具有進階安全性的 Windows 防火牆**，在 [hello 左的窗格中以滑鼠右鍵按一下**輸入規則**，然後按一下**新規則**hello 動作] 窗格中。</span><span class="sxs-lookup"><span data-stu-id="b0a94-106">In hello **Windows Firewall with Advanced Security**, in hello left pane, right-click **Inbound Rules**, and then click **New Rule** in hello action pane.</span></span>
   
    ![新增規則](./media/virtual-machines-sql-server-connection-steps/13New-FW-Rule.png)
4. <span data-ttu-id="b0a94-108">在 hello**新增輸入規則精靈**對話方塊的 **規則類型**，選取**連接埠**，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="b0a94-108">In hello **New Inbound Rule Wizard** dialog box, under **Rule Type**, select **Port**, and then click **Next**.</span></span>
5. <span data-ttu-id="b0a94-109">在 hello**通訊協定和連接埠**對話方塊中，使用 hello 預設**TCP**。</span><span class="sxs-lookup"><span data-stu-id="b0a94-109">In hello **Protocol and Ports** dialog, use hello default **TCP**.</span></span> <span data-ttu-id="b0a94-110">在 [hello**特定本機連接埠**] 方塊中，則型別 hello 連接埠號碼 hello hello Database Engine 執行個體 (**1433年**hello 預設執行個體，或您選擇的 hello hello 端點步驟中的私用連接埠)。</span><span class="sxs-lookup"><span data-stu-id="b0a94-110">In hello **Specific local ports** box, then type hello port number of hello instance of hello Database Engine (**1433** for hello default instance or your choice for hello private port in hello endpoint step).</span></span>
   
    ![TCP 連接埠 1433](./media/virtual-machines-sql-server-connection-steps/14Port-1433.png)
6. <span data-ttu-id="b0a94-112">按一下 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="b0a94-112">Click **Next**.</span></span>
7. <span data-ttu-id="b0a94-113">在 hello**動作**對話方塊中，選取**允許 hello 連線**，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="b0a94-113">In hello **Action** dialog box, select **Allow hello connection**, and then click **Next**.</span></span>
   
    <span data-ttu-id="b0a94-114">**安全性注意事項：**選取**允許 hello 連線是否安全**可以提供額外的安全性。</span><span class="sxs-lookup"><span data-stu-id="b0a94-114">**Security Note:** Selecting **Allow hello connection if it is secure** can provide additional security.</span></span> <span data-ttu-id="b0a94-115">如果您要在您的環境中的 tooconfigure 額外的安全性選項，請選取此選項。</span><span class="sxs-lookup"><span data-stu-id="b0a94-115">Select this option if you want tooconfigure additional security options in your environment.</span></span>
   
    ![允許連線](./media/virtual-machines-sql-server-connection-steps/15Allow-Connection.png)
8. <span data-ttu-id="b0a94-117">在 hello**設定檔**對話方塊中，選取**公用**，**私人**，和**網域**。</span><span class="sxs-lookup"><span data-stu-id="b0a94-117">In hello **Profile** dialog box, select **Public**, **Private**, and **Domain**.</span></span> <span data-ttu-id="b0a94-118">然後按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="b0a94-118">Then click **Next**.</span></span>
   
    <span data-ttu-id="b0a94-119">**安全性注意事項：**選取**公用**允許存取透過 hello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="b0a94-119">**Security Note:**  Selecting **Public** allows access over hello internet.</span></span> <span data-ttu-id="b0a94-120">請盡可能選取較具有限制性的設定檔。</span><span class="sxs-lookup"><span data-stu-id="b0a94-120">Whenever possible, select a more restrictive profile.</span></span>
   
    ![公用設定檔](./media/virtual-machines-sql-server-connection-steps/16Public-Private-Domain-Profile.png)
9. <span data-ttu-id="b0a94-122">在 hello**名稱**對話方塊中，輸入名稱和描述，此規則，然後按一下**完成**。</span><span class="sxs-lookup"><span data-stu-id="b0a94-122">In hello **Name** dialog box, type a name and description for this rule, and then click **Finish**.</span></span>
   
    ![規則名稱](./media/virtual-machines-sql-server-connection-steps/17Rule-Name.png)

<span data-ttu-id="b0a94-124">視需要為其他元件開啟額外的連接埠。</span><span class="sxs-lookup"><span data-stu-id="b0a94-124">Open additional ports for other components as needed.</span></span> <span data-ttu-id="b0a94-125">如需詳細資訊，請參閱[設定 hello SQL Server 存取的 Windows 防火牆 tooAllow](http://msdn.microsoft.com/library/cc646023.aspx)。</span><span class="sxs-lookup"><span data-stu-id="b0a94-125">For more information, see [Configuring hello Windows Firewall tooAllow SQL Server Access](http://msdn.microsoft.com/library/cc646023.aspx).</span></span>

### <a name="configure-sql-server-toolisten-on-hello-tcp-protocol"></a><span data-ttu-id="b0a94-126">設定 SQL Server toolisten hello TCP 通訊協定</span><span class="sxs-lookup"><span data-stu-id="b0a94-126">Configure SQL Server toolisten on hello TCP protocol</span></span>

[!INCLUDE [Enable TCP](virtual-machines-sql-server-connection-tcp-protocol.md)]

### <a name="configure-sql-server-for-mixed-mode-authentication"></a><span data-ttu-id="b0a94-127">設定 SQL Server 以進行混合模式驗證</span><span class="sxs-lookup"><span data-stu-id="b0a94-127">Configure SQL Server for mixed mode authentication</span></span>
<span data-ttu-id="b0a94-128">hello SQL Server Database Engine 無法使用 Windows 驗證，若沒有網域環境。</span><span class="sxs-lookup"><span data-stu-id="b0a94-128">hello SQL Server Database Engine cannot use Windows Authentication without domain environment.</span></span> <span data-ttu-id="b0a94-129">tooconnect toohello Database Engine 從另一部電腦，設定 SQL Server 混合的模式驗證。</span><span class="sxs-lookup"><span data-stu-id="b0a94-129">tooconnect toohello Database Engine from another computer, configure SQL Server for mixed mode authentication.</span></span> <span data-ttu-id="b0a94-130">混合模式驗證可允許 SQL Server 驗證和 Windows 驗證。</span><span class="sxs-lookup"><span data-stu-id="b0a94-130">Mixed mode authentication allows both SQL Server Authentication and Windows Authentication.</span></span>

> [!NOTE]
> <span data-ttu-id="b0a94-131">如果您已經設定具有已設定網域環境的 Azure 虛擬網路，可能就不需要設定混合模式驗證。</span><span class="sxs-lookup"><span data-stu-id="b0a94-131">Configuring mixed mode authentication might not be necessary if you have configured an Azure Virtual Network with a configured domain environment.</span></span>
> 
> 

1. <span data-ttu-id="b0a94-132">同時連接的 toohello 虛擬機器，在 hello 開始頁面上，輸入**SQL Server Management Studio**按一下 hello 選的圖示。</span><span class="sxs-lookup"><span data-stu-id="b0a94-132">While connected toohello virtual machine, on hello Start page, type **SQL Server Management Studio** and click hello selected icon.</span></span>
   
    <span data-ttu-id="b0a94-133">hello 第一次開啟 Management Studio，就必須建立 hello 使用者 Management Studio 環境。</span><span class="sxs-lookup"><span data-stu-id="b0a94-133">hello first time you open Management Studio it must create hello users Management Studio environment.</span></span> <span data-ttu-id="b0a94-134">這可能需要花費幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="b0a94-134">This may take a few moments.</span></span>
2. <span data-ttu-id="b0a94-135">Management Studio 顯示 hello**連接 tooServer**  對話方塊。</span><span class="sxs-lookup"><span data-stu-id="b0a94-135">Management Studio presents hello **Connect tooServer** dialog box.</span></span> <span data-ttu-id="b0a94-136">在 hello**伺服器名稱** 方塊中，輸入 hello 名稱 hello 虛擬機器 tooconnect toohello Database Engine 以 hello 物件總管 中的 (而不是 hello 虛擬機器名稱，您也可以使用**（本機）**或單一句號為 hello**伺服器名稱**)。</span><span class="sxs-lookup"><span data-stu-id="b0a94-136">In hello **Server name** box, type hello name of hello virtual machine tooconnect toohello Database Engine  with hello Object Explorer (Instead of hello virtual machine name you can also use **(local)** or a single period as hello **Server name**).</span></span> <span data-ttu-id="b0a94-137">選取**Windows 驗證**，並將保留 ***your_VM_name*\your_local_administrator**在 hello**使用者名**方塊。</span><span class="sxs-lookup"><span data-stu-id="b0a94-137">Select **Windows Authentication**, and leave ***your_VM_name*\your_local_administrator** in hello **User name** box.</span></span> <span data-ttu-id="b0a94-138">按一下 [ **連接**]。</span><span class="sxs-lookup"><span data-stu-id="b0a94-138">Click **Connect**.</span></span>
   
    ![連接 tooServer](./media/virtual-machines-sql-server-connection-steps/19Connect-to-Server.png)
3. <span data-ttu-id="b0a94-140">SQL Server Management Studio 物件總管，在 hello hello （hello 虛擬機器名稱） 的 SQL Server 執行個體名稱上按一下滑鼠右鍵，然後按一下**屬性**。</span><span class="sxs-lookup"><span data-stu-id="b0a94-140">In SQL Server Management Studio Object Explorer, right-click hello name of hello instance of SQL Server (hello virtual machine name), and then click **Properties**.</span></span>
   
    ![伺服器屬性](./media/virtual-machines-sql-server-connection-steps/20Server-Properties.png)
4. <span data-ttu-id="b0a94-142">Hello 上**安全性**頁面的 **伺服器驗證**，選取**SQL Server 及 Windows 驗證模式**，然後按一下**確定**.</span><span class="sxs-lookup"><span data-stu-id="b0a94-142">On hello **Security** page, under **Server authentication**, select **SQL Server and Windows Authentication mode**, and then click **OK**.</span></span>
   
    ![選取驗證模式](./media/virtual-machines-sql-server-connection-steps/21Mixed-Mode.png)
5. <span data-ttu-id="b0a94-144">在 hello SQL Server Management Studio 對話方塊中，按一下 **確定**tooacknowledge hello 需求 toorestart SQL Server。</span><span class="sxs-lookup"><span data-stu-id="b0a94-144">In hello SQL Server Management Studio dialog box, click **OK** tooacknowledge hello requirement toorestart SQL Server.</span></span>
6. <span data-ttu-id="b0a94-145">在物件總管中，以滑鼠右鍵按一下伺服器，然後按一下重新啟動。</span><span class="sxs-lookup"><span data-stu-id="b0a94-145">In Object Explorer, right-click your server, and then click **Restart**.</span></span> <span data-ttu-id="b0a94-146">(如果 SQL Server Agent 處於執行狀態，您也必須將其重新啟動。)</span><span class="sxs-lookup"><span data-stu-id="b0a94-146">(If SQL Server Agent is running, it must also be restarted.)</span></span>
   
    ![重新啟動](./media/virtual-machines-sql-server-connection-steps/22Restart2.png)
7. <span data-ttu-id="b0a94-148">在 hello SQL Server Management Studio 對話方塊中，按一下 **是**tooagree 想 toorestart SQL Server。</span><span class="sxs-lookup"><span data-stu-id="b0a94-148">In hello SQL Server Management Studio dialog box, click **Yes** tooagree that you want toorestart SQL Server.</span></span>

### <a name="create-sql-server-authentication-logins"></a><span data-ttu-id="b0a94-149">建立 SQL Server 驗證登入</span><span class="sxs-lookup"><span data-stu-id="b0a94-149">Create SQL Server authentication logins</span></span>
<span data-ttu-id="b0a94-150">tooconnect toohello Database Engine 從另一部電腦，您必須建立至少一個 SQL Server 驗證登入。</span><span class="sxs-lookup"><span data-stu-id="b0a94-150">tooconnect toohello Database Engine from another computer, you must create at least one SQL Server authentication login.</span></span>

1. <span data-ttu-id="b0a94-151">在 SQL Server Management Studio 物件總管 中，展開 hello 資料夾 hello 想 toocreate hello 新登入的伺服器執行個體。</span><span class="sxs-lookup"><span data-stu-id="b0a94-151">In SQL Server Management Studio Object Explorer, expand hello folder of hello server instance in which you want toocreate hello new login.</span></span>
2. <span data-ttu-id="b0a94-152">以滑鼠右鍵按一下 hello**安全性**資料夾中，點太**新增**，然後選取**登入...**.</span><span class="sxs-lookup"><span data-stu-id="b0a94-152">Right-click hello **Security** folder, point too**New**, and select **Login...**.</span></span>
   
    ![新增登入](./media/virtual-machines-sql-server-connection-steps/23New-Login.png)
3. <span data-ttu-id="b0a94-154">在 hello**登入-新增** 對話方塊上 hello**一般**頁面上，輸入 hello hello 新使用者名稱中 hello**登入名稱**方塊。</span><span class="sxs-lookup"><span data-stu-id="b0a94-154">In hello **Login - New** dialog box, on hello **General** page, enter hello name of hello new user in hello **Login name** box.</span></span>
4. <span data-ttu-id="b0a94-155">選取 [SQL Server 驗證] 。</span><span class="sxs-lookup"><span data-stu-id="b0a94-155">Select **SQL Server authentication**.</span></span>
5. <span data-ttu-id="b0a94-156">在 hello**密碼**方塊中，輸入 hello 新使用者的密碼。</span><span class="sxs-lookup"><span data-stu-id="b0a94-156">In hello **Password** box, enter a password for hello new user.</span></span> <span data-ttu-id="b0a94-157">該密碼一次輸入 hello**確認密碼**方塊。</span><span class="sxs-lookup"><span data-stu-id="b0a94-157">Enter that password again into hello **Confirm Password** box.</span></span>
6. <span data-ttu-id="b0a94-158">選取所需的 hello 密碼強制執行選項 (**強制執行密碼原則**，**強制執行密碼逾期**，和**使用者必須變更密碼，在下次登入時**)。</span><span class="sxs-lookup"><span data-stu-id="b0a94-158">Select hello password enforcement options required (**Enforce password policy**, **Enforce password expiration**, and **User must change password at next login**).</span></span> <span data-ttu-id="b0a94-159">如果您自行使用此登入，您不需要的 toorequire 在 hello 下次登入時變更密碼。</span><span class="sxs-lookup"><span data-stu-id="b0a94-159">If you are using this login for yourself, you do not need toorequire a password change at hello next login.</span></span>
7. <span data-ttu-id="b0a94-160">從 hello**預設資料庫**清單中，選取 hello 登入的預設資料庫。</span><span class="sxs-lookup"><span data-stu-id="b0a94-160">From hello **Default database** list, select a default database for hello login.</span></span> <span data-ttu-id="b0a94-161">**主要**hello 預設值，這個選項。</span><span class="sxs-lookup"><span data-stu-id="b0a94-161">**master** is hello default for this option.</span></span> <span data-ttu-id="b0a94-162">如果您尚未建立使用者資料庫，將這個資料集太**主要**。</span><span class="sxs-lookup"><span data-stu-id="b0a94-162">If you have not yet created a user database, leave this set too**master**.</span></span>
   
    ![登入屬性](./media/virtual-machines-sql-server-connection-steps/24Test-Login.png)
8. <span data-ttu-id="b0a94-164">如果這是您要建立 hello 第一個登入，您可能想 toodesignate 此登入 SQL Server 系統管理員身分。</span><span class="sxs-lookup"><span data-stu-id="b0a94-164">If this is hello first login you are creating, you may want toodesignate this login as a SQL Server administrator.</span></span> <span data-ttu-id="b0a94-165">如果是這樣，在 hello**伺服器角色**頁面上，核取**sysadmin**。</span><span class="sxs-lookup"><span data-stu-id="b0a94-165">If so, on hello **Server Roles** page, check **sysadmin**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="b0a94-166">Hello sysadmin 固定伺服器角色的成員擁有 hello Database Engine 的完整控制權。</span><span class="sxs-lookup"><span data-stu-id="b0a94-166">Members of hello sysadmin fixed server role have complete control of hello Database Engine.</span></span> <span data-ttu-id="b0a94-167">因此請謹慎限制此角色的成員資格。</span><span class="sxs-lookup"><span data-stu-id="b0a94-167">You should carefully restrict membership in this role.</span></span>
   > 
   > 
   
   ![系統管理員 (sysadmin)](./media/virtual-machines-sql-server-connection-steps/25sysadmin.png)
9. <span data-ttu-id="b0a94-169">按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="b0a94-169">Click OK.</span></span>

<span data-ttu-id="b0a94-170">如需 SQL Server 登入的詳細資訊，請參閱 [建立登入](http://msdn.microsoft.com/library/aa337562.aspx)。</span><span class="sxs-lookup"><span data-stu-id="b0a94-170">For more information about SQL Server logins, see [Create a Login](http://msdn.microsoft.com/library/aa337562.aspx).</span></span>

