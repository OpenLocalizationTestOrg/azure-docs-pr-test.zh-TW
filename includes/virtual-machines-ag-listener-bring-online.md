1. 在容錯移轉叢集管理員中，展開 [角色]，然後醒目提示您的可用性群組。  

2. 在 hello**資源**索引標籤上，hello 接聽程式名稱，以滑鼠右鍵按一下，然後按一下**屬性**。

3. 按一下 hello**相依性** 索引標籤。如果列出多個資源，請確認 hello IP 位址具有 OR、 not AND 相依性。  

4. 按一下 [確定] 。

5. Hello 接聽程式名稱，以滑鼠右鍵按一下，然後按一下**上線**。

6. Hello 之後，接聽程式是在 hello 上線**資源**索引標籤上，hello 可用性群組中，以滑鼠右鍵按一下，然後按一下**屬性**。
   
    ![設定 hello 可用性群組資源](./media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678772.gif)

7. Hello 接聽程式名稱資源 （不 hello IP 位址資源名稱），建立相依性，然後按一下**確定**。
   
    ![Hello 接聽程式名稱上新增相依性](./media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678773.gif)

8. 啟動 SQL Server Management Studio，然後連接 toohello 主要複本。

9. 跳過**AlwaysOn 高可用性** > **可用性群組** > **\<AvailabilityGroupName\>**  > **可用性群組接聽程式**。  
    建立容錯移轉叢集管理員 中的 hello 接聽項名稱應該會顯示。

10. Hello 接聽程式名稱，以滑鼠右鍵按一下，然後按一下**屬性**。

11. 在 hello**連接埠**方塊中，指定使用 hello 先前所用的 $EndpointPort hello hello 可用性群組接聽程式的連接埠號碼 （在本教學課程，1433年是 hello 預設值），然後按一下**確定**。

