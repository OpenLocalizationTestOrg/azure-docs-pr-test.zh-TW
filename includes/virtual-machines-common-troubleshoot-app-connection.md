<span data-ttu-id="ff93d-101">有各種原因會造成無法啟動或連接至在 Azure 虛擬機器 (VM) 上執行的應用程式。</span><span class="sxs-lookup"><span data-stu-id="ff93d-101">There are various reasons when you cannot start or connect to an application running on an Azure virtual machine (VM).</span></span> <span data-ttu-id="ff93d-102">原因包括應用程式並未執行，或未在預期的連接埠上接聽，接聽連接埠遭到封鎖，或網路規則未正確將流量傳遞至應用程式。</span><span class="sxs-lookup"><span data-stu-id="ff93d-102">Reasons include the application not running or listening on the expected ports, the listening port blocked, or networking rules not correctly passing traffic to the application.</span></span> <span data-ttu-id="ff93d-103">本文說明條理式方法，以找出並更正問題。</span><span class="sxs-lookup"><span data-stu-id="ff93d-103">This article describes a methodical approach to find and correct the problem.</span></span>

<span data-ttu-id="ff93d-104">如果您在使用 RDP 或 SSH 連接到 VM 時發生問題，請先參閱下列其中一篇文章︰</span><span class="sxs-lookup"><span data-stu-id="ff93d-104">If you are having issues connecting to your VM using RDP or SSH, see one of the following articles first:</span></span>

* [<span data-ttu-id="ff93d-105">針對以 Windows 為基礎的 Azure 虛擬機器的遠端桌面連線進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="ff93d-105">Troubleshoot Remote Desktop connections to a Windows-based Azure Virtual Machine</span></span>](../articles/virtual-machines/windows/troubleshoot-rdp-connection.md)
* <span data-ttu-id="ff93d-106">[針對以 Linux 為基礎的 Azure 虛擬機器的安全殼層 (SSH) 連線進行疑難排解](../articles/virtual-machines/linux/troubleshoot-ssh-connection.md)。</span><span class="sxs-lookup"><span data-stu-id="ff93d-106">[Troubleshoot Secure Shell (SSH) connections to a Linux-based Azure virtual machine](../articles/virtual-machines/linux/troubleshoot-ssh-connection.md).</span></span>

> [!NOTE]
> <span data-ttu-id="ff93d-107">Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../articles/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="ff93d-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../articles/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="ff93d-108">本文將說明如何使用這兩個模型，但 Microsoft 建議大多數新的部署請使用資源管理員模型。</span><span class="sxs-lookup"><span data-stu-id="ff93d-108">This article covers using both models, but Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="ff93d-109">如果在本文章中有任何需要協助的地方，您可以連絡 [MSDN Azure 和 Stack Overflow 論壇](https://azure.microsoft.com/support/forums/)上的 Azure 專家。</span><span class="sxs-lookup"><span data-stu-id="ff93d-109">If you need more help at any point in this article, you can contact the Azure experts on [the MSDN Azure and the Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="ff93d-110">或者，您也可以提出 Azure 支援事件。</span><span class="sxs-lookup"><span data-stu-id="ff93d-110">Alternatively, you can also file an Azure support incident.</span></span> <span data-ttu-id="ff93d-111">請移至 [Azure 支援網站](https://azure.microsoft.com/support/options/)，然後選取 [取得支援]。</span><span class="sxs-lookup"><span data-stu-id="ff93d-111">Go to the [Azure support site](https://azure.microsoft.com/support/options/) and select **Get Support**.</span></span>

## <a name="quick-start-troubleshooting-steps"></a><span data-ttu-id="ff93d-112">快速入門的疑難排解步驟</span><span class="sxs-lookup"><span data-stu-id="ff93d-112">Quick-start troubleshooting steps</span></span>
<span data-ttu-id="ff93d-113">如果您在連接到應用程式時發生問題，請嘗試下列一般疑難排解步驟。</span><span class="sxs-lookup"><span data-stu-id="ff93d-113">If you have problems connecting to an application, try the following general troubleshooting steps.</span></span> <span data-ttu-id="ff93d-114">請在每個步驟之後，嘗試重新連接到您的應用程式︰</span><span class="sxs-lookup"><span data-stu-id="ff93d-114">After each step, try connecting to your application again:</span></span>

