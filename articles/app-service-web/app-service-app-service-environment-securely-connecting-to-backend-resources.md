---
title: "安全地從 App Service 環境連接到後端資源"
description: "了解如何安全地從 App Service 環境連接到後端資源。"
services: app-service
documentationcenter: 
author: stefsch
manager: erikre
editor: 
ms.assetid: f82eb283-a6e7-4923-a00b-4b4ccf7c4b5b
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/04/2016
ms.author: stefsch
ms.openlocfilehash: 0b6d3a47dc429c469b37c2c74f546cfeca580358
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="securely-connecting-to-backend-resources-from-an-app-service-environment"></a><span data-ttu-id="26491-103">安全地從 App Service 環境連接到後端資源</span><span class="sxs-lookup"><span data-stu-id="26491-103">Securely Connecting to Backend Resources from an App Service Environment</span></span>
## <a name="overview"></a><span data-ttu-id="26491-104">概觀</span><span class="sxs-lookup"><span data-stu-id="26491-104">Overview</span></span>
<span data-ttu-id="26491-105">因為 App Service 環境一律會在 Azure Resource Manager 虛擬網路或者傳統式部署模型[虛擬網路][virtualnetwork]兩者之一中建立，從 App Service 環境傳出至其他後端資源的連線可以獨佔方式透過虛擬網路傳送。</span><span class="sxs-lookup"><span data-stu-id="26491-105">Since an App Service Environment is always created in **either** an Azure Resource Manager virtual network, **or** a classic deployment model [virtual network][virtualnetwork], outbound connections from an App Service Environment to other backend resources can flow exclusively over the virtual network.</span></span>  <span data-ttu-id="26491-106">在 2016 年 6 月所進行的最新變更之後，ASE 也可以部署到使用公用位址範圍或 RFC1918 位址空間 (也就是</span><span class="sxs-lookup"><span data-stu-id="26491-106">With a recent change made in June 2016, ASEs can also be deployed into virtual networks that use either public address ranges, or RFC1918 address spaces (i.e.</span></span> <span data-ttu-id="26491-107">私人位址) 的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="26491-107">private addresses).</span></span>  

<span data-ttu-id="26491-108">例如，SQL Server 可能會在已鎖定連接埠 1433 的虛擬機器叢集上執行。</span><span class="sxs-lookup"><span data-stu-id="26491-108">For example, there may be a SQL Server running on a cluster of virtual machines with port 1433 locked down.</span></span>  <span data-ttu-id="26491-109">此端點可能已納入 ACL，只允許從相同虛擬網路上的其他資源進行存取。</span><span class="sxs-lookup"><span data-stu-id="26491-109">The endpoint may be ACLd to only allow access from other resources on the same virtual network.</span></span>  

<span data-ttu-id="26491-110">另一個例子則是，敏感性端點可能會執行內部部署並透過[站台對站台][SiteToSite]或 [Azure ExpressRoute][ExpressRoute] 連線至 Azure。</span><span class="sxs-lookup"><span data-stu-id="26491-110">As another example, sensitive endpoints may run on-premises and be connected to Azure via either [Site-to-Site][SiteToSite] or [Azure ExpressRoute][ExpressRoute] connections.</span></span>  <span data-ttu-id="26491-111">因此，只有虛擬網路中連接到站台對站台或 ExpressRoute 通道的資源能夠存取內部部署端點。</span><span class="sxs-lookup"><span data-stu-id="26491-111">As a result, only resources in virtual networks connected to the Site-to-Site or ExpressRoute tunnels will be able to access on-premises endpoints.</span></span>

<span data-ttu-id="26491-112">在上述這些案例中，在 App Service 環境上執行的應用程式將能夠安全地連接到各種伺服器和資源。</span><span class="sxs-lookup"><span data-stu-id="26491-112">For all of these scenarios, apps running on an App Service Environment will be able to securely connect to the various servers and resources.</span></span>  <span data-ttu-id="26491-113">從 App Service 環境中執行之應用程式送至相同虛擬網路中私密端點 (或連接到相同的虛擬網路) 的輸出流量，只會透過虛擬網路傳送。</span><span class="sxs-lookup"><span data-stu-id="26491-113">Outbound traffic from apps running in an App Service Environment to private endpoints in the same virtual network (or connected to the same virtual network), will only flow over the virtual network.</span></span>  <span data-ttu-id="26491-114">送至私密端點的輸出流量不會透過公用網際網路傳送。</span><span class="sxs-lookup"><span data-stu-id="26491-114">Outbound traffic to private endpoints will not flow over the public Internet.</span></span>

