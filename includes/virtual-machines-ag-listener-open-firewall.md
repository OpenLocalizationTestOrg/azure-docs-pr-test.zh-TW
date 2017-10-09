<span data-ttu-id="8d0fd-101">在此步驟中，您可以建立防火牆規則 tooopen hello 探查連接埠用於 hello 負載平衡的端點 (59999，如先前所指定)，而另一個規則 tooopen hello 可用性群組接聽程式連接埠。</span><span class="sxs-lookup"><span data-stu-id="8d0fd-101">In this step, you create a firewall rule tooopen hello probe port for hello load-balanced endpoint (59999, as specified earlier) and another rule tooopen hello availability group listener port.</span></span> <span data-ttu-id="8d0fd-102">因為您已建立包含可用性群組複本的 Vm hello hello 負載平衡的端點，您需要 tooopen hello 探查連接埠和接聽程式連接埠 hello hello 各自的 Vm。</span><span class="sxs-lookup"><span data-stu-id="8d0fd-102">Because you created hello load-balanced endpoint on hello VMs that contain availability group replicas, you need tooopen hello probe port and hello listener port on hello respective VMs.</span></span>

1. <span data-ttu-id="8d0fd-103">在裝載複本的 VM 上，啟動 [具有進階安全性的 Windows 防火牆]。</span><span class="sxs-lookup"><span data-stu-id="8d0fd-103">On VMs that host replicas, start **Windows Firewall with Advanced Security**.</span></span>

2. <span data-ttu-id="8d0fd-104">以滑鼠右鍵按一下 輸入規則，然後按一下新增規則。</span><span class="sxs-lookup"><span data-stu-id="8d0fd-104">Right-click **Inbound Rules**, and then click **New Rule**.</span></span>

3. <span data-ttu-id="8d0fd-105">在 [hello**規則類型**頁面上，選取**連接埠**，然後按一下**下一步]**。</span><span class="sxs-lookup"><span data-stu-id="8d0fd-105">On hello **Rule Type** page, select **Port**, and then click **Next**.</span></span>

4. <span data-ttu-id="8d0fd-106">在 hello**通訊協定和連接埠**頁面上，選取**TCP**，型別**59999**在 hello**特定本機連接埠**方塊，然後再按一下  **下一步**。</span><span class="sxs-lookup"><span data-stu-id="8d0fd-106">On hello **Protocol and Ports** page, select **TCP**, type **59999** in hello **Specific local ports** box, and then click **Next**.</span></span>

5. <span data-ttu-id="8d0fd-107">在 hello**動作**頁面上，保留**允許 hello 連線**選取，然後再按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="8d0fd-107">On hello **Action** page, keep **Allow hello connection** selected, and then click **Next**.</span></span>

6. <span data-ttu-id="8d0fd-108">在 hello**設定檔**頁面上，接受 hello 預設設定，然後按**下一步**。</span><span class="sxs-lookup"><span data-stu-id="8d0fd-108">On hello **Profile** page, accept hello default settings, and then click **Next**.</span></span>

7. <span data-ttu-id="8d0fd-109">在 hello**名稱** 頁面的 hello**名稱**文字方塊中，指定規則的名稱，例如**一定在接聽程式探查連接埠**，然後按一下**完成**。</span><span class="sxs-lookup"><span data-stu-id="8d0fd-109">On hello **Name** page, in hello **Name** text box, specify a rule name, such as **Always On Listener Probe Port**, and then click **Finish**.</span></span>

8. <span data-ttu-id="8d0fd-110">重複先前步驟 hello 可用性群組接聽程式連接埠 （如指定稍早在 hello $EndpointPort hello 指令碼參數中），hello，然後指定適當的規則名稱，例如**一定在接聽程式通訊埠**。</span><span class="sxs-lookup"><span data-stu-id="8d0fd-110">Repeat hello preceding steps for hello availability group listener port (as specified earlier in hello $EndpointPort parameter of hello script), and then specify an appropriate rule name, such as **Always On Listener Port**.</span></span>

