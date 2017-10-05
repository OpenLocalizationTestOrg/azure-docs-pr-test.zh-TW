---
title: "使用 ExpressRoute 的網路組態詳細資料"
description: "在連接至 ExpressRoute 循環之虛擬網路中執行 App Service 環境的網路組態詳細資料。"
services: app-service
documentationcenter: 
author: stefsch
manager: nirma
editor: 
ms.assetid: 34b49178-2595-4d32-9b41-110c96dde6bf
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/14/2016
ms.author: stefsch
ms.openlocfilehash: de1d998ee86c127149dee18e9df577705054ddb4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="network-configuration-details-for-app-service-environments-with-expressroute"></a><span data-ttu-id="632de-103">使用 ExpressRoute 之 App Service 環境的網路組態詳細資料</span><span class="sxs-lookup"><span data-stu-id="632de-103">Network Configuration Details for App Service Environments with ExpressRoute</span></span>
## <a name="overview"></a><span data-ttu-id="632de-104">概觀</span><span class="sxs-lookup"><span data-stu-id="632de-104">Overview</span></span>
<span data-ttu-id="632de-105">客戶可以將 [Azure ExpressRoute][ExpressRoute] 循環連接至虛擬網路基礎結構，因而將其內部部署網路延伸至 Azure。</span><span class="sxs-lookup"><span data-stu-id="632de-105">Customers can connect an [Azure ExpressRoute][ExpressRoute] circuit to their virtual network infrastructure, thus extending their on-premises network to Azure.</span></span>  <span data-ttu-id="632de-106">您可以在這個[虛擬網路][virtualnetwork]基礎結構的子網路中建立 App Service 環境。</span><span class="sxs-lookup"><span data-stu-id="632de-106">An App Service Environment can  be created in a subnet of this [virtual network][virtualnetwork] infrastructure.</span></span>  <span data-ttu-id="632de-107">在 App Service 環境上執行的應用程式接著可以建立與後端資源的安全連線，而後端資源只能透過 ExpressRoute 連線來存取。</span><span class="sxs-lookup"><span data-stu-id="632de-107">Apps running on the App Service Environment can then establish secure connections to back-end resources accessible only over the ExpressRoute connection.</span></span>  

<span data-ttu-id="632de-108">您可以在 Azure Resource Manager 虛擬網路**或**傳統式部署模型虛擬網路中建立 App Service 環境。</span><span class="sxs-lookup"><span data-stu-id="632de-108">An App Service Environment can be created in **either** an Azure Resource Manager virtual network, **or** a classic deployment model virtual network.</span></span>  <span data-ttu-id="632de-109">在 2016 年 6 月所進行的最新變更之後，ASE 現在也可以部署到使用公用位址範圍或 RFC1918 位址空間 (也就是</span><span class="sxs-lookup"><span data-stu-id="632de-109">With a recent change made in June 2016, ASEs can also now be deployed into virtual networks that use either public address ranges, or RFC1918 address spaces (i.e.</span></span> <span data-ttu-id="632de-110">私人位址) 的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="632de-110">private addresses).</span></span> 

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="required-network-connectivity"></a><span data-ttu-id="632de-111">需要的網路連線</span><span class="sxs-lookup"><span data-stu-id="632de-111">Required Network Connectivity</span></span>
<span data-ttu-id="632de-112">在連接至 ExpressRoute 的虛擬網路中，可能一開始會不符合 App Service 環境的一些網路連線需求。</span><span class="sxs-lookup"><span data-stu-id="632de-112">There are network connectivity requirements for App Service Environments that may not be initially met in a virtual network connected to an ExpressRoute.</span></span>  <span data-ttu-id="632de-113">App Service 環境需要下列所有項目，才能正確運作：</span><span class="sxs-lookup"><span data-stu-id="632de-113">App Service Environments require all of the following in order to function properly:</span></span>