<span data-ttu-id="26491-115">從 App Service 環境輸出至虛擬網路內端點的流量有一點值得注意。</span><span class="sxs-lookup"><span data-stu-id="26491-115">One caveat applies to outbound traffic from an App Service Environment to endpoints within a virtual network.</span></span>  <span data-ttu-id="26491-116">App Service 環境無法連線到與 App Service 環境位於「相同」  子網路的虛擬機器端點。</span><span class="sxs-lookup"><span data-stu-id="26491-116">App Service Environments cannot reach endpoints of virtual machines located in the **same** subnet as the App Service Environment.</span></span>  <span data-ttu-id="26491-117">只要 App Service 環境是部署到保留給 App Service 環境專用的子網路中，這通常應該不致於構成問題。</span><span class="sxs-lookup"><span data-stu-id="26491-117">This normally should not be a problem as long as App Service Environments are deployed into a subnet reserved for exclusive use by only the App Service Environment.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="outbound-connectivity-and-dns-requirements"></a><span data-ttu-id="26491-118">輸出連線和 DNS 需求</span><span class="sxs-lookup"><span data-stu-id="26491-118">Outbound Connectivity and DNS Requirements</span></span>
<span data-ttu-id="26491-119">為了讓 App Service 環境正確運作，它需要不同端點的輸出存取權。</span><span class="sxs-lookup"><span data-stu-id="26491-119">For an App Service Environment to function properly, it requires outbound access to various endpoints.</span></span> <span data-ttu-id="26491-120">[ExpressRoute 的網路組態](app-service-app-service-environment-network-configuration-expressroute.md#required-network-connectivity) 文章的＜需要的網路連線＞一節中有提供 ASE 所使用的外部端點完整清單。</span><span class="sxs-lookup"><span data-stu-id="26491-120">A full list of the external endpoints used by an ASE is in the "Required Network Connectivity" section of the [Network Configuration for ExpressRoute](app-service-app-service-environment-network-configuration-expressroute.md#required-network-connectivity) article.</span></span>

<span data-ttu-id="26491-121">App Service 環境需要針對虛擬網路設定的有效 DNS 基礎結構。</span><span class="sxs-lookup"><span data-stu-id="26491-121">App Service Environments require a valid DNS infrastructure configured for the virtual network.</span></span>  <span data-ttu-id="26491-122">如果 DNS 設定在建立 App Service 環境之後因為任何原因而變更，開發人員可以強制 App Service 環境挑選新的 DNS 組態。</span><span class="sxs-lookup"><span data-stu-id="26491-122">If for any reason the DNS configuration is changed after an App Service Environment has been created, developers can force an App Service Environment to pick up the new DNS configuration.</span></span>  <span data-ttu-id="26491-123">使用位於入口網站中 [App Service 環境管理] 刀鋒視窗頂端的 [重新啟動] 圖示觸發輪流環境重新開機，會導致環境挑選新的 DNS 組態。</span><span class="sxs-lookup"><span data-stu-id="26491-123">Triggering a rolling environment reboot using the "Restart" icon located at the top of the App Service Environment management blade in the portal will cause the environment to pick up the new DNS configuration.</span></span>

<span data-ttu-id="26491-124">也建議事先在虛擬網路上設定任何自訂 DNS 伺服器，再建立 App Service 環境。</span><span class="sxs-lookup"><span data-stu-id="26491-124">It is also recommended that any custom DNS servers on the vnet be setup ahead of time prior to creating an App Service Environment.</span></span>  <span data-ttu-id="26491-125">如果在建立 App Service 環境時變更虛擬網路的 DNS 組態，則會導致 App Service 環境建立程序失敗。</span><span class="sxs-lookup"><span data-stu-id="26491-125">If a virtual network's DNS configuration is changed while an App Service Environment is being created, that will result in the App Service Environment creation process failing.</span></span>  <span data-ttu-id="26491-126">同樣地，若自訂 DNS 伺服器存在於 VPN 閘道的另一端，且 DNS 伺服器無法連線或使用，則 App Service 環境建立程序也會失敗。</span><span class="sxs-lookup"><span data-stu-id="26491-126">In a similar vein, if a custom DNS server exists on the other end of a VPN gateway, and the DNS server is unreachable or unavailable, the App Service Environment creation process will also fail.</span></span>

## <a name="connecting-to-a-sql-server"></a><span data-ttu-id="26491-127">連接至 SQL Server</span><span class="sxs-lookup"><span data-stu-id="26491-127">Connecting to a SQL Server</span></span>
<span data-ttu-id="26491-128">常見的 SQL Server 組態會有在連接埠 1433 上接聽的端點：</span><span class="sxs-lookup"><span data-stu-id="26491-128">A common SQL Server configuration has an endpoint listening on port 1433:</span></span>

![SQL Server 端點][SqlServerEndpoint]

<span data-ttu-id="26491-130">有兩種方法可限制送至此端點的流量：</span><span class="sxs-lookup"><span data-stu-id="26491-130">There are two approaches for restricting traffic to this endpoint:</span></span>

* <span data-ttu-id="26491-131">[網路存取控制清單][NetworkAccessControlLists] (網路 ACL)</span><span class="sxs-lookup"><span data-stu-id="26491-131">[Network Access Control Lists][NetworkAccessControlLists] (Network ACLs)</span></span>
* <span data-ttu-id="26491-132">[網路安全性群組][NetworkSecurityGroups]</span><span class="sxs-lookup"><span data-stu-id="26491-132">[Network Security Groups][NetworkSecurityGroups]</span></span>

## <a name="restricting-access-with-a-network-acl"></a><span data-ttu-id="26491-133">利用網路 ACL 限制存取</span><span class="sxs-lookup"><span data-stu-id="26491-133">Restricting Access With a Network ACL</span></span>
<span data-ttu-id="26491-134">使用網路存取控制清單可以保護連接埠 1433。</span><span class="sxs-lookup"><span data-stu-id="26491-134">Port 1433 can be secured using a network access control list.</span></span>  <span data-ttu-id="26491-135">下列範例將源自虛擬網路內部的用戶端位址列入白名單，並封鎖對所有其他用戶端的存取。</span><span class="sxs-lookup"><span data-stu-id="26491-135">The example below whitelists client addresses originating from inside of a virtual network, and blocks access to all other clients.</span></span>

![網路存取控制清單範例][NetworkAccessControlListExample]

<span data-ttu-id="26491-137">在與 SQL Server 相同虛擬網路的 App Service 環境中執行的所有應用程式，都將能夠使用 SQL Server 虛擬機器的 **VNet 內部** IP 位址連接到 SQL Server 執行個體。</span><span class="sxs-lookup"><span data-stu-id="26491-137">Any applications running in App Service Environment in the same virtual network as the SQL Server will be able to connect to the SQL Server instance using the **VNet internal** IP address for the SQL Server virtual machine.</span></span>  

<span data-ttu-id="26491-138">下列連接字串範例會使用其私密 IP 位址參考 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="26491-138">The example connection string below references the SQL Server using its private IP address.</span></span>

    Server=tcp:10.0.1.6;Database=MyDatabase;User ID=MyUser;Password=PasswordHere;provider=System.Data.SqlClient

<span data-ttu-id="26491-139">雖然虛擬機器也有公用端點，但使用公用 IP 位址的連接嘗試將會因為網路 ACL 而遭到拒絕。</span><span class="sxs-lookup"><span data-stu-id="26491-139">Although the virtual machine has a public endpoint as well, connection attempts using the public IP address will be rejected because of the network ACL.</span></span> 

## <a name="restricting-access-with-a-network-security-group"></a><span data-ttu-id="26491-140">利用網路安全性群組限制存取</span><span class="sxs-lookup"><span data-stu-id="26491-140">Restricting Access With a Network Security Group</span></span>
<span data-ttu-id="26491-141">另一種保護存取安全的方法是利用網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="26491-141">An alternative approach for securing access is with a network security group.</span></span>  <span data-ttu-id="26491-142">網路安全性群組可以套用到個別的虛擬機器，或含有虛擬機器的子網路。</span><span class="sxs-lookup"><span data-stu-id="26491-142">Network security groups can be applied to individual virtual machines, or to a subnet containing virtual machines.</span></span>

<span data-ttu-id="26491-143">首先需要建立網路安全性群組：</span><span class="sxs-lookup"><span data-stu-id="26491-143">First a network security group needs to be created:</span></span>

    New-AzureNetworkSecurityGroup -Name "testNSGexample" -Location "South Central US" -Label "Example network security group for an app service environment"

<span data-ttu-id="26491-144">利用網路安全性群組來限制僅只存取 VNet 內部流量極為容易。</span><span class="sxs-lookup"><span data-stu-id="26491-144">Restricting access to only VNet internal traffic is very simple with a network security group.</span></span>  <span data-ttu-id="26491-145">網路安全性群組中的預設規則只允許從相同虛擬網路中的其他網路用戶端存取。</span><span class="sxs-lookup"><span data-stu-id="26491-145">The default rules in a network security group only allow access from other network clients in the same virtual network.</span></span>

<span data-ttu-id="26491-146">因此鎖定 SQL Server 的存取權，就如同將網路安全性群組及其預設規則套用到執行 SQL Server 的虛擬機器或含有虛擬機器的子網路一樣簡單。</span><span class="sxs-lookup"><span data-stu-id="26491-146">As a result locking down access to SQL Server is as simple as applying a network security group with its default rules to either the virtual machines running SQL Server, or the subnet containing the virtual machines.</span></span>

<span data-ttu-id="26491-147">下列範例將網路安全性群組套用至包含的子網路：</span><span class="sxs-lookup"><span data-stu-id="26491-147">The sample below applies a network security group to the containing subnet:</span></span>

    Get-AzureNetworkSecurityGroup -Name "testNSGExample" | Set-AzureNetworkSecurityGroupToSubnet -VirtualNetworkName 'testVNet' -SubnetName 'Subnet-1'

<span data-ttu-id="26491-148">最終結果是一組可封鎖外部存取，同時允許 VNet 內部存取的安全性規則：</span><span class="sxs-lookup"><span data-stu-id="26491-148">The end result is a set of security rules that block external access, while allowing VNet internal access:</span></span>

![預設網路安全性規則][DefaultNetworkSecurityRules]

## <a name="getting-started"></a><span data-ttu-id="26491-150">開始使用</span><span class="sxs-lookup"><span data-stu-id="26491-150">Getting started</span></span>
<span data-ttu-id="26491-151">您可以在 [應用程式服務環境的讀我檔案](../app-service/app-service-app-service-environments-readme.md)中取得 App Service 環境的所有相關文章與做法。</span><span class="sxs-lookup"><span data-stu-id="26491-151">All articles and How-To's for App Service Environments are available in the [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="26491-152">若要開始使用 App Service Environment，請參閱 [App Service Environment 簡介][IntroToAppServiceEnvironment]</span><span class="sxs-lookup"><span data-stu-id="26491-152">To get started with App Service Environments, see [Introduction to App Service Environment][IntroToAppServiceEnvironment]</span></span>

<span data-ttu-id="26491-153">如需控制 App Service 環境輸入流量的詳細資訊，請參閱[控制 App Service 環境的輸入流量][ControlInboundASE]</span><span class="sxs-lookup"><span data-stu-id="26491-153">For details around controlling inbound traffic to your App Service Environment, see [Controlling inbound traffic to an App Service Environment][ControlInboundASE]</span></span>

<span data-ttu-id="26491-154">如需有關 Azure App Service 平台的詳細資訊，請參閱 [Azure App Service][AzureAppService]。</span><span class="sxs-lookup"><span data-stu-id="26491-154">For more information about the Azure App Service platform, see [Azure App Service][AzureAppService].</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[virtualnetwork]: https://azure.microsoft.com/documentation/articles/virtual-networks-faq/
[ControlInboundTraffic]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/
[SiteToSite]: https://azure.microsoft.com/documentation/articles/vpn-gateway-site-to-site-create/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
[NetworkAccessControlLists]: https://azure.microsoft.com/documentation/articles/virtual-networks-acl/
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[IntroToAppServiceEnvironment]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/ 
[ControlInboundASE]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/ 

<!-- IMAGES -->
[SqlServerEndpoint]: ./media/app-service-app-service-environment-securely-connecting-to-backend-resources/SqlServerEndpoint01.png
[NetworkAccessControlListExample]: ./media/app-service-app-service-environment-securely-connecting-to-backend-resources/NetworkAcl01.png
[DefaultNetworkSecurityRules]: ./media/app-service-app-service-environment-securely-connecting-to-backend-resources/DefaultNetworkSecurityRules01.png 
