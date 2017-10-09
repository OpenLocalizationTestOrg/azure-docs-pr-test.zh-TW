### <a name="create-a-tcp-endpoint-for-hello-virtual-machine"></a>建立 hello 虛擬機器的 TCP 端點
順序 tooaccess hello 從 SQL Server 在網際網路、 hello 虛擬機器必須能夠端點 toolisten，內送 TCP 通訊。 這個 Azure 組態步驟，指示內送 TCP 連接埠流量 tooa TCP 通訊埠是可存取 toohello 虛擬機器。

> [!NOTE]
> 如果您要在 hello 連接相同雲端服務或虛擬網路，您不需要 toocreate 可公開存取的端點。 在此情況下，您無法繼續 toohello 下一個步驟。 如需詳細資訊，請參閱[連接案例](../articles/virtual-machines/windows/sqlclassic/virtual-machines-windows-classic-sql-connect.md#connection-scenarios)。
> 
> 

1. 在 hello Azure 入口網站，選取 **虛擬機器 （傳統）**。
2. 然後選取您的 SQL Server 虛擬機器。
3. 選取**端點**，然後按一下hello**新增**在 hello hello 端點刀鋒視窗頂端的按鈕。
   
    ![建立端點的入口網站步驟](./media/virtual-machines-sql-server-connection-steps/portal-endpoint-creation.png)
4. 在 hello**加入端點**刀鋒視窗中，提供**名稱**SQLEndpoint 等。
5. 選取**TCP** hello**通訊協定**。
6. 對於 [公用連接埠]，請指定連接埠號碼，例如 **57500**。
7. 如**私用連接埠**，指定 SQL Server 接聽連接埠，其預設太**1433年**。
8. 按一下**確定**toocreate hello 端點。

