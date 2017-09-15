<span data-ttu-id="a769c-101">在此步驟中，您會建立防火牆規則來開啟負載平衡端點用的探查連接埠 (59999，如先前所指定)，以及建立另一個規則來開啟可用性群組接聽程式連接埠。</span><span class="sxs-lookup"><span data-stu-id="a769c-101">In this step, you create a firewall rule to open the probe port for the load-balanced endpoint (59999, as specified earlier) and another rule to open the availability group listener port.</span></span> <span data-ttu-id="a769c-102">因為您在包含可用性群組複本的 VM 上建立了負載平衡的端點，您必須在個別 VM 上開啟探查連接埠和接聽程式連接埠。</span><span class="sxs-lookup"><span data-stu-id="a769c-102">Because you created the load-balanced endpoint on the VMs that contain availability group replicas, you need to open the probe port and the listener port on the respective VMs.</span></span>

1. <span data-ttu-id="a769c-103">在裝載複本的 VM 上，啟動 [具有進階安全性的 Windows 防火牆]。</span><span class="sxs-lookup"><span data-stu-id="a769c-103">On VMs that host replicas, start **Windows Firewall with Advanced Security**.</span></span>

2. <span data-ttu-id="a769c-104">以滑鼠右鍵按一下 [輸入規則]，然後按一下 [新增規則]。</span><span class="sxs-lookup"><span data-stu-id="a769c-104">Right-click **Inbound Rules**, and then click **New Rule**.</span></span>

3. <span data-ttu-id="a769c-105">在 [規則類型] 頁面上，選取 [連接埠]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="a769c-105">On the **Rule Type** page, select **Port**, and then click **Next**.</span></span>

4. <span data-ttu-id="a769c-106">在 [通訊協定與連接埠] 頁面上，選取 [TCP]，然後在 [特定本機連接埠] 方塊中輸入 [59999]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="a769c-106">On the **Protocol and Ports** page, select **TCP**, type **59999** in the **Specific local ports** box, and then click **Next**.</span></span>

5. <span data-ttu-id="a769c-107">在 [動作] 頁面上，保持選取 [允許連線]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="a769c-107">On the **Action** page, keep **Allow the connection** selected, and then click **Next**.</span></span>

6. <span data-ttu-id="a769c-108">在 [設定檔] 頁面上，接受預設設定，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="a769c-108">On the **Profile** page, accept the default settings, and then click **Next**.</span></span>

7. <span data-ttu-id="a769c-109">在 [名稱] 頁面的 [名稱] 文字方塊中，指定規則名稱，例如 [AlwaysOn 接聽程式探查連接埠]，然後按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="a769c-109">On the **Name** page, in the **Name** text box, specify a rule name, such as **Always On Listener Probe Port**, and then click **Finish**.</span></span>

8. <span data-ttu-id="a769c-110">針對可用性群組接聽程式連接埠 (如稍早在指令碼的 $EndpointPort 參數中指定) 重複前述步驟，然後指定適當的規則名稱，例如 **AlwaysOn 接聽程式連接埠**。</span><span class="sxs-lookup"><span data-stu-id="a769c-110">Repeat the preceding steps for the availability group listener port (as specified earlier in the $EndpointPort parameter of the script), and then specify an appropriate rule name, such as **Always On Listener Port**.</span></span>