* <span data-ttu-id="632de-114">在連接埠 80 與 443 上，全球 Azure 儲存體端點的輸出網路連線能力。</span><span class="sxs-lookup"><span data-stu-id="632de-114">Outbound network connectivity to Azure Storage endpoints worldwide on both ports 80 and 443.</span></span>  <span data-ttu-id="632de-115">這包括位於與 App Service 環境相同區域中的端點，以及位於「其他」  Azure 區域的儲存體端點。</span><span class="sxs-lookup"><span data-stu-id="632de-115">This includes endpoints located in the same region as the App Service Environment, as well as storage endpoints located in **other** Azure regions.</span></span>  <span data-ttu-id="632de-116">Azure 儲存體端點在下列 DNS 網域之下解析：table.core.windows.net、blob.core.windows.net、queue.core.windows.net 和 file.core.windows.net。</span><span class="sxs-lookup"><span data-stu-id="632de-116">Azure Storage endpoints resolve under the following DNS domains: *table.core.windows.net*, *blob.core.windows.net*, *queue.core.windows.net* and *file.core.windows.net*.</span></span>  
* <span data-ttu-id="632de-117">位於連接埠 445 的 Azure 檔案服務的輸出網路連線</span><span class="sxs-lookup"><span data-stu-id="632de-117">Outbound network connectivity to the Azure Files service on port 445.</span></span>
* <span data-ttu-id="632de-118">位於與 App Service 環境相同區域中的 SQL DB 端點的輸出網路連接。</span><span class="sxs-lookup"><span data-stu-id="632de-118">Outbound network connectivity to Sql DB endpoints located in the same region as the App Service Environment.</span></span>  <span data-ttu-id="632de-119">Sql DB 端點在下列網域之下解析：database.windows.net。</span><span class="sxs-lookup"><span data-stu-id="632de-119">Sql DB endpoints resolve under the following domain:  *database.windows.net*.</span></span>  <span data-ttu-id="632de-120">這需要開啟連接埠 1433、11000-11999 和 14000 14999 的存取。</span><span class="sxs-lookup"><span data-stu-id="632de-120">This requires opening access to ports 1433, 11000-11999 and 14000-14999.</span></span>  <span data-ttu-id="632de-121">如需詳細資訊，請參閱 [Sql Database V12 連接埠使用方式](../sql-database/sql-database-develop-direct-route-ports-adonet-v12.md)一文。</span><span class="sxs-lookup"><span data-stu-id="632de-121">For more details see [this article on Sql Database V12 port usage](../sql-database/sql-database-develop-direct-route-ports-adonet-v12.md).</span></span>
* <span data-ttu-id="632de-122">Azure 管理平面端點 (ASM 和 ARM 端點) 的輸出網路連線。</span><span class="sxs-lookup"><span data-stu-id="632de-122">Outbound network connectivity to the Azure management plane endpoints (both ASM and ARM endpoints).</span></span>  <span data-ttu-id="632de-123">這包括 management.core.windows.net 和 management.azure.com 的輸出連線。</span><span class="sxs-lookup"><span data-stu-id="632de-123">This includes outbound connectivity to both *management.core.windows.net* and *management.azure.com*.</span></span> 
* <span data-ttu-id="632de-124">ocsp.msocsp.com、mscrl.microsoft.com 和 crl.microsoft.com 的輸出網路連線。</span><span class="sxs-lookup"><span data-stu-id="632de-124">Outbound network connectivity to *ocsp.msocsp.com*, *mscrl.microsoft.com* and *crl.microsoft.com*.</span></span>  <span data-ttu-id="632de-125">需要此連線才能支援 SSL 功能。</span><span class="sxs-lookup"><span data-stu-id="632de-125">This is needed to support SSL functionality.</span></span>
* <span data-ttu-id="632de-126">虛擬網路的 DNS 設定必須能夠解析前面幾點所提到的所有端點和網域。</span><span class="sxs-lookup"><span data-stu-id="632de-126">The DNS configuration for the virtual network must be capable of resolving all of the endpoints and domains mentioned in the earlier points.</span></span>  <span data-ttu-id="632de-127">如果無法解析這些端點，App Service 環境建立嘗試將會失敗，而且現有的 App Service 環境會標示為狀況不良。</span><span class="sxs-lookup"><span data-stu-id="632de-127">If these endpoints cannot be resolved, App Service Environment creation attempts will fail, and existing App Service Environments will be marked as unhealthy.</span></span>
* <span data-ttu-id="632de-128">需要有連接埠 53 的輸出存取，才能與 DNS 伺服器通訊。</span><span class="sxs-lookup"><span data-stu-id="632de-128">Outbound access on port 53 is required for communication with DNS servers.</span></span>
* <span data-ttu-id="632de-129">如果 VPN 閘道的另一端有自訂 DNS 伺服器存在，則必須可從包含 App Service 環境的子網路連接該 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="632de-129">If a custom DNS server exists on the other end of a VPN gateway, the DNS server must be reachable from the subnet containing the App Service Environment.</span></span> 
* <span data-ttu-id="632de-130">輸出網路路徑不可經過內部公司 Proxy，也不可使用強制通道傳送至內部部署。</span><span class="sxs-lookup"><span data-stu-id="632de-130">The outbound network path cannot travel through internal corporate proxies, nor can it be force tunneled to on-premises.</span></span>  <span data-ttu-id="632de-131">這麼會變更來自 App Service 環境的輸出網路流量的有效 NAT 位址。</span><span class="sxs-lookup"><span data-stu-id="632de-131">Doing so changes the effective NAT address of outbound network traffic from the App Service Environment.</span></span>  <span data-ttu-id="632de-132">變更 App Service 環境之輸出網路流量的 NAT 位址會導致上述眾多端點的連接失敗。</span><span class="sxs-lookup"><span data-stu-id="632de-132">Changing the NAT address of an App Service Environment's outbound network traffic will cause connectivity failures to many of the endpoints listed above.</span></span>  <span data-ttu-id="632de-133">這會導致 App Service 環境建立嘗試失敗，而之前狀況良好的 App Service 環境會標示為狀況不良。</span><span class="sxs-lookup"><span data-stu-id="632de-133">This results in failed App Service Environment creation attempts, as well as previously healthy App Service Environments being marked as unhealthy.</span></span>  
* <span data-ttu-id="632de-134">如[本文][requiredports]所述，您必須允許輸入網路存取 App Service 環境的必要連接埠。</span><span class="sxs-lookup"><span data-stu-id="632de-134">Inbound network access to required ports for App Service Environments must be allowed as described in this [article][requiredports].</span></span>

