1. 遠端桌面連線的 toohello 虛擬機器，同時搜尋**Configuration Manager**:

    ![開啟 SSCM](./media/virtual-machines-sql-server-connection-tcp-protocol/sql-server-configuration-manager.png)

1. 在 「 SQL Server 組態管理員 」 中，在 [hello] 主控台窗格中，展開**SQL Server 網路組態**。

1. Hello 主控台窗格中，按一下  **MSSQLSERVER 的通訊協定**（hello 預設執行個體名稱）。在 hello 詳細資料窗格中，以滑鼠右鍵按一下**TCP**按一下**啟用**如果尚未啟用。

    ![啟用 TCP](./media/virtual-machines-sql-server-connection-tcp-protocol/enable-tcp.png)

1. Hello 主控台窗格中，按一下  **SQL Server 服務**。 在 [hello] 詳細資料窗格中，以滑鼠右鍵按一下 **SQL Server (*執行個體名稱*) * * (hello 預設執行個體是**SQL Server (MSSQLSERVER)**)，然後按一下**重新啟動**，toostop 並重新啟動 hello SQL Server 執行個體。

    ![重新啟動 Database Engine](./media/virtual-machines-sql-server-connection-tcp-protocol/restart-sql-server.png)

1. 關閉 SQL Server 組態管理員。

如需啟用通訊協定 hello SQL Server Database Engine 的詳細資訊，請參閱[啟用或停用伺服器網路通訊協定](http://msdn.microsoft.com/library/ms191294.aspx)。
