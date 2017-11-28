1. <span data-ttu-id="28a27-101">在容錯移轉叢集管理員中，展開 [角色]，然後醒目提示您的可用性群組。</span><span class="sxs-lookup"><span data-stu-id="28a27-101">In Failover Cluster Manager, expand **Roles**, and then highlight your availability group.</span></span>  

2. <span data-ttu-id="28a27-102">在 [資源] 索引標籤上，以滑鼠右鍵按一下接聽程式名稱，然後按一下 [屬性]。</span><span class="sxs-lookup"><span data-stu-id="28a27-102">On the **Resources** tab, right-click the listener name, and then click **Properties**.</span></span>

3. <span data-ttu-id="28a27-103">按一下 [相依性]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="28a27-103">Click the **Dependencies** tab.</span></span> <span data-ttu-id="28a27-104">如果列出多個資源，請確認 IP 位址具有 OR (而非 AND) 相依性。</span><span class="sxs-lookup"><span data-stu-id="28a27-104">If multiple resources are listed, verify that the IP addresses have OR, not AND, dependencies.</span></span>  

4. <span data-ttu-id="28a27-105">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="28a27-105">Click **OK**.</span></span>

5. <span data-ttu-id="28a27-106">以滑鼠右鍵按一下接聽程式名稱，然後按一下 [上線]。</span><span class="sxs-lookup"><span data-stu-id="28a27-106">Right-click the listener name, and then click **Bring Online**.</span></span>

6. <span data-ttu-id="28a27-107">接聽程式上線後，在 [資源] 索引標籤上，以滑鼠右鍵按一下可用性群組，然後按一下 [屬性]。</span><span class="sxs-lookup"><span data-stu-id="28a27-107">After the listener is online, on the **Resources** tab, right-click the availability group, and then click **Properties**.</span></span>
   
    ![設定可用性群組資源](./media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678772.gif)

7. <span data-ttu-id="28a27-109">建立對接聽程式名稱資源 (非 IP 位址資源名稱) 的相依性，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="28a27-109">Create a dependency on the listener name resource (not the IP address resources name), and then click **OK**.</span></span>
   
    ![新增對接聽程式名稱的相依性](./media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678773.gif)

8. <span data-ttu-id="28a27-111">啟動 SQL Server Management Studio，然後連線到主要複本。</span><span class="sxs-lookup"><span data-stu-id="28a27-111">Start SQL Server Management Studio, and then connect to the primary replica.</span></span>

9. <span data-ttu-id="28a27-112">移至 [AlwaysOn 高可用性] > [可用性群組] > [\<AvailabilityGroupName\>] > [可用性群組接聽程式]。</span><span class="sxs-lookup"><span data-stu-id="28a27-112">Go to **AlwaysOn High Availability** > **Availability Groups** > **\<AvailabilityGroupName\>** > **Availability Group Listeners**.</span></span>  
    <span data-ttu-id="28a27-113">您在容錯移轉叢集管理員中建立的接聽程式名稱應會顯示。</span><span class="sxs-lookup"><span data-stu-id="28a27-113">The listener name that you created in Failover Cluster Manager should be displayed.</span></span>

10. <span data-ttu-id="28a27-114">以滑鼠右鍵按一下接聽程式名稱，然後按一下 [屬性]。</span><span class="sxs-lookup"><span data-stu-id="28a27-114">Right-click the listener name, and then click **Properties**.</span></span>

11. <span data-ttu-id="28a27-115">在 [連接埠] 方塊中，使用您稍早所用的 $EndpointPort 來指定可用性群組接聽程式的連接埠號碼 (在本教學課程中，預設值為 1433)，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="28a27-115">In the **Port** box, specify the port number for the availability group listener by using the $EndpointPort that you used earlier (in this tutorial, 1433 was the default), and then click **OK**.</span></span>