<span data-ttu-id="632de-135">確定已針對虛擬網路設定及維護有效的 DNS 基礎結構，即可符合 DNS 需求。</span><span class="sxs-lookup"><span data-stu-id="632de-135">The DNS requirements can be met by ensuring a valid DNS infrastructure is configured and maintained for the virtual network.</span></span>  <span data-ttu-id="632de-136">如果 DNS 設定在建立 App Service 環境之後因為任何原因而變更，開發人員可以強制 App Service 環境挑選新的 DNS 組態。</span><span class="sxs-lookup"><span data-stu-id="632de-136">If for any reason the DNS configuration is changed after an App Service Environment has been created, developers can force an App Service Environment to pick up the new DNS configuration.</span></span>  <span data-ttu-id="632de-137">若是使用位於 [Azure 入口網站][NewPortal]中 [App Service Environment 管理] 刀鋒視窗頂端的 [重新啟動] 圖示來觸發輪流環境重新開機，就會導致環境挑選新的 DNS 組態。</span><span class="sxs-lookup"><span data-stu-id="632de-137">Triggering a rolling environment reboot using the "Restart" icon located at the top of the App Service Environment management blade in the [Azure portal][NewPortal] will cause the environment to pick up the new DNS configuration.</span></span>

<span data-ttu-id="632de-138">在 App Service 環境的子網路上設定[網路安全性群組][NetworkSecurityGroups]以允許必要存取權，即可符合輸入網路存取的需求，如[本文][requiredports]所述。</span><span class="sxs-lookup"><span data-stu-id="632de-138">The inbound network access requirements can be met by configuring a [network security group][NetworkSecurityGroups] on the App Service Environment's subnet to allow the required access as described in this [article][requiredports].</span></span>

## <a name="enabling-outbound-network-connectivity-for-an-app-service-environment"></a><span data-ttu-id="632de-139">啟用 App Service 環境的輸出網路連線</span><span class="sxs-lookup"><span data-stu-id="632de-139">Enabling Outbound Network Connectivity for an App Service Environment</span></span>
<span data-ttu-id="632de-140">新建立的 ExpressRoute 循環預設會通告允許輸出網際網路連線的預設路由。</span><span class="sxs-lookup"><span data-stu-id="632de-140">By default, a newly created ExpressRoute circuit advertises a default route that allows outbound Internet connectivity.</span></span>  <span data-ttu-id="632de-141">使用此組態，App Service 環境將可以連接至其他 Azure 端點。</span><span class="sxs-lookup"><span data-stu-id="632de-141">With this configuration an App Service Environment will be able to connect to other Azure endpoints.</span></span>

