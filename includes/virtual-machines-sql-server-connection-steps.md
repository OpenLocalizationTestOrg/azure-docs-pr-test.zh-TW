### <a name="open-tcp-ports-in-hello-windows-firewall-for-hello-default-instance-of-hello-database-engine"></a>Hello hello 的 hello Database Engine 的預設執行個體的 Windows 防火牆中開啟 TCP 通訊埠
1. 使用遠端桌面連線 toohello 虛擬機器。 連接 toohello VM 連接的詳細指示，請參閱[開啟遠端桌面的 SQL VM](../articles/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision.md#open-the-vm-with-remote-desktop)。
2. 一旦登入，在 hello 開始畫面，輸入**WF.msc**，然後按 enter 鍵。
   
    ![啟動防火牆程式 hello](./media/virtual-machines-sql-server-connection-steps/12Open-WF.png)
3. 在 hello**具有進階安全性的 Windows 防火牆**，在 [hello 左的窗格中以滑鼠右鍵按一下**輸入規則**，然後按一下**新規則**hello 動作] 窗格中。
   
    ![新增規則](./media/virtual-machines-sql-server-connection-steps/13New-FW-Rule.png)
4. 在 hello**新增輸入規則精靈**對話方塊的 **規則類型**，選取**連接埠**，然後按一下**下一步**。
5. 在 hello**通訊協定和連接埠**對話方塊中，使用 hello 預設**TCP**。 在 [hello**特定本機連接埠**] 方塊中，則型別 hello 連接埠號碼 hello hello Database Engine 執行個體 (**1433年**hello 預設執行個體，或您選擇的 hello hello 端點步驟中的私用連接埠)。
   
    ![TCP 連接埠 1433](./media/virtual-machines-sql-server-connection-steps/14Port-1433.png)
6. 按一下 [下一步] 。
7. 在 hello**動作**對話方塊中，選取**允許 hello 連線**，然後按一下**下一步**。
   
    **安全性注意事項：**選取**允許 hello 連線是否安全**可以提供額外的安全性。 如果您要在您的環境中的 tooconfigure 額外的安全性選項，請選取此選項。
   
    ![允許連線](./media/virtual-machines-sql-server-connection-steps/15Allow-Connection.png)
8. 在 hello**設定檔**對話方塊中，選取**公用**，**私人**，和**網域**。 然後按 [下一步] 。
   
    **安全性注意事項：**選取**公用**允許存取透過 hello 網際網路。 請盡可能選取較具有限制性的設定檔。
   
    ![公用設定檔](./media/virtual-machines-sql-server-connection-steps/16Public-Private-Domain-Profile.png)
9. 在 hello**名稱**對話方塊中，輸入名稱和描述，此規則，然後按一下**完成**。
   
    ![規則名稱](./media/virtual-machines-sql-server-connection-steps/17Rule-Name.png)

視需要為其他元件開啟額外的連接埠。 如需詳細資訊，請參閱[設定 hello SQL Server 存取的 Windows 防火牆 tooAllow](http://msdn.microsoft.com/library/cc646023.aspx)。

### <a name="configure-sql-server-toolisten-on-hello-tcp-protocol"></a>設定 SQL Server toolisten hello TCP 通訊協定

[!INCLUDE [Enable TCP](virtual-machines-sql-server-connection-tcp-protocol.md)]

### <a name="configure-sql-server-for-mixed-mode-authentication"></a>設定 SQL Server 以進行混合模式驗證
hello SQL Server Database Engine 無法使用 Windows 驗證，若沒有網域環境。 tooconnect toohello Database Engine 從另一部電腦，設定 SQL Server 混合的模式驗證。 混合模式驗證可允許 SQL Server 驗證和 Windows 驗證。

> [!NOTE]
> 如果您已經設定具有已設定網域環境的 Azure 虛擬網路，可能就不需要設定混合模式驗證。
> 
> 

1. 同時連接的 toohello 虛擬機器，在 hello 開始頁面上，輸入**SQL Server Management Studio**按一下 hello 選的圖示。
   
    hello 第一次開啟 Management Studio，就必須建立 hello 使用者 Management Studio 環境。 這可能需要花費幾分鐘的時間。
2. Management Studio 顯示 hello**連接 tooServer**  對話方塊。 在 hello**伺服器名稱** 方塊中，輸入 hello 名稱 hello 虛擬機器 tooconnect toohello Database Engine 以 hello 物件總管 中的 (而不是 hello 虛擬機器名稱，您也可以使用**（本機）**或單一句號為 hello**伺服器名稱**)。 選取**Windows 驗證**，並將保留 ***your_VM_name*\your_local_administrator**在 hello**使用者名**方塊。 按一下 [ **連接**]。
   
    ![連接 tooServer](./media/virtual-machines-sql-server-connection-steps/19Connect-to-Server.png)
3. SQL Server Management Studio 物件總管，在 hello hello （hello 虛擬機器名稱） 的 SQL Server 執行個體名稱上按一下滑鼠右鍵，然後按一下**屬性**。
   
    ![伺服器屬性](./media/virtual-machines-sql-server-connection-steps/20Server-Properties.png)
4. Hello 上**安全性**頁面的 **伺服器驗證**，選取**SQL Server 及 Windows 驗證模式**，然後按一下**確定**.
   
    ![選取驗證模式](./media/virtual-machines-sql-server-connection-steps/21Mixed-Mode.png)
5. 在 hello SQL Server Management Studio 對話方塊中，按一下 **確定**tooacknowledge hello 需求 toorestart SQL Server。
6. 在物件總管中，以滑鼠右鍵按一下伺服器，然後按一下重新啟動。 (如果 SQL Server Agent 處於執行狀態，您也必須將其重新啟動。)
   
    ![重新啟動](./media/virtual-machines-sql-server-connection-steps/22Restart2.png)
7. 在 hello SQL Server Management Studio 對話方塊中，按一下 **是**tooagree 想 toorestart SQL Server。

### <a name="create-sql-server-authentication-logins"></a>建立 SQL Server 驗證登入
tooconnect toohello Database Engine 從另一部電腦，您必須建立至少一個 SQL Server 驗證登入。

1. 在 SQL Server Management Studio 物件總管 中，展開 hello 資料夾 hello 想 toocreate hello 新登入的伺服器執行個體。
2. 以滑鼠右鍵按一下 hello**安全性**資料夾中，點太**新增**，然後選取**登入...**.
   
    ![新增登入](./media/virtual-machines-sql-server-connection-steps/23New-Login.png)
3. 在 hello**登入-新增** 對話方塊上 hello**一般**頁面上，輸入 hello hello 新使用者名稱中 hello**登入名稱**方塊。
4. 選取 [SQL Server 驗證] 。
5. 在 hello**密碼**方塊中，輸入 hello 新使用者的密碼。 該密碼一次輸入 hello**確認密碼**方塊。
6. 選取所需的 hello 密碼強制執行選項 (**強制執行密碼原則**，**強制執行密碼逾期**，和**使用者必須變更密碼，在下次登入時**)。 如果您自行使用此登入，您不需要的 toorequire 在 hello 下次登入時變更密碼。
7. 從 hello**預設資料庫**清單中，選取 hello 登入的預設資料庫。 **主要**hello 預設值，這個選項。 如果您尚未建立使用者資料庫，將這個資料集太**主要**。
   
    ![登入屬性](./media/virtual-machines-sql-server-connection-steps/24Test-Login.png)
8. 如果這是您要建立 hello 第一個登入，您可能想 toodesignate 此登入 SQL Server 系統管理員身分。 如果是這樣，在 hello**伺服器角色**頁面上，核取**sysadmin**。
   
   > [!NOTE]
   > Hello sysadmin 固定伺服器角色的成員擁有 hello Database Engine 的完整控制權。 因此請謹慎限制此角色的成員資格。
   > 
   > 
   
   ![系統管理員 (sysadmin)](./media/virtual-machines-sql-server-connection-steps/25sysadmin.png)
9. 按一下 [確定]。

如需 SQL Server 登入的詳細資訊，請參閱 [建立登入](http://msdn.microsoft.com/library/aa337562.aspx)。