* <span data-ttu-id="ff93d-115">重新啟動虛擬機器</span><span class="sxs-lookup"><span data-stu-id="ff93d-115">Restart the virtual machine</span></span>
* <span data-ttu-id="ff93d-116">重新建立端點/防火牆規則/網路安全性群組 (NSG) 規則</span><span class="sxs-lookup"><span data-stu-id="ff93d-116">Recreate the endpoint / firewall rules / network security group (NSG) rules</span></span>
  * [<span data-ttu-id="ff93d-117">資源管理員模型 - 管理網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="ff93d-117">Resource Manager model - Manage Network Security Groups</span></span>](../articles/virtual-network/virtual-networks-create-nsg-arm-pportal.md)
  * [<span data-ttu-id="ff93d-118">傳統模型 - 管理雲端服務端點</span><span class="sxs-lookup"><span data-stu-id="ff93d-118">Classic model - Manage Cloud Services endpoints</span></span>](../articles/cloud-services/cloud-services-enable-communication-role-instances.md)
* <span data-ttu-id="ff93d-119">從不同的位置 (例如不同的 Azure 虛擬網路) 進行連線</span><span class="sxs-lookup"><span data-stu-id="ff93d-119">Connect from different location, such as a different Azure virtual network</span></span>
* <span data-ttu-id="ff93d-120">重新部署虛擬機器</span><span class="sxs-lookup"><span data-stu-id="ff93d-120">Redeploy the virtual machine</span></span>
  * [<span data-ttu-id="ff93d-121">重新部署 Windows VM</span><span class="sxs-lookup"><span data-stu-id="ff93d-121">Redeploy Windows VM</span></span>](../articles/virtual-machines/windows/redeploy-to-new-node.md)
  * [<span data-ttu-id="ff93d-122">重新部署 Linux VM</span><span class="sxs-lookup"><span data-stu-id="ff93d-122">Redeploy Linux VM</span></span>](../articles/virtual-machines/linux/redeploy-to-new-node.md)
* <span data-ttu-id="ff93d-123">重新建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="ff93d-123">Recreate the virtual machine</span></span>

