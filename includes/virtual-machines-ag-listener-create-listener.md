在此步驟中，您可以手動建立容錯移轉叢集管理員和 SQL Server Management Studio 中的 hello 可用性群組接聽程式。

1. 開啟 容錯移轉叢集管理員從裝載主要複本的 hello hello 節點。

2. 選取 hello**網路**節點，然後注意 hello 叢集網路名稱。 Hello PowerShell 指令碼中的 hello $ClusterNetworkName 變數中，會使用此名稱。

3. 展開 hello 叢集名稱，然後按一下**角色**。

4. 在 hello**角色**窗格中，以滑鼠右鍵按一下 hello 可用性群組名稱，然後再選取**加入資源** > **用戶端存取點**。
   
    ![新增可用性群組的用戶端存取點](./media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678769.gif)

5. 在 hello**名稱**，建立新的接聽程式的名稱，按一下**下一步**兩次，然後按一下**完成**。  
    請勿讓 hello 接聽程式或資源上線此時。

6. 按一下 hello**資源**索引標籤，然後再展開您剛才建立的 hello 用戶端存取點。 
    會顯示 hello 叢集中的每個叢集網路的 IP 位址資源。 如果這是僅限 Azure 的解決方案，只會顯示一個 IP 位址資源。

7. 執行 hello 下列其中一項：
   
   * tooconfigure 混合式解決方案：
     
        a. 以滑鼠右鍵按一下 hello 對應 tooyour 在內部部署子網路，IP 位址資源，然後選取**屬性**。 請注意 hello IP 位址名稱和網路名稱。
   
        b. 選取 靜態 IP 位址、指派未使用的 IP 位址，然後按一下確定。
 
   * tooconfigure 僅 Azure 」 的方案：

        a. 以滑鼠右鍵按一下 hello 對應 tooyour Azure 子網路，IP 位址資源，然後選取**屬性**。
       
       > [!NOTE]
       > 如果稍後 hello 接聽程式會因為衝突的 IP 位址，DHCP 所選取的失敗 toocome 線上，您可以設定此屬性 視窗中的有效靜態 IP 位址。
       > 
       > 

       b. 在 hello 相同**IP 位址**屬性視窗中，變更 hello **IP 位址名稱**。  
        在 hello $IPResourceName 變數中的 hello PowerShell 指令碼會使用此名稱。 如果您的解決方案跨越多個 Azure 虛擬網路，請針對每個 IP 資源重複此步驟。

