<span data-ttu-id="c72f7-101">您無法啟動或連接 Azure 虛擬機器 (VM) 上執行的 tooan 應用程式時，有各種原因。</span><span class="sxs-lookup"><span data-stu-id="c72f7-101">There are various reasons when you cannot start or connect tooan application running on an Azure virtual machine (VM).</span></span> <span data-ttu-id="c72f7-102">原因包括 hello 應用程式未執行或接聽 hello 預期的通訊埠，hello 接聽連接埠被封鎖，或是網路不會正確傳遞流量 toohello 應用程式的規則。</span><span class="sxs-lookup"><span data-stu-id="c72f7-102">Reasons include hello application not running or listening on hello expected ports, hello listening port blocked, or networking rules not correctly passing traffic toohello application.</span></span> <span data-ttu-id="c72f7-103">本文說明有系統的方法 toofind 和正確的 hello 問題。</span><span class="sxs-lookup"><span data-stu-id="c72f7-103">This article describes a methodical approach toofind and correct hello problem.</span></span>

<span data-ttu-id="c72f7-104">如果您在連接時發生問題 tooyour VM hello 下列其中一種文件第一次使用 RDP 或 SSH，請參閱：</span><span class="sxs-lookup"><span data-stu-id="c72f7-104">If you are having issues connecting tooyour VM using RDP or SSH, see one of hello following articles first:</span></span>

* [<span data-ttu-id="c72f7-105">疑難排解遠端桌面連線 tooa windows Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="c72f7-105">Troubleshoot Remote Desktop connections tooa Windows-based Azure Virtual Machine</span></span>](../articles/virtual-machines/windows/troubleshoot-rdp-connection.md)
* <span data-ttu-id="c72f7-106">[疑難排解安全殼層 (SSH) 連線 tooa Linux 型 Azure 虛擬機器](../articles/virtual-machines/linux/troubleshoot-ssh-connection.md)。</span><span class="sxs-lookup"><span data-stu-id="c72f7-106">[Troubleshoot Secure Shell (SSH) connections tooa Linux-based Azure virtual machine](../articles/virtual-machines/linux/troubleshoot-ssh-connection.md).</span></span>

> [!NOTE]
> <span data-ttu-id="c72f7-107">Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../articles/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="c72f7-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../articles/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="c72f7-108">本文將說明如何使用這兩個模型，但 Microsoft 建議的最新的部署使用 hello 資源管理員的模型。</span><span class="sxs-lookup"><span data-stu-id="c72f7-108">This article covers using both models, but Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="c72f7-109">如果您需要更多說明，在本文中的任何時間點，您可以連絡上 hello Azure 專家[hello MSDN Azure 和 hello 堆疊溢位論壇](https://azure.microsoft.com/support/forums/)。</span><span class="sxs-lookup"><span data-stu-id="c72f7-109">If you need more help at any point in this article, you can contact hello Azure experts on [hello MSDN Azure and hello Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="c72f7-110">或者，您也可以提出 Azure 支援事件。</span><span class="sxs-lookup"><span data-stu-id="c72f7-110">Alternatively, you can also file an Azure support incident.</span></span> <span data-ttu-id="c72f7-111">移 toohello [Azure 支援服務網站](https://azure.microsoft.com/support/options/)選取**取得支援**。</span><span class="sxs-lookup"><span data-stu-id="c72f7-111">Go toohello [Azure support site](https://azure.microsoft.com/support/options/) and select **Get Support**.</span></span>

## <a name="quick-start-troubleshooting-steps"></a><span data-ttu-id="c72f7-112">快速入門的疑難排解步驟</span><span class="sxs-lookup"><span data-stu-id="c72f7-112">Quick-start troubleshooting steps</span></span>
<span data-ttu-id="c72f7-113">如果您有連接 tooan 應用程式的問題，請嘗試下列一般疑難排解步驟的 hello。</span><span class="sxs-lookup"><span data-stu-id="c72f7-113">If you have problems connecting tooan application, try hello following general troubleshooting steps.</span></span> <span data-ttu-id="c72f7-114">在每個步驟中之後, 再試一次連接 tooyour 一次應用程式：</span><span class="sxs-lookup"><span data-stu-id="c72f7-114">After each step, try connecting tooyour application again:</span></span>

