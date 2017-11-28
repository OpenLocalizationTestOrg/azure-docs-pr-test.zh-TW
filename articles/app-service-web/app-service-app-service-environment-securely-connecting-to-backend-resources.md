---
title: "aaaSecurely 連接 tooBackEnd App Service 環境的資源"
description: "深入了解 toosecurely 從 App Service 環境連接 toobackend 資源的方式。"
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
ms.openlocfilehash: 6311d3fc301512ea3c4ed8f14f268f75755aa415
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="securely-connecting-toobackend-resources-from-an-app-service-environment"></a><span data-ttu-id="28586-103">安全地連接 tooBackend App Service 環境的資源</span><span class="sxs-lookup"><span data-stu-id="28586-103">Securely Connecting tooBackend Resources from an App Service Environment</span></span>
## <a name="overview"></a><span data-ttu-id="28586-104">概觀</span><span class="sxs-lookup"><span data-stu-id="28586-104">Overview</span></span>
<span data-ttu-id="28586-105">因為永遠建立 App Service 環境**任一**Azure 資源管理員的虛擬網路，**或**傳統部署模型[虛擬網路][ virtualnetwork]，App Service 環境 tooother 後端資源的傳出連線以獨佔方式可以經過 hello 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="28586-105">Since an App Service Environment is always created in **either** an Azure Resource Manager virtual network, **or** a classic deployment model [virtual network][virtualnetwork], outbound connections from an App Service Environment tooother backend resources can flow exclusively over hello virtual network.</span></span>  <span data-ttu-id="28586-106">在 2016 年 6 月所進行的最新變更之後，ASE 也可以部署到使用公用位址範圍或 RFC1918 位址空間 (也就是私人位址) 的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="28586-106">With a recent change made in June 2016, ASEs can also be deployed into virtual networks that use either public address ranges, or RFC1918 address spaces (i.e. private addresses).</span></span>  

<span data-ttu-id="28586-107">例如，SQL Server 可能會在已鎖定連接埠 1433 的虛擬機器叢集上執行。</span><span class="sxs-lookup"><span data-stu-id="28586-107">For example, there may be a SQL Server running on a cluster of virtual machines with port 1433 locked down.</span></span>  <span data-ttu-id="28586-108">hello 端點可能是的 ACLd tooonly 允許從其他資源的存取 hello 相同虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="28586-108">hello endpoint may be ACLd tooonly allow access from other resources on hello same virtual network.</span></span>  

<span data-ttu-id="28586-109">另舉一例，機密端點可能在內部部署執行，且不連線的 tooAzure 經由下列[站對站][ SiteToSite]或[Azure ExpressRoute] [ ExpressRoute]連線。</span><span class="sxs-lookup"><span data-stu-id="28586-109">As another example, sensitive endpoints may run on-premises and be connected tooAzure via either [Site-to-Site][SiteToSite] or [Azure ExpressRoute][ExpressRoute] connections.</span></span>  <span data-ttu-id="28586-110">如此一來，只有在虛擬網路中的資源連接 toohello 站對站或 ExpressRoute 通道將會無法 tooaccess 內部端點。</span><span class="sxs-lookup"><span data-stu-id="28586-110">As a result, only resources in virtual networks connected toohello Site-to-Site or ExpressRoute tunnels will be able tooaccess on-premises endpoints.</span></span>

<span data-ttu-id="28586-111">針對所有這些情況下，App Service 環境上執行應用程式將無法 toosecurely 連接 toohello 各種伺服器和資源。</span><span class="sxs-lookup"><span data-stu-id="28586-111">For all of these scenarios, apps running on an App Service Environment will be able toosecurely connect toohello various servers and resources.</span></span>  <span data-ttu-id="28586-112">從執行中 hello App Service 環境 tooprivate 端點中的應用程式的輸出流量相同虛擬網路 (或連接 toohello 相同虛擬網路)，將只流程 hello 虛擬網路上。</span><span class="sxs-lookup"><span data-stu-id="28586-112">Outbound traffic from apps running in an App Service Environment tooprivate endpoints in hello same virtual network (or connected toohello same virtual network), will only flow over hello virtual network.</span></span>  <span data-ttu-id="28586-113">端點不會透過輸出流量 tooprivate hello 公用網際網路。</span><span class="sxs-lookup"><span data-stu-id="28586-113">Outbound traffic tooprivate endpoints will not flow over hello public Internet.</span></span>

