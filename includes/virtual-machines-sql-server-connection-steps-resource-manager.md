### <a name="configure-a-dns-label-for-hello-public-ip-address"></a>設定 DNS 標籤 hello 公用 IP 位址

tooconnect toohello SQL Server Database Engine 從 hello 網際網路，請考慮建立 DNS 索引標籤的公用 IP 位址。 您可以連線的 IP 位址，但 hello DNS 標籤建立 A 記錄，更容易 tooidentify 並摘要 hello 基礎公用 IP 位址。

> [!NOTE]
> 如果您計劃 tooonly 連接 toohello SQL Server 執行個體 hello 相同 DNS 標籤不需要虛擬網路或只會在本機。

先選取 toocreate DNS 標籤**虛擬機器**hello 入口網站中。 選取您的 SQL Server VM toobring 其內容。

1. 在 [hello 虛擬機器概觀] 中，選取您**公用 IP 位址**。

    ![公用 IP 位址](./media/virtual-machines-sql-server-connection-steps/rm-public-ip-address.png)

1. 在您的公用 IP 位址的 hello 屬性，依序展開**組態**。

1. 輸入 DNS 標籤名稱。 這個名稱是可以直接是使用的 tooconnect tooyour SQL Server VM 的名稱而不是使用 IP 位址的 A 記錄。

1. 按一下 hello**儲存** 按鈕。

    ![DNS 標籤](./media/virtual-machines-sql-server-connection-steps/rm-dns-label.png)

### <a name="connect-toohello-database-engine-from-another-computer"></a>從另一部電腦連接 toohello Database Engine

1. 在電腦上連接 toohello 網際網路上，開啟 SQL Server Management Studio (SSMS)。 如果您沒有 SQL Server Management Studio，您可以在[這裡](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)下載。

1. 在 hello**連接 tooServer**或**連接 tooDatabase 引擎**對話方塊中，編輯 hello**伺服器名稱**值。 輸入 hello IP 位址或 hello （決定 hello 先前工作中） 的虛擬機器的完整 DNS 名稱。 您也可以新增逗號並提供 SQL Server 的 TCP 連接埠。 例如： `mysqlvmlabel.eastus.cloudapp.azure.com,1433`。

1. 在 hello**驗證**方塊中，選取**SQL Server 驗證**。

1. 在 [hello**登入**] 方塊中，輸入 hello 名稱的有效 SQL 登入。

1. 在 [hello**密碼**] 方塊中，輸入 hello 密碼 hello 登入。

1. 按一下 [ **連接**]。

    ![SSMS 連線](./media/virtual-machines-sql-server-connection-steps/rm-ssms-connect.png)