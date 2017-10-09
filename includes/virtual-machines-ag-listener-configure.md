hello 可用性群組接聽程式是 hello SQL Server 可用性群組接聽的 IP 位址和網路名稱。 toocreate hello 可用性群組接聽程式，請勿 hello 遵循：

1. <a name="getnet"></a>收到 hello hello 叢集網路資源名稱。

    a. 使用 RDP tooconnect toohello 裝載 hello 主要複本的 Azure 虛擬機器。 

    b. 開始容錯移轉叢集管理員。

    c. 選取 hello**網路**節點，然後注意 hello 叢集網路名稱。 使用此名稱在 hello `$ClusterNetworkName` hello PowerShell 指令碼中的變數。 下列影像 hello 叢集網路名稱是在 hello**叢集網路 1**:

   ![叢集網路名稱](./media/virtual-machines-ag-listener-configure/90-clusternetworkname.png)

2. <a name="addcap"></a>加入 hello 用戶端存取點。  
    hello 用戶端存取點是應用程式使用 tooconnect toohello 資料庫可用性群組中的 hello 網路名稱。 在 [容錯移轉叢集管理員] 中建立 hello 用戶端存取點。

    a. 展開 hello 叢集名稱，然後按一下**角色**。

    b. 在 hello**角色**窗格中，以滑鼠右鍵按一下 hello 可用性群組名稱，然後再選取**加入資源** > **用戶端存取點**。

   ![用戶端存取點](./media/virtual-machines-ag-listener-configure/92-addclientaccesspoint.png)

    c. 在 hello**名稱**方塊中，建立新的接聽程式的名稱。 
   hello hello 新的接聽程式名稱是應用程式使用 tooconnect toodatabases hello SQL Server 可用性群組中的 hello 網路名稱。
   
    d. toofinish 建立 hello 接聽程式，按一下**下一步**兩次，然後按一下**完成**。 請勿讓 hello 接聽程式或資源上線此時。

3. <a name="congroup"></a>設定 hello 可用性群組的 hello IP 資源。

    a. 按一下 hello**資源**索引標籤，然後再展開您建立 hello 用戶端存取點。  
    hello 用戶端存取點處於離線狀態。

   ![用戶端存取點](./media/virtual-machines-ag-listener-configure/94-newclientaccesspoint.png) 

    b. Hello IP 資源，以滑鼠右鍵按一下，然後按一下屬性。 請注意 hello 名稱 hello IP 位址，並將它用於 hello `$IPResourceName` hello PowerShell 指令碼中的變數。

    c. 在 [IP 地址] 下，按一下 [靜態 IP 位址]。 與 hello 相同位址，使用 hello Azure 入口網站上設定 hello 負載平衡器位址時，請設定 hello IP 位址。

   ![IP 資源](./media/virtual-machines-ag-listener-configure/96-ipresource.png) 

    <!-----------------------I don't see this option on server 2016
    1. Disable NetBIOS for this address and click **OK**. Repeat this step for each IP resource if your solution spans multiple Azure VNets. 
    ------------------------->

4. <a name = "dependencyGroup"></a>讓 hello SQL Server 可用性群組資源相依於 hello 用戶端存取點。

    a. 在 [容錯移轉叢集管理員] 中，按一下 [角色]，然後按一下您的 [可用性群組]。

    b. 在 hello**資源**索引標籤，在**其他資源**hello 可用性資源群組中，以滑鼠右鍵按一下，然後按**屬性**。 

    c. Hello 相依性 索引標籤上新增 hello hello 用戶端存取點 （hello 接聽程式） 的資源名稱。

   ![IP 資源](./media/virtual-machines-ag-listener-configure/97-propertiesdependencies.png) 

    d. 按一下 [確定] 。

5. <a name="listname"></a>使 hello 用戶端存取點依存於 hello IP 位址資源。

    a. 在 [容錯移轉叢集管理員] 中，按一下 [角色]，然後按一下您的 [可用性群組]。 

    b. 在 hello**資源**索引標籤上，以滑鼠右鍵按一下 hello 用戶端存取點資源下的**伺服器名稱**，然後按一下**屬性**。 

   ![IP 資源](./media/virtual-machines-ag-listener-configure/98-dependencies.png) 

    c. 按一下 hello**相依性** 索引標籤。請確認 hello IP 位址相依性。 如果不是，設定 hello IP 位址相依性。 如果有多個資源列出，請確認 hello IP 位址具有 OR、 not AND 相依性。 按一下 [確定] 。 

   ![IP 資源](./media/virtual-machines-ag-listener-configure/98-propertiesdependencies.png) 

    d. Hello 接聽程式名稱，以滑鼠右鍵按一下，然後按一下**上線**。 

    >[!TIP]
    >您可以驗證相依性已正確設定該 hello。 在 [容錯移轉叢集管理員] 中，移 tooRoles、 hello 可用性群組上按一下滑鼠右鍵、 按一下**其他動作**，然後按一下**顯示相依性報告**。 Hello 相依性已正確設定，hello 可用性群組是依存於 hello 網路名稱，而 hello 網路名稱是取決於 hello IP 位址。 


6. <a name="setparam"></a>在 PowerShell 中設定 hello 叢集參數。
    
    a. 複製下列 SQL Server 執行個體的 PowerShell 指令碼 tooone hello。 更新您的環境的 hello 變數。     
    
    ```PowerShell
    $ClusterNetworkName = "<MyClusterNetworkName>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name)
    $IPResourceName = "<IPResourceName>" # hello IP Address resource name
    $ILBIP = “<n.n.n.n>” # hello IP Address of hello Internal Load Balancer (ILB). This is hello static IP address for hello load balancer you configured in hello Azure portal.
    [int]$ProbePort = <nnnnn>
    
    Import-Module FailoverClusters
    
    Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"=$ProbePort;"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}
    ```

    b. 其中一個 hello 叢集節點上執行 hello PowerShell 指令碼，以設定 hello 叢集參數。  

    > [!NOTE]
    > 如果您的 SQL Server 執行個體位於不同的區域中，您需要 toorun hello PowerShell 指令碼兩次。 hello 第一次，請使用 hello`$ILBIP`和`$ProbePort`hello 第一個區域中。 hello 第二次，請使用 hello`$ILBIP`和`$ProbePort`從 hello 第二個區域。 hello 叢集網路名稱和 hello 叢集 IP 資源名稱是 hello 相同。 
