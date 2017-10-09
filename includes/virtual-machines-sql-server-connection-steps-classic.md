### <a name="determine-hello-dns-name-of-hello-virtual-machine"></a>判斷 hello hello 虛擬機器的 DNS 名稱
tooconnect toohello SQL Server Database Engine 從另一部電腦，您必須知道 hello 網域名稱系統 (DNS) hello 虛擬機器的名稱。 （這是 hello 名稱 hello 網際網路使用 tooidentify hello 虛擬機器。 您可以使用 hello IP 位址，但當 Azure 基於冗餘或維護移動資源時，可能會變更 hello IP 位址。 hello DNS 名稱將會是穩定，因為它可能會重新導向 tooa 新的 IP 位址。)  

1. 在 hello Azure 入口網站 （或從 hello 上一個步驟），選取**虛擬機器 （傳統）**。
2. 選取您的 SQL VM。
3. 在 hello**虛擬機器**刀鋒視窗，複製 hello **DNS 名稱**hello 虛擬機器。
   
    ![DNS 名稱](./media/virtual-machines-sql-server-connection-steps/sql-vm-dns-name.png)

### <a name="connect-toohello-database-engine-from-another-computer"></a>從另一部電腦連接 toohello Database Engine
1. 在電腦上連接 toohello 網際網路上，開啟 SQL Server Management Studio。
2. 在 hello**連接 tooServer**或**連接 tooDatabase 引擎**對話方塊中的，在 hello**伺服器名稱**方塊中，輸入 hello 虛擬機器 （決定 hello hello DNS 名稱前一項工作） 和公用端點連接埠號碼格式的 hello *DNSName，portnumber*例如**mysqlvm.cloudapp.net,57500**。
   
    ![使用 SSMS 進行連線](./media/virtual-machines-sql-server-connection-steps/33Connect-SSMS.png)
   
    如果您不記得 hello 公用端點連接埠號碼先前所建立，您可以在 hello**端點**區域 hello**虛擬機器**刀鋒視窗。
   
    ![公用連接埠](./media/virtual-machines-sql-server-connection-steps/sql-vm-port-number.png)
3. 在 hello**驗證**方塊中，選取**SQL Server 驗證**。
4. 在 hello**登入**中，輸入您在稍早的工作中建立登入的 hello 名稱。
5. 在 [hello**密碼**] 方塊中，輸入 hello 密碼 hello 登入您在稍早的工作中建立。
6. 按一下 [ **連接**]。

