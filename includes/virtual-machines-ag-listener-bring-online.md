1. <span data-ttu-id="49582-101">在容錯移轉叢集管理員中，展開 [角色]，然後醒目提示您的可用性群組。</span><span class="sxs-lookup"><span data-stu-id="49582-101">In Failover Cluster Manager, expand **Roles**, and then highlight your availability group.</span></span>  

2. <span data-ttu-id="49582-102">在 hello**資源**索引標籤上，hello 接聽程式名稱，以滑鼠右鍵按一下，然後按一下**屬性**。</span><span class="sxs-lookup"><span data-stu-id="49582-102">On hello **Resources** tab, right-click hello listener name, and then click **Properties**.</span></span>

3. <span data-ttu-id="49582-103">按一下 hello**相依性** 索引標籤。如果列出多個資源，請確認 hello IP 位址具有 OR、 not AND 相依性。</span><span class="sxs-lookup"><span data-stu-id="49582-103">Click hello **Dependencies** tab. If multiple resources are listed, verify that hello IP addresses have OR, not AND, dependencies.</span></span>  

4. <span data-ttu-id="49582-104">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="49582-104">Click **OK**.</span></span>

5. <span data-ttu-id="49582-105">Hello 接聽程式名稱，以滑鼠右鍵按一下，然後按一下**上線**。</span><span class="sxs-lookup"><span data-stu-id="49582-105">Right-click hello listener name, and then click **Bring Online**.</span></span>

6. <span data-ttu-id="49582-106">Hello 之後，接聽程式是在 hello 上線**資源**索引標籤上，hello 可用性群組中，以滑鼠右鍵按一下，然後按一下**屬性**。</span><span class="sxs-lookup"><span data-stu-id="49582-106">After hello listener is online, on hello **Resources** tab, right-click hello availability group, and then click **Properties**.</span></span>
   
    ![設定 hello 可用性群組資源](./media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678772.gif)

7. <span data-ttu-id="49582-108">Hello 接聽程式名稱資源 （不 hello IP 位址資源名稱），建立相依性，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="49582-108">Create a dependency on hello listener name resource (not hello IP address resources name), and then click **OK**.</span></span>
   
    ![Hello 接聽程式名稱上新增相依性](./media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678773.gif)

8. <span data-ttu-id="49582-110">啟動 SQL Server Management Studio，然後連接 toohello 主要複本。</span><span class="sxs-lookup"><span data-stu-id="49582-110">Start SQL Server Management Studio, and then connect toohello primary replica.</span></span>

9. <span data-ttu-id="49582-111">跳過**AlwaysOn 高可用性** > **可用性群組** > **\<AvailabilityGroupName\>**  > **可用性群組接聽程式**。</span><span class="sxs-lookup"><span data-stu-id="49582-111">Go too**AlwaysOn High Availability** > **Availability Groups** > **\<AvailabilityGroupName\>** > **Availability Group Listeners**.</span></span>  
    <span data-ttu-id="49582-112">建立容錯移轉叢集管理員 中的 hello 接聽項名稱應該會顯示。</span><span class="sxs-lookup"><span data-stu-id="49582-112">hello listener name that you created in Failover Cluster Manager should be displayed.</span></span>

10. <span data-ttu-id="49582-113">Hello 接聽程式名稱，以滑鼠右鍵按一下，然後按一下**屬性**。</span><span class="sxs-lookup"><span data-stu-id="49582-113">Right-click hello listener name, and then click **Properties**.</span></span>

11. <span data-ttu-id="49582-114">在 hello**連接埠**方塊中，指定使用 hello 先前所用的 $EndpointPort hello hello 可用性群組接聽程式的連接埠號碼 （在本教學課程，1433年是 hello 預設值），然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="49582-114">In hello **Port** box, specify hello port number for hello availability group listener by using hello $EndpointPort that you used earlier (in this tutorial, 1433 was hello default), and then click **OK**.</span></span>