<span data-ttu-id="ff93d-124">如需詳細資訊，請參閱 [疑難排解端點連接能力 (RDP/SSH/HTTP 等失敗問題)](https://social.msdn.microsoft.com/Forums/azure/en-US/538a8f18-7c1f-4d6e-b81c-70c00e25c93d/troubleshooting-endpoint-connectivity-rdpsshhttp-etc-failures?forum=WAVirtualMachinesforWindows)。</span><span class="sxs-lookup"><span data-stu-id="ff93d-124">For more information, see [Troubleshooting Endpoint Connectivity (RDP/SSH/HTTP, etc. failures)](https://social.msdn.microsoft.com/Forums/azure/en-US/538a8f18-7c1f-4d6e-b81c-70c00e25c93d/troubleshooting-endpoint-connectivity-rdpsshhttp-etc-failures?forum=WAVirtualMachinesforWindows).</span></span>

## <a name="detailed-troubleshooting-overview"></a><span data-ttu-id="ff93d-125">詳細疑難排解概觀</span><span class="sxs-lookup"><span data-stu-id="ff93d-125">Detailed troubleshooting overview</span></span>
<span data-ttu-id="ff93d-126">有四個主要區域來疑難排解在 Azure 虛擬機器執行上之應用程式的存取。</span><span class="sxs-lookup"><span data-stu-id="ff93d-126">There are four main areas to troubleshoot the access of an application that is running on an Azure virtual machine.</span></span>

![疑難排解無法啟動應用程式](./media/virtual-machines-common-troubleshoot-app-connection/tshoot_app_access1.png)

1. <span data-ttu-id="ff93d-128">在 Azure 虛擬機器上執行的應用程式。</span><span class="sxs-lookup"><span data-stu-id="ff93d-128">The application running on the Azure virtual machine.</span></span>
   * <span data-ttu-id="ff93d-129">應用程式本身是否正確地執行？</span><span class="sxs-lookup"><span data-stu-id="ff93d-129">Is the application itself running correctly?</span></span>
2. <span data-ttu-id="ff93d-130">Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="ff93d-130">The Azure virtual machine.</span></span>
   * <span data-ttu-id="ff93d-131">VM 本身是否正確地執行並回應要求？</span><span class="sxs-lookup"><span data-stu-id="ff93d-131">Is the VM itself running correctly and responding to requests?</span></span>
3. <span data-ttu-id="ff93d-132">Azure 網路端點。</span><span class="sxs-lookup"><span data-stu-id="ff93d-132">Azure network endpoints.</span></span>
   * <span data-ttu-id="ff93d-133">傳統部署模型中虛擬機器的雲端服務端點。</span><span class="sxs-lookup"><span data-stu-id="ff93d-133">Cloud service endpoints for virtual machines in the Classic deployment model.</span></span>
   * <span data-ttu-id="ff93d-134">資源管理員部署模型中虛擬機器的網路安全性群組和輸入 NAT 規則。</span><span class="sxs-lookup"><span data-stu-id="ff93d-134">Network Security Groups and inbound NAT rules for virtual machines in Resource Manager deployment model.</span></span>
   * <span data-ttu-id="ff93d-135">流量是否可以透過預期的連接埠從使用者流向 VM/應用程式？</span><span class="sxs-lookup"><span data-stu-id="ff93d-135">Can traffic flow from users to the VM/application on the expected ports?</span></span>
4. <span data-ttu-id="ff93d-136">您的網際網路邊緣裝置。</span><span class="sxs-lookup"><span data-stu-id="ff93d-136">Your Internet edge device.</span></span>
   * <span data-ttu-id="ff93d-137">是否已經有防火牆規則會防止流量正確地流動？</span><span class="sxs-lookup"><span data-stu-id="ff93d-137">Are firewall rules in place preventing traffic from flowing correctly?</span></span>

<span data-ttu-id="ff93d-138">針對正透過站對站 VPN 或 ExpressRoute 連線存取應用程式的用戶端電腦，可能造成問題的主要區域是應用程式和 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="ff93d-138">For client computers that are accessing the application over a site-to-site VPN or ExpressRoute connection, the main areas that can cause problems are the application and the Azure virtual machine.</span></span>

<span data-ttu-id="ff93d-139">若要判斷問題的來源並更正，請遵循下列步驟。</span><span class="sxs-lookup"><span data-stu-id="ff93d-139">To determine the source of the problem and its correction, follow these steps.</span></span>

## <a name="step-1-access-application-from-target-vm"></a><span data-ttu-id="ff93d-140">步驟 1︰從目標 VM 存取應用程式</span><span class="sxs-lookup"><span data-stu-id="ff93d-140">Step 1: Access application from target VM</span></span>
<span data-ttu-id="ff93d-141">嘗試使用適當的用戶端程式，從執行所在的 VM 存取應用程式。</span><span class="sxs-lookup"><span data-stu-id="ff93d-141">Try to access the application with the appropriate client program from the VM on which it is running.</span></span> <span data-ttu-id="ff93d-142">使用本機主機名稱、本機 IP 位址或迴路位址 (127.0.0.1)。</span><span class="sxs-lookup"><span data-stu-id="ff93d-142">Use the local host name, the local IP address, or the loopback address (127.0.0.1).</span></span>

![直接從 VM 啟動應用程式](./media/virtual-machines-common-troubleshoot-app-connection/tshoot_app_access2.png)

<span data-ttu-id="ff93d-144">例如，如果應用程式是網頁伺服器，則在 VM 上開啟瀏覽器，並嘗試存取在 VM 上託管的網頁。</span><span class="sxs-lookup"><span data-stu-id="ff93d-144">For example, if the application is a web server, open a browser on the VM and try to access a web page hosted on the VM.</span></span>

<span data-ttu-id="ff93d-145">如果您可以存取應用程式，請移至 [步驟 3](#step2)。</span><span class="sxs-lookup"><span data-stu-id="ff93d-145">If you can access the application, go to [Step 2](#step2).</span></span>

<span data-ttu-id="ff93d-146">如果您無法存取應用程式，請檢查下列設定：</span><span class="sxs-lookup"><span data-stu-id="ff93d-146">If you cannot access the application, verify the following settings:</span></span>

* <span data-ttu-id="ff93d-147">應用程式正在目標虛擬機器上執行。</span><span class="sxs-lookup"><span data-stu-id="ff93d-147">The application is running on the target virtual machine.</span></span>
* <span data-ttu-id="ff93d-148">應用程式正在接聽預期的 TCP 和 UDP 連接埠。</span><span class="sxs-lookup"><span data-stu-id="ff93d-148">The application is listening on the expected TCP and UDP ports.</span></span>

<span data-ttu-id="ff93d-149">在 Windows 和 Linux 虛擬機器兩者上，使用 **netstat -a** 命令顯示作用中的接聽連接埠。</span><span class="sxs-lookup"><span data-stu-id="ff93d-149">On both Windows and Linux-based virtual machines, use the **netstat -a** command to show the active listening ports.</span></span> <span data-ttu-id="ff93d-150">檢查應用程式應該接聽之預期連接埠的輸出。</span><span class="sxs-lookup"><span data-stu-id="ff93d-150">Examine the output for the expected ports on which your application should be listening.</span></span> <span data-ttu-id="ff93d-151">重新啟動應用程式，或視需要將它設定成使用預期的連接埠，然後嘗試在本機重新存取應用程式。</span><span class="sxs-lookup"><span data-stu-id="ff93d-151">Restart the application or configure it to use the expected ports as needed and try to access the application locally again.</span></span>

## <span data-ttu-id="ff93d-152"><a id="step2"></a>步驟 2︰從相同虛擬網路中的其他 VM 存取應用程式</span><span class="sxs-lookup"><span data-stu-id="ff93d-152"><a id="step2"></a>Step 2: Access application from another VM in the same virtual network</span></span>
<span data-ttu-id="ff93d-153">使用 VM 的主機名稱或其 Azure 指派的公用、私人或提供者 IP 位址，嘗試存取不同 VM，但相同虛擬網路中的應用程式。</span><span class="sxs-lookup"><span data-stu-id="ff93d-153">Try to access the application from a different VM but in the same virtual network, using the VM's host name or its Azure-assigned public, private, or provider IP address.</span></span> <span data-ttu-id="ff93d-154">若為使用傳統部署模型建立的虛擬機器，請勿使用雲端服務的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="ff93d-154">For virtual machines created using the classic deployment model, do not use the public IP address of the cloud service.</span></span>

![從其他 VM 啟動應用程式](./media/virtual-machines-common-troubleshoot-app-connection/tshoot_app_access3.png)

<span data-ttu-id="ff93d-156">例如，如果應用程式是網頁伺服器，請嘗試在相同虛擬網路中的其他 VM 上使用瀏覽器存取網頁。</span><span class="sxs-lookup"><span data-stu-id="ff93d-156">For example, if the application is a web server, try to access a web page from a browser on a different VM in the same virtual network.</span></span>

<span data-ttu-id="ff93d-157">如果您可以存取應用程式，請移至 [步驟 3](#step3)。</span><span class="sxs-lookup"><span data-stu-id="ff93d-157">If you can access the application, go to [Step 3](#step3).</span></span>

<span data-ttu-id="ff93d-158">如果您無法存取應用程式，請檢查下列設定：</span><span class="sxs-lookup"><span data-stu-id="ff93d-158">If you cannot access the application, verify the following settings:</span></span>

* <span data-ttu-id="ff93d-159">目標 VM 上的主機防火牆允許輸入要求與輸出回應的流量。</span><span class="sxs-lookup"><span data-stu-id="ff93d-159">The host firewall on the target VM is allowing the inbound request and outbound response traffic.</span></span>
* <span data-ttu-id="ff93d-160">在目標 VM 上執行的入侵偵測或網路監視軟體允許流量。</span><span class="sxs-lookup"><span data-stu-id="ff93d-160">Intrusion detection or network monitoring software running on the target VM is allowing the traffic.</span></span>
* <span data-ttu-id="ff93d-161">雲端服務端點或網路安全性群組允許流量：</span><span class="sxs-lookup"><span data-stu-id="ff93d-161">Cloud Services endpoints or Network Security Groups are allowing the traffic:</span></span>
  * [<span data-ttu-id="ff93d-162">傳統模型 - 管理雲端服務端點</span><span class="sxs-lookup"><span data-stu-id="ff93d-162">Classic model - Manage Cloud Services endpoints</span></span>](../articles/cloud-services/cloud-services-enable-communication-role-instances.md)
  * [<span data-ttu-id="ff93d-163">資源管理員模型 - 管理網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="ff93d-163">Resource Manager model - Manage Network Security Groups</span></span>](../articles/virtual-network/virtual-networks-create-nsg-arm-pportal.md)
* <span data-ttu-id="ff93d-164">在您的 VM 中，測試 VM 與 VM 間的路徑執行的個別元件 (例如負載平衡器或防火牆) 允許流量。</span><span class="sxs-lookup"><span data-stu-id="ff93d-164">A separate component running in your VM in the path between the test VM and your VM, such as a load balancer or firewall, is allowing the traffic.</span></span>

<span data-ttu-id="ff93d-165">在 Windows 虛擬機器上，請使用「具有進階安全性的 Windows 防火牆」判斷防火牆規則是否排除了您應用程式的輸入與輸出流量。</span><span class="sxs-lookup"><span data-stu-id="ff93d-165">On a Windows-based virtual machine, use Windows Firewall with Advanced Security to determine whether the firewall rules exclude your application's inbound and outbound traffic.</span></span>

## <span data-ttu-id="ff93d-166"><a id="step3"></a>步驟 3︰ 從虛擬網路外部存取應用程式</span><span class="sxs-lookup"><span data-stu-id="ff93d-166"><a id="step3"></a>Step 3: Access application from outside the virtual network</span></span>
<span data-ttu-id="ff93d-167">嘗試從位於虛擬網路外部的電腦存取在該虛擬網路內 VM 上執行的應用程式。</span><span class="sxs-lookup"><span data-stu-id="ff93d-167">Try to access the application from a computer outside the virtual network as the VM on which the application is running.</span></span> <span data-ttu-id="ff93d-168">使用與您的原始用戶端電腦不同的網路。</span><span class="sxs-lookup"><span data-stu-id="ff93d-168">Use a different network as your original client computer.</span></span>

![從位於虛擬網路之外的電腦啟動應用程式](./media/virtual-machines-common-troubleshoot-app-connection/tshoot_app_access4.png)

<span data-ttu-id="ff93d-170">例如，如果應用程式是 Web 伺服器，請嘗試從虛擬網路外的電腦執行瀏覽器來存取網頁。</span><span class="sxs-lookup"><span data-stu-id="ff93d-170">For example, if the application is a web server, try to access the web page from a browser running on a computer that is not in the virtual network.</span></span>

<span data-ttu-id="ff93d-171">如果您無法存取應用程式，請檢查下列設定：</span><span class="sxs-lookup"><span data-stu-id="ff93d-171">If you cannot access the application, verify the following settings:</span></span>

* <span data-ttu-id="ff93d-172">對於使用傳統部署模型建立的 VM：</span><span class="sxs-lookup"><span data-stu-id="ff93d-172">For VMs created using the classic deployment model:</span></span>
  
  * <span data-ttu-id="ff93d-173">確認 VM 的端點組態允許連入流量，特別是通訊協定 (TCP 或 UDP) 和公用與私人連接埠號碼。</span><span class="sxs-lookup"><span data-stu-id="ff93d-173">Verify that the endpoint configuration for the VM is allowing the incoming traffic, especially the protocol (TCP or UDP) and the public and private port numbers.</span></span>
  * <span data-ttu-id="ff93d-174">確認端點上的存取控制清單 (ACL) 不會阻擋來自網際網路的連入流量。</span><span class="sxs-lookup"><span data-stu-id="ff93d-174">Verify that access control lists (ACLs) on the endpoint are not preventing incoming traffic from the Internet.</span></span>
  * <span data-ttu-id="ff93d-175">如需詳細資訊，請參閱[如何設定虛擬機器的端點](../articles/virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="ff93d-175">For more information, see [How to Set Up Endpoints to a Virtual Machine](../articles/virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>
* <span data-ttu-id="ff93d-176">對於使用資源管理員部署模型建立的 VM：</span><span class="sxs-lookup"><span data-stu-id="ff93d-176">For VMs created using the Resource Manager deployment model:</span></span>
  
  * <span data-ttu-id="ff93d-177">確認 VM 的輸入 NAT 規則組態允許連入流量，特別是通訊協定 (TCP 或 UDP) 和公用與私人連接埠號碼。</span><span class="sxs-lookup"><span data-stu-id="ff93d-177">Verify that the inbound NAT rule configuration for the VM is allowing the incoming traffic, especially the protocol (TCP or UDP) and the public and private port numbers.</span></span>
  * <span data-ttu-id="ff93d-178">確認網路安全性群組允許輸入要求與輸出回應的流量。</span><span class="sxs-lookup"><span data-stu-id="ff93d-178">Verify that Network Security Groups are allowing the inbound request and outbound response traffic.</span></span>
  * <span data-ttu-id="ff93d-179">如需詳細資訊，請參閱 [什麼是網路安全性群組 (NSG)？](../articles/virtual-network/virtual-networks-nsg.md)</span><span class="sxs-lookup"><span data-stu-id="ff93d-179">For more information, see [What is a Network Security Group (NSG)?](../articles/virtual-network/virtual-networks-nsg.md)</span></span>

<span data-ttu-id="ff93d-180">如果虛擬機器或端點是負載平衡集的成員：</span><span class="sxs-lookup"><span data-stu-id="ff93d-180">If the virtual machine or endpoint is a member of a load-balanced set:</span></span>

* <span data-ttu-id="ff93d-181">請確認探查通訊協定 (TCP 或 UDP) 和連接埠號碼正確。</span><span class="sxs-lookup"><span data-stu-id="ff93d-181">Verify that the probe protocol (TCP or UDP) and port number are correct.</span></span>
* <span data-ttu-id="ff93d-182">如果探查通訊協定和連接埠與負載平衡集通訊協定和連接埠不同：</span><span class="sxs-lookup"><span data-stu-id="ff93d-182">If the probe protocol and port is different than the load-balanced set protocol and port:</span></span>
  * <span data-ttu-id="ff93d-183">請確認應用程式正在接聽探查通訊協定 (TCP 或 UDP) 和連接埠號碼 (在目標 VM 上使用 **netstat –a** )。</span><span class="sxs-lookup"><span data-stu-id="ff93d-183">Verify that the application is listening on the probe protocol (TCP or UDP) and port number (use **netstat –a** on the target VM).</span></span>
  * <span data-ttu-id="ff93d-184">確認目標 VM 上的主機防火牆允許輸入探查要求與輸出探查回應的流量。</span><span class="sxs-lookup"><span data-stu-id="ff93d-184">Verify that the host firewall on the target VM is allowing the inbound probe request and outbound probe response traffic.</span></span>

<span data-ttu-id="ff93d-185">如果您可以存取應用程式，請確定您的網際網路邊緣裝置允許：</span><span class="sxs-lookup"><span data-stu-id="ff93d-185">If you can access the application, ensure that your Internet edge device is allowing:</span></span>

* <span data-ttu-id="ff93d-186">從您的用戶端電腦輸出到 Azure 虛擬機器的應用程式要求流量。</span><span class="sxs-lookup"><span data-stu-id="ff93d-186">The outbound application request traffic from your client computer to the Azure virtual machine.</span></span>
* <span data-ttu-id="ff93d-187">來自 Azure 虛擬機器的輸入應用程式回應流量。</span><span class="sxs-lookup"><span data-stu-id="ff93d-187">The inbound application response traffic from the Azure virtual machine.</span></span>

## <a name="step-4-if-you-cannot-access-the-application-use-ip-verify-to-check-the-settings"></a><span data-ttu-id="ff93d-188">步驟 4 如果您無法存取應用程式，請使用 IP 驗證來檢查設定。</span><span class="sxs-lookup"><span data-stu-id="ff93d-188">Step 4 If you cannot access the application, use IP Verify to check the settings.</span></span> 

<span data-ttu-id="ff93d-189">如需詳細資訊，請參閱 [Azure 網路監視概觀](https://docs.microsoft.com/en-us/azure/network-watcher/network-watcher-monitoring-overview)。</span><span class="sxs-lookup"><span data-stu-id="ff93d-189">For more information, see [Azure network monitoring overview](https://docs.microsoft.com/en-us/azure/network-watcher/network-watcher-monitoring-overview).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="ff93d-190">其他資源</span><span class="sxs-lookup"><span data-stu-id="ff93d-190">Additional resources</span></span>
[<span data-ttu-id="ff93d-191">針對以 Windows 為基礎的 Azure 虛擬機器的遠端桌面連線進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="ff93d-191">Troubleshoot Remote Desktop connections to a Windows-based Azure Virtual Machine</span></span>](../articles/virtual-machines/windows/troubleshoot-rdp-connection.md)

[<span data-ttu-id="ff93d-192">疑難排解以 Linux 為基礎之 Azure 虛擬機器的安全殼層 (SSH) 連線</span><span class="sxs-lookup"><span data-stu-id="ff93d-192">Troubleshoot Secure Shell (SSH) connections to a Linux-based Azure virtual machine</span></span>](../articles/virtual-machines/linux/troubleshoot-ssh-connection.md)

