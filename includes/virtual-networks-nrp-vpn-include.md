## <a name="vpn-gateway"></a><span data-ttu-id="2a7f5-101">VPN 閘道</span><span class="sxs-lookup"><span data-stu-id="2a7f5-101">VPN Gateway</span></span>
<span data-ttu-id="2a7f5-102">VPN 閘道資源可讓您 toocreate 其內部部署資料中心與 Azure 之間的安全連線。</span><span class="sxs-lookup"><span data-stu-id="2a7f5-102">A VPN gateway resource enables you toocreate a secure connection between their on-premises data center and Azure.</span></span> <span data-ttu-id="2a7f5-103">您可以使用三種不同的方式設定 VPN 閘道資源：</span><span class="sxs-lookup"><span data-stu-id="2a7f5-103">A VPN gateway resource can be configured in three different ways:</span></span>

* <span data-ttu-id="2a7f5-104">**點 tooSite** – 您可以安全地存取您的 Azure 資源所使用的 VPN 用戶端從任何電腦裝載的 VNET。</span><span class="sxs-lookup"><span data-stu-id="2a7f5-104">**Point tooSite** – you can securely access your Azure resources hosted in a VNET by using a VPN client from any computer.</span></span> 
* <span data-ttu-id="2a7f5-105">**多站台連線**– 您可以安全地連接從內部部署資料中心 tooresources 在 VNET 中執行。</span><span class="sxs-lookup"><span data-stu-id="2a7f5-105">**Multi-site connection** – you can securely connect from your on-premises data centers tooresources running in a VNET.</span></span> 
* <span data-ttu-id="2a7f5-106">**VNET tooVNET** – 您可以安全地透過 Azure VNET 內連接 hello 相同區域中，或在異地備援的區域 toobuild 工作負載間。</span><span class="sxs-lookup"><span data-stu-id="2a7f5-106">**VNET tooVNET** – you can securely connect across Azure VNETS within hello same region, or across regions toobuild workloads with geo-redundancy.</span></span>

<span data-ttu-id="2a7f5-107">VPN 閘道的重要屬性包括：</span><span class="sxs-lookup"><span data-stu-id="2a7f5-107">Key properties of a VPN gateway include:</span></span>

* <span data-ttu-id="2a7f5-108">**閘道類型** - 動態路由閘道或靜態路由閘道。</span><span class="sxs-lookup"><span data-stu-id="2a7f5-108">**Gateway type** - dynamically routed or a static routed gateway.</span></span> 
* <span data-ttu-id="2a7f5-109">**VPN 用戶端位址集區首碼**-連接點 toosite 組態中的 IP 位址指派 toobe tooclients。</span><span class="sxs-lookup"><span data-stu-id="2a7f5-109">**VPN Client Address Pool Prefix** – IP addresses toobe assigned tooclients connecting in a point toosite configuration.</span></span>

