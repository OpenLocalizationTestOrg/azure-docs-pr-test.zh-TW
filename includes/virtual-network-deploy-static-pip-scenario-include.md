## <a name="scenario"></a><span data-ttu-id="d4037-101">案例</span><span class="sxs-lookup"><span data-stu-id="d4037-101">Scenario</span></span>
<span data-ttu-id="d4037-102">本文件將逐步引導使用靜態公用 IP 位址配置 tooa 虛擬機器 (VM) 的部署。</span><span class="sxs-lookup"><span data-stu-id="d4037-102">This document will walk through a deployment that uses a static public IP address allocated tooa virtual machine (VM).</span></span> <span data-ttu-id="d4037-103">在此案例中，您擁有具有自己的靜態公用 IP 位址的單一 VM。</span><span class="sxs-lookup"><span data-stu-id="d4037-103">In this scenario, you have a single VM with its own static public IP address.</span></span> <span data-ttu-id="d4037-104">hello VM 是名為的子網路的一部分**前端**，也可靜態私人 IP 位址 (**192.168.1.101**) 的子網路中。</span><span class="sxs-lookup"><span data-stu-id="d4037-104">hello VM is part of a subnet named **FrontEnd** and also has a static private IP address (**192.168.1.101**) in that subnet.</span></span>

<span data-ttu-id="d4037-105">您可能需要靜態 IP 位址，需要使用中的 hello SSL 憑證是連結的 tooan IP SSL 連線的 web 伺服器的位址。</span><span class="sxs-lookup"><span data-stu-id="d4037-105">You may need a static IP address for web servers that require SSL connections in which hello SSL certificate is linked tooan IP address.</span></span> 

![影像說明](./media/virtual-network-deploy-static-pip-scenario-include/figure1.png)

<span data-ttu-id="d4037-107">您可以依照下列 hello 上圖所示的 toodeploy hello 環境的 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="d4037-107">You can follow hello steps below toodeploy hello environment shown in hello figure above.</span></span>