<span data-ttu-id="632de-142">不過，常見的客戶組態是定義其專屬預設路由 (0.0.0.0/0)，以強制輸出網際網路流量來替代透過內部部署方式流動。</span><span class="sxs-lookup"><span data-stu-id="632de-142">However a common customer configuration is to define their own default route (0.0.0.0/0) which forces outbound Internet traffic to instead flow on-premises.</span></span>  <span data-ttu-id="632de-143">此流量流程一定會中斷 App Service 環境，因為已透過內部部署方式封鎖輸出流量，或 NAT 至無法再使用各種 Azure 端點的一組無法辨識位址。</span><span class="sxs-lookup"><span data-stu-id="632de-143">This traffic flow invariably breaks App Service Environments because the outbound traffic is either blocked on-premises, or NAT'd to an unrecognizable set of addresses that no longer work with various Azure endpoints.</span></span>

<span data-ttu-id="632de-144">解決方法是在子網路上定義包含 App Service 環境的一 (或多個) 使用者定義路由 (UDR)。</span><span class="sxs-lookup"><span data-stu-id="632de-144">The solution is to define one (or more) user defined routes (UDRs) on the subnet that contains the App Service Environment.</span></span>  <span data-ttu-id="632de-145">UDR 會定義將使用的子網路特有路由，而非預設路由。</span><span class="sxs-lookup"><span data-stu-id="632de-145">A UDR defines subnet-specific routes that will be honored instead of the default route.</span></span>

<span data-ttu-id="632de-146">如果可能，建議使用下列設定：</span><span class="sxs-lookup"><span data-stu-id="632de-146">If possible, it is recommended to use the following configuration:</span></span>

* <span data-ttu-id="632de-147">ExpressRoute 組態會通告 0.0.0.0/0 而且預設會使用強制通道將所有輸出流量傳送至內部部署。</span><span class="sxs-lookup"><span data-stu-id="632de-147">The ExpressRoute configuration advertises 0.0.0.0/0 and by default force tunnels all outbound traffic on-premises.</span></span>
* <span data-ttu-id="632de-148">已套用至包含 App Service 環境之子網路的 UDR 會使用網際網路的下一個躍點類型定義 0.0.0.0/0 (本文後面會提供其範例)。</span><span class="sxs-lookup"><span data-stu-id="632de-148">The UDR applied to the subnet containing the App Service Environment defines 0.0.0.0/0 with a next hop type of Internet (an example of this is farther down in this article).</span></span>

<span data-ttu-id="632de-149">這些步驟的合併效果是子網路層級 UDR 會優先於 ExpressRoute 強制通道，因而確保來自 App Service 環境的輸出網際網路存取。</span><span class="sxs-lookup"><span data-stu-id="632de-149">The combined effect of these steps is that the subnet level UDR will take precedence over the ExpressRoute forced tunneling, thus ensuring outbound Internet access from the App Service Environment.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="632de-150">UDR 中定義的路由**必須**明確足以優先於 ExpressRoute 組態所通告的任何路由。</span><span class="sxs-lookup"><span data-stu-id="632de-150">The routes defined in a UDR **must** be specific enough to  take precedence over any routes advertised by the ExpressRoute configuration.</span></span>  <span data-ttu-id="632de-151">以下範例使用廣泛 0.0.0.0/0 位址範圍，因此使用更明確的位址範圍，有可能會不小心由路由通告所覆寫。</span><span class="sxs-lookup"><span data-stu-id="632de-151">The example below uses the broad 0.0.0.0/0 address range, and as such can potentially be accidentally overridden by route advertisements using more specific address ranges.</span></span>
> 
> <span data-ttu-id="632de-152">**交叉通告從公用對等互連路徑至私人對等互連路徑之路由**的 ExpressRoute 組態不支援 App Service 環境。</span><span class="sxs-lookup"><span data-stu-id="632de-152">App Service Environments are not supported with ExpressRoute configurations that **cross-advertise routes from the public peering path to the private peering path**.</span></span>  <span data-ttu-id="632de-153">已設定公用對等互連的 ExpressRoute 組態，會收到來自 Microsoft 的一大組 Microsoft Azure IP 位址範圍的路由通告。</span><span class="sxs-lookup"><span data-stu-id="632de-153">ExpressRoute configurations that have public peering configured, will receive route advertisements from Microsoft for a large set of Microsoft Azure IP address ranges.</span></span>  <span data-ttu-id="632de-154">如果這些位址範圍在私人對等互連路徑上交叉通告，最後的結果會是來自 App Service 環境子網路的所有輸出網路封包都會使用強制通道傳送至客戶的內部部署網路基礎結構。</span><span class="sxs-lookup"><span data-stu-id="632de-154">If these address ranges are cross-advertised on the private peering path, the end result is that all outbound network packets from the App Service Environment's subnet will be force-tunneled to a customer's on-premises network infrastructure.</span></span>  <span data-ttu-id="632de-155">App Service 環境目前不支援這個網路流量。</span><span class="sxs-lookup"><span data-stu-id="632de-155">This network flow is currently not supported with App Service Environments.</span></span>  <span data-ttu-id="632de-156">此問題的一個解決方案是停止從公用對等互連路徑至私人對等互連路徑的交叉通告路由。</span><span class="sxs-lookup"><span data-stu-id="632de-156">One solution to this problem is to stop cross-advertising routes from the public peering path to the private peering path.</span></span>
> 
> 