<span data-ttu-id="28586-114">必須注意套用虛擬網路內的 App Service 環境 tooendpoints toooutbound 流量。</span><span class="sxs-lookup"><span data-stu-id="28586-114">One caveat applies toooutbound traffic from an App Service Environment tooendpoints within a virtual network.</span></span>  <span data-ttu-id="28586-115">應用程式服務環境無法連線到端點的虛擬機器位於 hello**相同**為 hello App Service 環境的子網路。</span><span class="sxs-lookup"><span data-stu-id="28586-115">App Service Environments cannot reach endpoints of virtual machines located in hello **same** subnet as hello App Service Environment.</span></span>  <span data-ttu-id="28586-116">這通常不應該有問題，只要應用程式服務環境已部署到保留給專用 hello App Service 環境的子網路。</span><span class="sxs-lookup"><span data-stu-id="28586-116">This normally should not be a problem as long as App Service Environments are deployed into a subnet reserved for exclusive use by only hello App Service Environment.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="outbound-connectivity-and-dns-requirements"></a><span data-ttu-id="28586-117">輸出連線和 DNS 需求</span><span class="sxs-lookup"><span data-stu-id="28586-117">Outbound Connectivity and DNS Requirements</span></span>
<span data-ttu-id="28586-118">App Service 環境 toofunction 正常運作，它需要對外存取 toovarious 端點。</span><span class="sxs-lookup"><span data-stu-id="28586-118">For an App Service Environment toofunction properly, it requires outbound access toovarious endpoints.</span></span> <span data-ttu-id="28586-119">Hello hello 」 所需的網路連接性 」 一節中的 hello ase 中所使用的外部端點的完整清單位於[expressroute 的網路組態](app-service-app-service-environment-network-configuration-expressroute.md#required-network-connectivity)發行項。</span><span class="sxs-lookup"><span data-stu-id="28586-119">A full list of hello external endpoints used by an ASE is in hello "Required Network Connectivity" section of hello [Network Configuration for ExpressRoute](app-service-app-service-environment-network-configuration-expressroute.md#required-network-connectivity) article.</span></span>

<span data-ttu-id="28586-120">App Service 環境需要有效的 DNS 基礎結構，設定 hello 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="28586-120">App Service Environments require a valid DNS infrastructure configured for hello virtual network.</span></span>  <span data-ttu-id="28586-121">如果任何原因 hello DNS 設定會變更在建立 App Service 環境之後，開發人員可以強制的 App Service 環境 toopick hello 新的 DNS 設定。</span><span class="sxs-lookup"><span data-stu-id="28586-121">If for any reason hello DNS configuration is changed after an App Service Environment has been created, developers can force an App Service Environment toopick up hello new DNS configuration.</span></span>  <span data-ttu-id="28586-122">觸發輪流的環境重新開機，使用位於頂端 hello hello App Service 環境的 hello 「 重新啟動 」 圖示 hello 入口網站中的管理刀鋒視窗，將會導致 hello 環境 toopick hello 新的 DNS 設定。</span><span class="sxs-lookup"><span data-stu-id="28586-122">Triggering a rolling environment reboot using hello "Restart" icon located at hello top of hello App Service Environment management blade in hello portal will cause hello environment toopick up hello new DNS configuration.</span></span>

<span data-ttu-id="28586-123">也建議 hello vnet 上的任何自訂 DNS 伺服器會預先時間先前 toocreating App Service 環境的安裝程式。</span><span class="sxs-lookup"><span data-stu-id="28586-123">It is also recommended that any custom DNS servers on hello vnet be setup ahead of time prior toocreating an App Service Environment.</span></span>  <span data-ttu-id="28586-124">如果在建立 App Service 環境期間變更虛擬網路的 DNS 設定，，因而造成 hello App Service 環境建立程序失敗。</span><span class="sxs-lookup"><span data-stu-id="28586-124">If a virtual network's DNS configuration is changed while an App Service Environment is being created, that will result in hello App Service Environment creation process failing.</span></span>  <span data-ttu-id="28586-125">同樣地，如果自訂的 DNS 伺服器 hello 存在於另一端的 VPN 閘道和 hello DNS 伺服器會為無法連線到或無法使用，hello App Service 環境的建立程序也會失敗。</span><span class="sxs-lookup"><span data-stu-id="28586-125">In a similar vein, if a custom DNS server exists on hello other end of a VPN gateway, and hello DNS server is unreachable or unavailable, hello App Service Environment creation process will also fail.</span></span>

## <a name="connecting-tooa-sql-server"></a><span data-ttu-id="28586-126">連接 SQL Server tooa</span><span class="sxs-lookup"><span data-stu-id="28586-126">Connecting tooa SQL Server</span></span>
<span data-ttu-id="28586-127">常見的 SQL Server 組態會有在連接埠 1433 上接聽的端點：</span><span class="sxs-lookup"><span data-stu-id="28586-127">A common SQL Server configuration has an endpoint listening on port 1433:</span></span>

![SQL Server 端點][SqlServerEndpoint]

<span data-ttu-id="28586-129">有兩種方法來限制流量 toothis 端點：</span><span class="sxs-lookup"><span data-stu-id="28586-129">There are two approaches for restricting traffic toothis endpoint:</span></span>

* <span data-ttu-id="28586-130">[網路存取控制清單][NetworkAccessControlLists] (網路 ACL)</span><span class="sxs-lookup"><span data-stu-id="28586-130">[Network Access Control Lists][NetworkAccessControlLists] (Network ACLs)</span></span>
* <span data-ttu-id="28586-131">[網路安全性群組][NetworkSecurityGroups]</span><span class="sxs-lookup"><span data-stu-id="28586-131">[Network Security Groups][NetworkSecurityGroups]</span></span>

## <a name="restricting-access-with-a-network-acl"></a><span data-ttu-id="28586-132">利用網路 ACL 限制存取</span><span class="sxs-lookup"><span data-stu-id="28586-132">Restricting Access With a Network ACL</span></span>
<span data-ttu-id="28586-133">使用網路存取控制清單可以保護連接埠 1433。</span><span class="sxs-lookup"><span data-stu-id="28586-133">Port 1433 can be secured using a network access control list.</span></span>  <span data-ttu-id="28586-134">白名單用戶端的 hello 下例源自內虛擬網路，並封鎖存取 tooall 其他用戶端。</span><span class="sxs-lookup"><span data-stu-id="28586-134">hello example below whitelists client addresses originating from inside of a virtual network, and blocks access tooall other clients.</span></span>

![網路存取控制清單範例][NetworkAccessControlListExample]

<span data-ttu-id="28586-136">中的 App Service 環境中執行的任何應用程式 hello 相同虛擬網路，當 hello SQL Server 將會無法 tooconnect toohello SQL Server 執行個體使用 hello **VNet 內部**hello SQL Server 虛擬機器的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="28586-136">Any applications running in App Service Environment in hello same virtual network as hello SQL Server will be able tooconnect toohello SQL Server instance using hello **VNet internal** IP address for hello SQL Server virtual machine.</span></span>  

<span data-ttu-id="28586-137">下面參考 hello 範例連接字串 hello 使用其私人 IP 位址的 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="28586-137">hello example connection string below references hello SQL Server using its private IP address.</span></span>

    Server=tcp:10.0.1.6;Database=MyDatabase;User ID=MyUser;Password=PasswordHere;provider=System.Data.SqlClient

<span data-ttu-id="28586-138">雖然 hello 虛擬機器有為公用的端點，但是使用 hello 公用 IP 位址的連接嘗試會遭到拒絕因為 hello 網路 ACL。</span><span class="sxs-lookup"><span data-stu-id="28586-138">Although hello virtual machine has a public endpoint as well, connection attempts using hello public IP address will be rejected because of hello network ACL.</span></span> 

## <a name="restricting-access-with-a-network-security-group"></a><span data-ttu-id="28586-139">利用網路安全性群組限制存取</span><span class="sxs-lookup"><span data-stu-id="28586-139">Restricting Access With a Network Security Group</span></span>
<span data-ttu-id="28586-140">另一種保護存取安全的方法是利用網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="28586-140">An alternative approach for securing access is with a network security group.</span></span>  <span data-ttu-id="28586-141">套用的 tooindividual 虛擬機器或包含虛擬機器的 tooa 子網路，可以是網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="28586-141">Network security groups can be applied tooindividual virtual machines, or tooa subnet containing virtual machines.</span></span>

<span data-ttu-id="28586-142">第一次網路安全性小組需要建立 toobe:</span><span class="sxs-lookup"><span data-stu-id="28586-142">First a network security group needs toobe created:</span></span>

    New-AzureNetworkSecurityGroup -Name "testNSGexample" -Location "South Central US" -Label "Example network security group for an app service environment"

<span data-ttu-id="28586-143">限制存取 tooonly VNet 內部流量是非常簡單的網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="28586-143">Restricting access tooonly VNet internal traffic is very simple with a network security group.</span></span>  <span data-ttu-id="28586-144">網路安全性群組中的 hello 預設規則僅允許存取網路中其他用戶端 hello 從相同虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="28586-144">hello default rules in a network security group only allow access from other network clients in hello same virtual network.</span></span>

<span data-ttu-id="28586-145">如此一來鎖定存取 tooSQL 伺服器很簡單，只套用其預設規則 tooeither hello 與虛擬機器搭配執行 SQL Server 或包含 hello 虛擬機器的 hello 子網路的網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="28586-145">As a result locking down access tooSQL Server is as simple as applying a network security group with its default rules tooeither hello virtual machines running SQL Server, or hello subnet containing hello virtual machines.</span></span>

<span data-ttu-id="28586-146">以下的 hello 範例適用於安全性群組 toohello 包含子網路：</span><span class="sxs-lookup"><span data-stu-id="28586-146">hello sample below applies a network security group toohello containing subnet:</span></span>

    Get-AzureNetworkSecurityGroup -Name "testNSGExample" | Set-AzureNetworkSecurityGroupToSubnet -VirtualNetworkName 'testVNet' -SubnetName 'Subnet-1'

<span data-ttu-id="28586-147">hello 最終結果是一組區塊外部存取，同時允許 VNet 內部存取的安全性規則：</span><span class="sxs-lookup"><span data-stu-id="28586-147">hello end result is a set of security rules that block external access, while allowing VNet internal access:</span></span>

![預設網路安全性規則][DefaultNetworkSecurityRules]

## <a name="getting-started"></a><span data-ttu-id="28586-149">開始使用</span><span class="sxs-lookup"><span data-stu-id="28586-149">Getting started</span></span>
<span data-ttu-id="28586-150">所有發行項以及-的應用程式服務環境的 hello[讀我檔案的應用程式服務環境](../app-service/app-service-app-service-environments-readme.md)。</span><span class="sxs-lookup"><span data-stu-id="28586-150">All articles and How-To's for App Service Environments are available in hello [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="28586-151">tooget 開始使用應用程式服務環境中，請參閱[簡介 tooApp Service 環境][IntroToAppServiceEnvironment]</span><span class="sxs-lookup"><span data-stu-id="28586-151">tooget started with App Service Environments, see [Introduction tooApp Service Environment][IntroToAppServiceEnvironment]</span></span>

<span data-ttu-id="28586-152">如需周圍控制輸入的流量 tooyour App Service 環境的詳細資訊，請參閱[控制輸入的流量 tooan App Service 環境][ControlInboundASE]</span><span class="sxs-lookup"><span data-stu-id="28586-152">For details around controlling inbound traffic tooyour App Service Environment, see [Controlling inbound traffic tooan App Service Environment][ControlInboundASE]</span></span>

<span data-ttu-id="28586-153">如需 hello Azure 應用程式服務平台的詳細資訊，請參閱[Azure App Service][AzureAppService]。</span><span class="sxs-lookup"><span data-stu-id="28586-153">For more information about hello Azure App Service platform, see [Azure App Service][AzureAppService].</span></span>

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