* <span data-ttu-id="c72f7-115">重新啟動 hello 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="c72f7-115">Restart hello virtual machine</span></span>
* <span data-ttu-id="c72f7-116">重新建立 hello 端點 / 防火牆規則/網路安全性群組 (NSG) 規則</span><span class="sxs-lookup"><span data-stu-id="c72f7-116">Recreate hello endpoint / firewall rules / network security group (NSG) rules</span></span>
  * [<span data-ttu-id="c72f7-117">資源管理員模型 - 管理網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="c72f7-117">Resource Manager model - Manage Network Security Groups</span></span>](../articles/virtual-network/virtual-networks-create-nsg-arm-pportal.md)
  * [<span data-ttu-id="c72f7-118">傳統模型 - 管理雲端服務端點</span><span class="sxs-lookup"><span data-stu-id="c72f7-118">Classic model - Manage Cloud Services endpoints</span></span>](../articles/cloud-services/cloud-services-enable-communication-role-instances.md)
* <span data-ttu-id="c72f7-119">從不同的位置 (例如不同的 Azure 虛擬網路) 進行連線</span><span class="sxs-lookup"><span data-stu-id="c72f7-119">Connect from different location, such as a different Azure virtual network</span></span>
* <span data-ttu-id="c72f7-120">重新部署 hello 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="c72f7-120">Redeploy hello virtual machine</span></span>
  * [<span data-ttu-id="c72f7-121">重新部署 Windows VM</span><span class="sxs-lookup"><span data-stu-id="c72f7-121">Redeploy Windows VM</span></span>](../articles/virtual-machines/windows/redeploy-to-new-node.md)
  * [<span data-ttu-id="c72f7-122">重新部署 Linux VM</span><span class="sxs-lookup"><span data-stu-id="c72f7-122">Redeploy Linux VM</span></span>](../articles/virtual-machines/linux/redeploy-to-new-node.md)
* <span data-ttu-id="c72f7-123">重新建立 hello 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="c72f7-123">Recreate hello virtual machine</span></span>