<span data-ttu-id="632de-157">如需使用者定義路由的背景資訊，請參閱此[概觀][UDROverview]。</span><span class="sxs-lookup"><span data-stu-id="632de-157">Background information on user defined routes is available in this [overview][UDROverview].</span></span>  

<span data-ttu-id="632de-158">如需建立和設定使用者定義路由的詳細資訊，請參閱此[作法指南][UDRHowTo]。</span><span class="sxs-lookup"><span data-stu-id="632de-158">Details on creating and configuring user defined routes is available in this [How To Guide][UDRHowTo].</span></span>

## <a name="example-udr-configuration-for-an-app-service-environment"></a><span data-ttu-id="632de-159">App Service 環境的範例 UDR 組態</span><span class="sxs-lookup"><span data-stu-id="632de-159">Example UDR Configuration for an App Service Environment</span></span>
<span data-ttu-id="632de-160">**必要條件**</span><span class="sxs-lookup"><span data-stu-id="632de-160">**Pre-requisites**</span></span>

1. <span data-ttu-id="632de-161">從 [Azure 下載頁面][AzureDownloads]安裝 Azure Powershell (日期為 2015 年 6 月或更新版本)。</span><span class="sxs-lookup"><span data-stu-id="632de-161">Install Azure Powershell from the [Azure Downloads page][AzureDownloads] (dated June 2015 or later).</span></span>  <span data-ttu-id="632de-162">在 [命令列工具] 的 [Windows Powershell] 下，有一個 [安裝] 連結可安裝最新的 Powershell Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="632de-162">Under "Command-line tools" there is an "Install" link under "Windows Powershell" that will install the latest Powershell cmdlets.</span></span>
2. <span data-ttu-id="632de-163">建議您建立唯一的子網路，以專供 App Service 環境使用。</span><span class="sxs-lookup"><span data-stu-id="632de-163">It is recommended that a unique subnet is created for exclusive use by an App Service Environment.</span></span>  <span data-ttu-id="632de-164">這可確保套用至子網路的 UDR 只會開啟 App Service 環境的輸出流量。</span><span class="sxs-lookup"><span data-stu-id="632de-164">This ensures that the UDRs applied to the subnet will only open outbound traffic for the App Service Environment.</span></span>
3. <span data-ttu-id="632de-165">**重要事項**：**除非**已經進行下列組態步驟，否則不要部署 App Service 環境。</span><span class="sxs-lookup"><span data-stu-id="632de-165">**Important**:  do not deploy the App Service Environment until **after** the following configuration steps are followed.</span></span>  <span data-ttu-id="632de-166">這可確保輸出網路連線可用，再嘗試部署 App Service 環境。</span><span class="sxs-lookup"><span data-stu-id="632de-166">This ensures that outbound network connectivity is available before attempting to deploy an App Service Environment.</span></span>

<span data-ttu-id="632de-167">**步驟 1：建立具名路由表**</span><span class="sxs-lookup"><span data-stu-id="632de-167">**Step 1:  Create a named route table**</span></span>

<span data-ttu-id="632de-168">下列程式碼片段會在 West US Azure 區域中建立稱為 "DirectInternetRouteTable" 的路由表：</span><span class="sxs-lookup"><span data-stu-id="632de-168">The following snippet creates a route table called "DirectInternetRouteTable" in the West US Azure region:</span></span>

    New-AzureRouteTable -Name 'DirectInternetRouteTable' -Location uswest

<span data-ttu-id="632de-169">**步驟 2：在路由表中建立一或多個路由**</span><span class="sxs-lookup"><span data-stu-id="632de-169">**Step 2:  Create one or more routes in the route table**</span></span>

<span data-ttu-id="632de-170">您必須將一或多個路由新增至路由表中，才能啟用輸出網際網路存取。</span><span class="sxs-lookup"><span data-stu-id="632de-170">You will need to add one or more routes to the route table in order to enable outbound Internet access.</span></span>  

<span data-ttu-id="632de-171">設定網際網路輸出存取的建議方法是定義 0.0.0.0/0 的路由，如下所示。</span><span class="sxs-lookup"><span data-stu-id="632de-171">The recommended approach for configuring outbound access to the Internet is to define a route for 0.0.0.0/0 as shown below.</span></span>

    Get-AzureRouteTable -Name 'DirectInternetRouteTable' | Set-AzureRoute -RouteName 'Direct Internet Range 0' -AddressPrefix 0.0.0.0/0 -NextHopType Internet

<span data-ttu-id="632de-172">請記住 0.0.0.0/0 是廣泛的位址範圍，因此會被 ExpressRoute 所通告的更明確位址範圍所覆寫。</span><span class="sxs-lookup"><span data-stu-id="632de-172">Remember that 0.0.0.0/0 is a broad address range, and as such will be overridden by more specific address ranges advertised by the ExpressRoute.</span></span>  <span data-ttu-id="632de-173">若要重新反覆執行先前的建議，具有 0.0.0.0/0 路由的 UDR 應搭配也只會通告 0.0.0.0/0 的 ExressRoute 組態使用。</span><span class="sxs-lookup"><span data-stu-id="632de-173">To re-iterate the earlier recommendation, a UDR with a 0.0.0.0/0 route should be used in conjunction with an ExressRoute configuration that only advertises 0.0.0.0/0 as well.</span></span> 

<span data-ttu-id="632de-174">或者，您可以下載完整和更新的由 Azure 使用中的 CIDR 範圍清單。</span><span class="sxs-lookup"><span data-stu-id="632de-174">As an alternative, you can download a comprehensive and updated list of CIDR ranges in use by Azure.</span></span>  <span data-ttu-id="632de-175">從 [Microsoft 下載中心][DownloadCenterAddressRanges]可取得包含所有 Azure IP 位址範圍的 Xml 檔案。</span><span class="sxs-lookup"><span data-stu-id="632de-175">The Xml file containing all of the Azure IP address ranges is available from the [Microsoft Download Center][DownloadCenterAddressRanges].</span></span>  

<span data-ttu-id="632de-176">不過請注意，這些範圍會隨著時間改變，因此需要定期手動更新使用者定義路由，才能保持同步。</span><span class="sxs-lookup"><span data-stu-id="632de-176">Note though that these ranges change over time, thus necessitating periodic manual updates to the user defined routes to keep in sync.</span></span>  <span data-ttu-id="632de-177">此外，因為單一 UDR 有 100 個路由的預設上限，所以您需要「總結」Azure IP 位址範圍以符合 100 個路由的限制，請記住，UDR 定義的路由必須比 ExpressRoute 所通告的路由更明確。</span><span class="sxs-lookup"><span data-stu-id="632de-177">Also, since there is a default upper limit of 100 routes in a single UDR, you will need to "summarize" the Azure IP address ranges to fit within the 100 route limit, keeping in mind that UDR defined routes need to be more specific than the routes advertised by your ExpressRoute.</span></span>  

<span data-ttu-id="632de-178">**步驟 3：將路由表與包含 App Service 環境的子網路產生關聯**</span><span class="sxs-lookup"><span data-stu-id="632de-178">**Step 3:  Associate the route table to the subnet containing the App Service Environment**</span></span>

<span data-ttu-id="632de-179">最後一個設定步驟是將路由表與將要部署 App Service 環境的子網路產生關聯。</span><span class="sxs-lookup"><span data-stu-id="632de-179">The last  configuration step is to associate the route table to the subnet where the App Service Environment will be deployed.</span></span>  <span data-ttu-id="632de-180">下列命令會建立 "DirectInternetRouteTable" 與最後將包含 App Service 環境之 "ASESubnet" 的關聯。</span><span class="sxs-lookup"><span data-stu-id="632de-180">The following command associates the "DirectInternetRouteTable" to the "ASESubnet" that will eventually contain an App Service Environment.</span></span>

    Set-AzureSubnetRouteTable -VirtualNetworkName 'YourVirtualNetworkNameHere' -SubnetName 'ASESubnet' -RouteTableName 'DirectInternetRouteTable'