<span data-ttu-id="c72f7-124">如需詳細資訊，請參閱 [疑難排解端點連接能力 (RDP/SSH/HTTP 等失敗問題)](https://social.msdn.microsoft.com/Forums/azure/en-US/538a8f18-7c1f-4d6e-b81c-70c00e25c93d/troubleshooting-endpoint-connectivity-rdpsshhttp-etc-failures?forum=WAVirtualMachinesforWindows)。</span><span class="sxs-lookup"><span data-stu-id="c72f7-124">For more information, see [Troubleshooting Endpoint Connectivity (RDP/SSH/HTTP, etc. failures)](https://social.msdn.microsoft.com/Forums/azure/en-US/538a8f18-7c1f-4d6e-b81c-70c00e25c93d/troubleshooting-endpoint-connectivity-rdpsshhttp-etc-failures?forum=WAVirtualMachinesforWindows).</span></span>

## <a name="detailed-troubleshooting-overview"></a><span data-ttu-id="c72f7-125">詳細疑難排解概觀</span><span class="sxs-lookup"><span data-stu-id="c72f7-125">Detailed troubleshooting overview</span></span>
<span data-ttu-id="c72f7-126">有四個主要區域 tootroubleshoot hello 存取 Azure 虛擬機器上執行的應用程式。</span><span class="sxs-lookup"><span data-stu-id="c72f7-126">There are four main areas tootroubleshoot hello access of an application that is running on an Azure virtual machine.</span></span>

![疑難排解無法啟動應用程式](./media/virtual-machines-common-troubleshoot-app-connection/tshoot_app_access1.png)

1. <span data-ttu-id="c72f7-128">hello hello Azure 虛擬機器上執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="c72f7-128">hello application running on hello Azure virtual machine.</span></span>
   * <span data-ttu-id="c72f7-129">Hello 應用程式本身已正確執行？</span><span class="sxs-lookup"><span data-stu-id="c72f7-129">Is hello application itself running correctly?</span></span>
2. <span data-ttu-id="c72f7-130">hello Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="c72f7-130">hello Azure virtual machine.</span></span>
   * <span data-ttu-id="c72f7-131">是 hello VM 本身正確執行，而且回應 toorequests 嗎？</span><span class="sxs-lookup"><span data-stu-id="c72f7-131">Is hello VM itself running correctly and responding toorequests?</span></span>
3. <span data-ttu-id="c72f7-132">Azure 網路端點。</span><span class="sxs-lookup"><span data-stu-id="c72f7-132">Azure network endpoints.</span></span>
   * <span data-ttu-id="c72f7-133">Hello 傳統部署模型中的虛擬機器的雲端服務端點。</span><span class="sxs-lookup"><span data-stu-id="c72f7-133">Cloud service endpoints for virtual machines in hello Classic deployment model.</span></span>
   * <span data-ttu-id="c72f7-134">資源管理員部署模型中虛擬機器的網路安全性群組和輸入 NAT 規則。</span><span class="sxs-lookup"><span data-stu-id="c72f7-134">Network Security Groups and inbound NAT rules for virtual machines in Resource Manager deployment model.</span></span>
   * <span data-ttu-id="c72f7-135">可以將流量從使用者 toohello hello 預期的連接埠上的 VM/應用程式的流程嗎？</span><span class="sxs-lookup"><span data-stu-id="c72f7-135">Can traffic flow from users toohello VM/application on hello expected ports?</span></span>
4. <span data-ttu-id="c72f7-136">您的網際網路邊緣裝置。</span><span class="sxs-lookup"><span data-stu-id="c72f7-136">Your Internet edge device.</span></span>
   * <span data-ttu-id="c72f7-137">是否已經有防火牆規則會防止流量正確地流動？</span><span class="sxs-lookup"><span data-stu-id="c72f7-137">Are firewall rules in place preventing traffic from flowing correctly?</span></span>

<span data-ttu-id="c72f7-138">透過站對站 VPN 或 ExpressRoute 連線存取 hello 應用程式的用戶端電腦，可能會造成問題的 hello 主要區域 hello 應用程式和 hello Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="c72f7-138">For client computers that are accessing hello application over a site-to-site VPN or ExpressRoute connection, hello main areas that can cause problems are hello application and hello Azure virtual machine.</span></span>

<span data-ttu-id="c72f7-139">toodetermine hello 來源 hello 問題和更正，請遵循下列步驟。</span><span class="sxs-lookup"><span data-stu-id="c72f7-139">toodetermine hello source of hello problem and its correction, follow these steps.</span></span>

## <a name="step-1-access-application-from-target-vm"></a><span data-ttu-id="c72f7-140">步驟 1︰從目標 VM 存取應用程式</span><span class="sxs-lookup"><span data-stu-id="c72f7-140">Step 1: Access application from target VM</span></span>
<span data-ttu-id="c72f7-141">請嘗試 tooaccess hello 應用程式與 hello 適當的用戶端程式從執行所在的 hello VM。</span><span class="sxs-lookup"><span data-stu-id="c72f7-141">Try tooaccess hello application with hello appropriate client program from hello VM on which it is running.</span></span> <span data-ttu-id="c72f7-142">使用 hello 本機主機名稱、 hello 本機 IP 位址或 hello 回送位址 (127.0.0.1)。</span><span class="sxs-lookup"><span data-stu-id="c72f7-142">Use hello local host name, hello local IP address, or hello loopback address (127.0.0.1).</span></span>

![直接從 hello VM 啟動應用程式](./media/virtual-machines-common-troubleshoot-app-connection/tshoot_app_access2.png)

<span data-ttu-id="c72f7-144">例如，如果 hello 應用程式是 web 伺服器，開啟 hello VM 上的瀏覽器，然後再次嘗試 tooaccess hello VM 上裝載的網頁。</span><span class="sxs-lookup"><span data-stu-id="c72f7-144">For example, if hello application is a web server, open a browser on hello VM and try tooaccess a web page hosted on hello VM.</span></span>

<span data-ttu-id="c72f7-145">如果您可以存取 hello 應用程式，請移至太[步驟 2](#step2)。</span><span class="sxs-lookup"><span data-stu-id="c72f7-145">If you can access hello application, go too[Step 2](#step2).</span></span>

<span data-ttu-id="c72f7-146">如果您無法存取 hello 應用程式，請確認下列設定的 hello:</span><span class="sxs-lookup"><span data-stu-id="c72f7-146">If you cannot access hello application, verify hello following settings:</span></span>

* <span data-ttu-id="c72f7-147">hello 應用程式正在 hello 目標虛擬機器上執行。</span><span class="sxs-lookup"><span data-stu-id="c72f7-147">hello application is running on hello target virtual machine.</span></span>
* <span data-ttu-id="c72f7-148">hello 應用程式正在接聽 hello 必須是 TCP 和 UDP 通訊埠。</span><span class="sxs-lookup"><span data-stu-id="c72f7-148">hello application is listening on hello expected TCP and UDP ports.</span></span>

<span data-ttu-id="c72f7-149">在 Windows 和 Linux 型虛擬機器上使用 hello **netstat-a** tooshow hello 作用中的接聽連接埠的命令。</span><span class="sxs-lookup"><span data-stu-id="c72f7-149">On both Windows and Linux-based virtual machines, use hello **netstat -a** command tooshow hello active listening ports.</span></span> <span data-ttu-id="c72f7-150">檢查您的應用程式應接聽的 hello 預期通訊埠的 hello 輸出。</span><span class="sxs-lookup"><span data-stu-id="c72f7-150">Examine hello output for hello expected ports on which your application should be listening.</span></span> <span data-ttu-id="c72f7-151">重新啟動 hello 應用程式或視需要將它設定 toouse hello 預期的連接埠並再試一次本機 tooaccess hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c72f7-151">Restart hello application or configure it toouse hello expected ports as needed and try tooaccess hello application locally again.</span></span>

## <span data-ttu-id="c72f7-152"><a id="step2"></a>步驟 2： 從另一個 VM hello 中存取應用程式相同的虛擬網路</span><span class="sxs-lookup"><span data-stu-id="c72f7-152"><a id="step2"></a>Step 2: Access application from another VM in hello same virtual network</span></span>
<span data-ttu-id="c72f7-153">嘗試從不同的 VM tooaccess hello 應用程式，但在 hello 相同虛擬網路上使用 hello VM 的主機名稱或其 Azure 指派公用、 私用或提供者 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="c72f7-153">Try tooaccess hello application from a different VM but in hello same virtual network, using hello VM's host name or its Azure-assigned public, private, or provider IP address.</span></span> <span data-ttu-id="c72f7-154">針對使用 hello 傳統部署模型所建立的虛擬機器，請勿 hello 雲端服務的 hello 公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="c72f7-154">For virtual machines created using hello classic deployment model, do not use hello public IP address of hello cloud service.</span></span>

![從其他 VM 啟動應用程式](./media/virtual-machines-common-troubleshoot-app-connection/tshoot_app_access3.png)

<span data-ttu-id="c72f7-156">例如，如果 hello 應用程式是 web 伺服器，再試一次 tooaccess 網頁中的不同 VM 上的瀏覽器從 hello 相同虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="c72f7-156">For example, if hello application is a web server, try tooaccess a web page from a browser on a different VM in hello same virtual network.</span></span>

<span data-ttu-id="c72f7-157">如果您可以存取 hello 應用程式，請移至太[步驟 3](#step3)。</span><span class="sxs-lookup"><span data-stu-id="c72f7-157">If you can access hello application, go too[Step 3](#step3).</span></span>

<span data-ttu-id="c72f7-158">如果您無法存取 hello 應用程式，請確認下列設定的 hello:</span><span class="sxs-lookup"><span data-stu-id="c72f7-158">If you cannot access hello application, verify hello following settings:</span></span>

* <span data-ttu-id="c72f7-159">hello hello 目標 VM 上的主機防火牆允許 hello 輸入的要求和回應的輸出流量。</span><span class="sxs-lookup"><span data-stu-id="c72f7-159">hello host firewall on hello target VM is allowing hello inbound request and outbound response traffic.</span></span>
* <span data-ttu-id="c72f7-160">入侵偵測或監視 hello 目標 VM 上執行的軟體的網路允許 hello 流量。</span><span class="sxs-lookup"><span data-stu-id="c72f7-160">Intrusion detection or network monitoring software running on hello target VM is allowing hello traffic.</span></span>
* <span data-ttu-id="c72f7-161">雲端服務端點或網路安全性群組允許 hello 流量：</span><span class="sxs-lookup"><span data-stu-id="c72f7-161">Cloud Services endpoints or Network Security Groups are allowing hello traffic:</span></span>
  * [<span data-ttu-id="c72f7-162">傳統模型 - 管理雲端服務端點</span><span class="sxs-lookup"><span data-stu-id="c72f7-162">Classic model - Manage Cloud Services endpoints</span></span>](../articles/cloud-services/cloud-services-enable-communication-role-instances.md)
  * [<span data-ttu-id="c72f7-163">資源管理員模型 - 管理網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="c72f7-163">Resource Manager model - Manage Network Security Groups</span></span>](../articles/virtual-network/virtual-networks-create-nsg-arm-pportal.md)
* <span data-ttu-id="c72f7-164">VM 和 VM，例如負載平衡器或防火牆，hello 測試之間執行 hello 路徑中在 VM 中的個別元件允許 hello 流量。</span><span class="sxs-lookup"><span data-stu-id="c72f7-164">A separate component running in your VM in hello path between hello test VM and your VM, such as a load balancer or firewall, is allowing hello traffic.</span></span>

<span data-ttu-id="c72f7-165">Windows 型虛擬機器上，使用 Windows 防火牆具有進階安全性 toodetermine 是否 hello 防火牆規則中排除應用程式的輸入和輸出流量。</span><span class="sxs-lookup"><span data-stu-id="c72f7-165">On a Windows-based virtual machine, use Windows Firewall with Advanced Security toodetermine whether hello firewall rules exclude your application's inbound and outbound traffic.</span></span>

## <span data-ttu-id="c72f7-166"><a id="step3"></a>步驟 3： 從外部 hello 虛擬網路中存取應用程式</span><span class="sxs-lookup"><span data-stu-id="c72f7-166"><a id="step3"></a>Step 3: Access application from outside hello virtual network</span></span>
<span data-ttu-id="c72f7-167">請嘗試 tooaccess hello 應用程式從 hello 虛擬網路外的電腦作為 hello 應用程式執行所在的 hello VM。</span><span class="sxs-lookup"><span data-stu-id="c72f7-167">Try tooaccess hello application from a computer outside hello virtual network as hello VM on which hello application is running.</span></span> <span data-ttu-id="c72f7-168">使用與您的原始用戶端電腦不同的網路。</span><span class="sxs-lookup"><span data-stu-id="c72f7-168">Use a different network as your original client computer.</span></span>

![從 hello 虛擬網路外的電腦啟動應用程式](./media/virtual-machines-common-troubleshoot-app-connection/tshoot_app_access4.png)

<span data-ttu-id="c72f7-170">例如，如果 hello 應用程式是 web 伺服器，請嘗試 tooaccess hello 網頁，從瀏覽器不在 hello 虛擬網路的電腦上執行。</span><span class="sxs-lookup"><span data-stu-id="c72f7-170">For example, if hello application is a web server, try tooaccess hello web page from a browser running on a computer that is not in hello virtual network.</span></span>

<span data-ttu-id="c72f7-171">如果您無法存取 hello 應用程式，請確認下列設定的 hello:</span><span class="sxs-lookup"><span data-stu-id="c72f7-171">If you cannot access hello application, verify hello following settings:</span></span>

* <span data-ttu-id="c72f7-172">針對 Vm 建立使用 hello 傳統部署模型：</span><span class="sxs-lookup"><span data-stu-id="c72f7-172">For VMs created using hello classic deployment model:</span></span>
  
  * <span data-ttu-id="c72f7-173">請確認 VM 允許 hello 連入流量，特別是 「 hello 通訊協定 （TCP 或 UDP） 」 和 「 hello 公用和私用連接埠號碼的 hello 該 hello 端點組態。</span><span class="sxs-lookup"><span data-stu-id="c72f7-173">Verify that hello endpoint configuration for hello VM is allowing hello incoming traffic, especially hello protocol (TCP or UDP) and hello public and private port numbers.</span></span>
  * <span data-ttu-id="c72f7-174">請確認 hello 端點上的存取控制清單 (Acl)，不會阻礙 hello 網際網路的連入流量。</span><span class="sxs-lookup"><span data-stu-id="c72f7-174">Verify that access control lists (ACLs) on hello endpoint are not preventing incoming traffic from hello Internet.</span></span>
  * <span data-ttu-id="c72f7-175">如需詳細資訊，請參閱[如何 tooSet 端點 tooa 虛擬機器](../articles/virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="c72f7-175">For more information, see [How tooSet Up Endpoints tooa Virtual Machine](../articles/virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>
* <span data-ttu-id="c72f7-176">若是使用 hello Resource Manager 部署模型所建立的 Vm:</span><span class="sxs-lookup"><span data-stu-id="c72f7-176">For VMs created using hello Resource Manager deployment model:</span></span>
  
  * <span data-ttu-id="c72f7-177">請確認的 hello 的 hello VM 允許 hello 連入流量，特別是 「 hello 通訊協定 （TCP 或 UDP） 」 和 「 hello 公用和私用連接埠號碼的輸入的 NAT 規則組態。</span><span class="sxs-lookup"><span data-stu-id="c72f7-177">Verify that hello inbound NAT rule configuration for hello VM is allowing hello incoming traffic, especially hello protocol (TCP or UDP) and hello public and private port numbers.</span></span>
  * <span data-ttu-id="c72f7-178">請確認網路安全性群組允許 hello 輸入的要求和回應的輸出流量。</span><span class="sxs-lookup"><span data-stu-id="c72f7-178">Verify that Network Security Groups are allowing hello inbound request and outbound response traffic.</span></span>
  * <span data-ttu-id="c72f7-179">如需詳細資訊，請參閱 [什麼是網路安全性群組 (NSG)？](../articles/virtual-network/virtual-networks-nsg.md)</span><span class="sxs-lookup"><span data-stu-id="c72f7-179">For more information, see [What is a Network Security Group (NSG)?](../articles/virtual-network/virtual-networks-nsg.md)</span></span>

<span data-ttu-id="c72f7-180">如果 hello 虛擬機器或端點是一組負載平衡的成員：</span><span class="sxs-lookup"><span data-stu-id="c72f7-180">If hello virtual machine or endpoint is a member of a load-balanced set:</span></span>

* <span data-ttu-id="c72f7-181">請確認 hello 探查通訊協定 （TCP 或 UDP） 和連接埠號碼正確。</span><span class="sxs-lookup"><span data-stu-id="c72f7-181">Verify that hello probe protocol (TCP or UDP) and port number are correct.</span></span>
* <span data-ttu-id="c72f7-182">如果 hello 探查通訊協定和連接埠是不同於 hello 負載平衡集的通訊協定和連接埠：</span><span class="sxs-lookup"><span data-stu-id="c72f7-182">If hello probe protocol and port is different than hello load-balanced set protocol and port:</span></span>
  * <span data-ttu-id="c72f7-183">確認 hello 應用程式正在接聽 hello 探查通訊協定 （TCP 或 UDP） 和通訊埠編號 (使用**netstat – a** hello 上目標 VM)。</span><span class="sxs-lookup"><span data-stu-id="c72f7-183">Verify that hello application is listening on hello probe protocol (TCP or UDP) and port number (use **netstat –a** on hello target VM).</span></span>
  * <span data-ttu-id="c72f7-184">請確認該 VM 允許 hello 輸入的探查要求，而輸出探查回應流量 hello 目標上的 hello 主機防火牆。</span><span class="sxs-lookup"><span data-stu-id="c72f7-184">Verify that hello host firewall on hello target VM is allowing hello inbound probe request and outbound probe response traffic.</span></span>

<span data-ttu-id="c72f7-185">如果您可以存取 hello 應用程式，確認您的網際網路邊緣裝置會允許：</span><span class="sxs-lookup"><span data-stu-id="c72f7-185">If you can access hello application, ensure that your Internet edge device is allowing:</span></span>

* <span data-ttu-id="c72f7-186">hello 輸出應用程式要求流量從您的用戶端電腦 toohello Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="c72f7-186">hello outbound application request traffic from your client computer toohello Azure virtual machine.</span></span>
* <span data-ttu-id="c72f7-187">hello 輸入應用程式回應 hello Azure 虛擬機器流量。</span><span class="sxs-lookup"><span data-stu-id="c72f7-187">hello inbound application response traffic from hello Azure virtual machine.</span></span>

## <a name="step-4-if-you-cannot-access-hello-application-use-ip-verify-toocheck-hello-settings"></a><span data-ttu-id="c72f7-188">步驟 4，如果您無法存取 hello 應用程式，使用 IP 確認 toocheck hello 設定。</span><span class="sxs-lookup"><span data-stu-id="c72f7-188">Step 4 If you cannot access hello application, use IP Verify toocheck hello settings.</span></span> 

<span data-ttu-id="c72f7-189">如需詳細資訊，請參閱 [Azure 網路監視概觀](https://docs.microsoft.com/en-us/azure/network-watcher/network-watcher-monitoring-overview)。</span><span class="sxs-lookup"><span data-stu-id="c72f7-189">For more information, see [Azure network monitoring overview](https://docs.microsoft.com/en-us/azure/network-watcher/network-watcher-monitoring-overview).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="c72f7-190">其他資源</span><span class="sxs-lookup"><span data-stu-id="c72f7-190">Additional resources</span></span>
[<span data-ttu-id="c72f7-191">疑難排解遠端桌面連線 tooa windows Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="c72f7-191">Troubleshoot Remote Desktop connections tooa Windows-based Azure Virtual Machine</span></span>](../articles/virtual-machines/windows/troubleshoot-rdp-connection.md)

[<span data-ttu-id="c72f7-192">疑難排解安全殼層 (SSH) 連線 tooa Linux 型 Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="c72f7-192">Troubleshoot Secure Shell (SSH) connections tooa Linux-based Azure virtual machine</span></span>](../articles/virtual-machines/linux/troubleshoot-ssh-connection.md)