<span data-ttu-id="632de-181">**步驟 4：最後步驟**</span><span class="sxs-lookup"><span data-stu-id="632de-181">**Step 4:  Final Steps**</span></span>

<span data-ttu-id="632de-182">路由表繫結至子網路之後，建議您先測試並確認預期的效果。</span><span class="sxs-lookup"><span data-stu-id="632de-182">Once the route table is bound to the subnet, it is recommended to first test and confirm the intended effect.</span></span>  <span data-ttu-id="632de-183">例如，將虛擬機器部署至子網路，並確認：</span><span class="sxs-lookup"><span data-stu-id="632de-183">For example, deploy a virtual machine into the subnet and confirm that:</span></span>

* <span data-ttu-id="632de-184">本文前面提到的 Azure 和非 Azure 端點的輸出流量 **不會** 流到 ExpressRoute 循環。</span><span class="sxs-lookup"><span data-stu-id="632de-184">Outbound traffic to both Azure and non-Azure endpoints mentioned earlier in this article is **not** flowing down the ExpressRoute circuit.</span></span>  <span data-ttu-id="632de-185">請務必確認此行為，因為如果來自子網路的輸出流量仍是使用強制通道傳送至內部部署，App Service 環境建立一律會失敗。</span><span class="sxs-lookup"><span data-stu-id="632de-185">It is very important to verify this behavior, since if outbound traffic from the subnet is still being forced tunneled on-premises, App Service Environment creation will always fail.</span></span> 
* <span data-ttu-id="632de-186">已正確解析前面所提端點的所有 DNS 查閱。</span><span class="sxs-lookup"><span data-stu-id="632de-186">DNS lookups for the endpoints mentioned earlier are all resolving properly.</span></span> 

<span data-ttu-id="632de-187">一旦確認上述步驟後，您必須刪除虛擬機器，因為在建立 App Service 環境時，子網路必須是「空的」。</span><span class="sxs-lookup"><span data-stu-id="632de-187">Once the above steps are confirmed, you will need to delete the virtual machine because the subnet needs to be "empty" at the time the App Service Environment is created.</span></span>

<span data-ttu-id="632de-188">然後繼續建立 App Service 環境！</span><span class="sxs-lookup"><span data-stu-id="632de-188">Then proceed with creating an App Service Environment!</span></span>

## <a name="getting-started"></a><span data-ttu-id="632de-189">開始使用</span><span class="sxs-lookup"><span data-stu-id="632de-189">Getting started</span></span>
<span data-ttu-id="632de-190">您可以在 [應用程式服務環境的讀我檔案](../app-service/app-service-app-service-environments-readme.md)中取得 App Service 環境的所有相關文章與做法。</span><span class="sxs-lookup"><span data-stu-id="632de-190">All articles and How-To's for App Service Environments are available in the [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="632de-191">若要開始使用 App Service Environment，請參閱 [App Service Environment 簡介][IntroToAppServiceEnvironment]</span><span class="sxs-lookup"><span data-stu-id="632de-191">To get started with App Service Environments, see [Introduction to App Service Environment][IntroToAppServiceEnvironment]</span></span>

<span data-ttu-id="632de-192">如需有關 Azure App Service 平台的詳細資訊，請參閱 [Azure App Service][AzureAppService]。</span><span class="sxs-lookup"><span data-stu-id="632de-192">For more information about the Azure App Service platform, see [Azure App Service][AzureAppService].</span></span>

<!-- LINKS -->
[virtualnetwork]: http://azure.microsoft.com/services/virtual-network/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
[requiredports]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/
[NetworkSecurityGroups]: http://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[UDROverview]: http://azure.microsoft.com/documentation/articles/virtual-networks-udr-overview/
[UDRHowTo]: http://azure.microsoft.com/documentation/articles/virtual-networks-udr-how-to/
[HowToCreateAnAppServiceEnvironment]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-an-app-service-environment/
[AzureDownloads]: http://azure.microsoft.com/en-us/downloads/ 
[DownloadCenterAddressRanges]: http://www.microsoft.com/download/details.aspx?id=41653  
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/
[IntroToAppServiceEnvironment]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[NewPortal]:  https://portal.azure.com


<!-- IMAGES -->
