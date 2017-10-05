---
title: "適用於 Azure ExpressRoute 的 NAT | Microsoft Docs"
description: "此頁面提供用來設定和管理 ExpressRoute 循環路由的詳細需求。"
documentationcenter: na
services: expressroute
author: osamazia
manager: ganesr
editor: 
ms.assetid: eaaf0393-d384-4496-9a5c-328e94c262a7
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: osamam
ms.openlocfilehash: 5c039a80b24feda61da0793fa64b48cb4783c3f1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="nat-for-expressroute"></a><span data-ttu-id="4e6a9-103">適用於 ExpressRoute 的 NAT</span><span class="sxs-lookup"><span data-stu-id="4e6a9-103">NAT for ExpressRoute</span></span>

<span data-ttu-id="4e6a9-104">若要使用 ExpressRoute 連線到 Microsoft 雲端服務，您必須設定和管理路由。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-104">To connect to Microsoft cloud services using ExpressRoute, you’ll need to set up and manage routing.</span></span> <span data-ttu-id="4e6a9-105">有些連線提供者會以受管理的服務形式提供路由的設定和管理。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-105">Some connectivity providers offer setting up and managing routing as a managed service.</span></span> <span data-ttu-id="4e6a9-106">請洽詢您的連線服務提供者，以查看他們是否提供這類服務。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-106">Check with your connectivity provider to see if they offer this service.</span></span> <span data-ttu-id="4e6a9-107">如果沒有，您必須遵循下列需求。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-107">If they don't, you must adhere to the following requirements.</span></span> 

<span data-ttu-id="4e6a9-108">如需必須設定才能進行連線的路由工作階段的說明，請參閱[線路和路由網域](expressroute-circuit-peerings.md)一文。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-108">Refer to the [Circuits and routing domains](expressroute-circuit-peerings.md) article for a description of the routing sessions that need to be set up in to facilitate connectivity.</span></span>

> [!NOTE]
> <span data-ttu-id="4e6a9-109">Microsoft 不支援任何高可用性組態的路由器備援通訊協定 (如 HSRP、VRRP)。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-109">Microsoft does not support any router redundancy protocols (e.g., HSRP, VRRP) for high availability configurations.</span></span> <span data-ttu-id="4e6a9-110">我們依賴每個對等互連的一組備援 BGP 工作階段來取得高可用性。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-110">We rely on a redundant pair of BGP sessions per peering for high availability.</span></span>
> 
> 

## <a name="ip-addresses-used-for-peerings"></a><span data-ttu-id="4e6a9-111">用於對等互連的 IP 位址</span><span class="sxs-lookup"><span data-stu-id="4e6a9-111">IP addresses used for peerings</span></span>

<span data-ttu-id="4e6a9-112">您必須保留一些 IP 位址來設定您的網路與 Microsoft 的 Enterprise Edge (MSEEs) 路由器之間的路由。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-112">You need to reserve a few blocks of IP addresses to configure routing between your network and Microsoft's Enterprise edge (MSEEs) routers.</span></span> <span data-ttu-id="4e6a9-113">本節提供需求清單並描述必須如何取得和使用這些 IP 位址的相關規則。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-113">This section provides a list of requirements and describes the rules regarding how these IP addresses must be acquired and used.</span></span>

### <a name="ip-addresses-used-for-azure-private-peering"></a><span data-ttu-id="4e6a9-114">用於 Azure 私人對等互連的 IP 位址</span><span class="sxs-lookup"><span data-stu-id="4e6a9-114">IP addresses used for Azure private peering</span></span>

<span data-ttu-id="4e6a9-115">您可以使用私人 IP 位址或公用 IP 位址來設定對等互連。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-115">You can use either private IP addresses or public IP addresses to configure the peerings.</span></span> <span data-ttu-id="4e6a9-116">用來設定路由的位址範圍不得與用來在 Azure 中建立虛擬網路的位址範圍重疊。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-116">The address range used for configuring routes must not overlap with address ranges used to create virtual networks in Azure.</span></span> 

* <span data-ttu-id="4e6a9-117">您必須為路由介面保留一個 /29 子網路或兩個 /30 子網路。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-117">You must reserve a /29 subnet or two /30 subnets for routing interfaces.</span></span>
* <span data-ttu-id="4e6a9-118">用於路由的子網路可以是私人 IP 位址或公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-118">The subnets used for routing can be either private IP addresses or public IP addresses.</span></span>
* <span data-ttu-id="4e6a9-119">子網路不得與客戶保留以便用於 Microsoft Cloud 的範圍衝突。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-119">The subnets must not conflict with the range reserved by the customer for use in the Microsoft cloud.</span></span>
* <span data-ttu-id="4e6a9-120">如果使用 /29 子網路，它就會分割成兩個 /30 子網路。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-120">If a /29 subnet is used, it will be split into two /30 subnets.</span></span> 
  * <span data-ttu-id="4e6a9-121">第一個 /30 子網路將用於主要連結，而第二個 /30 子網路將用於次要連結。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-121">The first /30 subnet will be used for the primary link and the second /30 subnet will be used for the secondary link.</span></span>
  * <span data-ttu-id="4e6a9-122">針對每個 /30 子網路，您必須在您的路由器上使用 /30 子網路的第一個 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-122">For each of the /30 subnets, you must use the first IP address of the /30 subnet on your router.</span></span> <span data-ttu-id="4e6a9-123">Microsoft 會使用 /30 子網路的第二個 IP 位址來設定 BGP 工作階段。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-123">Microsoft will use the second IP address of the /30 subnet to set up a BGP session.</span></span>
  * <span data-ttu-id="4e6a9-124">您必須設定兩個 BGP 工作階段，我們的 [可用性 SLA](https://azure.microsoft.com/support/legal/sla/) 才會有效。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-124">You must set up both BGP sessions for our [availability SLA](https://azure.microsoft.com/support/legal/sla/) to be valid.</span></span>  

#### <a name="example-for-private-peering"></a><span data-ttu-id="4e6a9-125">私人對等互連範例</span><span class="sxs-lookup"><span data-stu-id="4e6a9-125">Example for private peering</span></span>

<span data-ttu-id="4e6a9-126">如果您選擇使用 a.b.c.d/29 來設定對等互連，它會分割成兩個 /30 子網路。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-126">If you choose to use a.b.c.d/29 to set up the peering, it will be split into two /30 subnets.</span></span> <span data-ttu-id="4e6a9-127">在下列範例中，我們會探討如何使用 a.b.c.d/29 子網路。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-127">In the example below, we will look at how the a.b.c.d/29 subnet is used.</span></span> 

<span data-ttu-id="4e6a9-128">a.b.c.d/29 會分割成 a.b.c.d/30 和 a.b.c.d+4/30 並透過佈建 API 向下傳遞至 Microsoft。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-128">a.b.c.d/29 will be split to a.b.c.d/30 and a.b.c.d+4/30 and passed down to Microsoft through the provisioning APIs.</span></span> <span data-ttu-id="4e6a9-129">您將使用 a.b.c.d+1 作為主要 PE 的 VRF IP，而 Microsoft 將使用 a.b.c.d+2 作為主要 MSEE 的 VRF IP。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-129">You will use a.b.c.d+1 as the VRF IP for the Primary PE and Microsoft will consume a.b.c.d+2 as the VRF IP for the primary MSEE.</span></span> <span data-ttu-id="4e6a9-130">您將使用 a.b.c.d+5 作為次要 PE 的 VRF IP，而 Microsoft 將使用 a.b.c.d+6 作為次要 MSEE 的 VRF IP。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-130">You will use a.b.c.d+5 as the VRF IP for the secondary PE and Microsoft will use a.b.c.d+6 as the VRF IP for the secondary MSEE.</span></span>

<span data-ttu-id="4e6a9-131">請考慮您選取 192.168.100.128/29 來設定私人互連的情況。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-131">Consider a case where you select 192.168.100.128/29 to set up private peering.</span></span> <span data-ttu-id="4e6a9-132">192.168.100.128/29 包含從 192.168.100.128 至 192.168.100.135 的位址，其中︰</span><span class="sxs-lookup"><span data-stu-id="4e6a9-132">192.168.100.128/29 includes addresses from 192.168.100.128 to 192.168.100.135, among which:</span></span>

* <span data-ttu-id="4e6a9-133">192.168.100.128/30 將會指派給 link1 (提供者使用 192.168.100.129，而 Microsoft 使用 192.168.100.130)。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-133">192.168.100.128/30 will be assigned to link1, with provider using 192.168.100.129 and Microsoft using 192.168.100.130.</span></span>
* <span data-ttu-id="4e6a9-134">192.168.100.132/30 將會指派給 link2 (提供者使用 192.168.100.133，而 Microsoft 使用 192.168.100.134)。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-134">192.168.100.132/30 will be assigned to link2, with provider using 192.168.100.133 and Microsoft using 192.168.100.134.</span></span>

### <a name="ip-addresses-used-for-azure-public-and-microsoft-peering"></a><span data-ttu-id="4e6a9-135">用於 Azure 公用與 Microsoft 對等互連的 IP 位址</span><span class="sxs-lookup"><span data-stu-id="4e6a9-135">IP addresses used for Azure public and Microsoft peering</span></span>

<span data-ttu-id="4e6a9-136">您必須使用自己的公用 IP 位址來設定 BGP 工作階段。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-136">You must use public IP addresses that you own for setting up the BGP sessions.</span></span> <span data-ttu-id="4e6a9-137">Microsoft 必須能夠透過路由網際網路登錄和網際網路路由登錄來驗證 IP 位址的擁有權。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-137">Microsoft must be able to verify the ownership of the IP addresses through Routing Internet Registries and Internet Routing Registries.</span></span> 

* <span data-ttu-id="4e6a9-138">您必須使用唯一的 /29 子網路或兩個 /30 子網路來為每個 ExpressRoute 循環 (如果您有多個) 的每個對等互連設定 BGP 對等互連。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-138">You must use a unique /29 subnet or two /30 subnets to set up the BGP peering for each peering per ExpressRoute circuit (if you have more than one).</span></span> 
* <span data-ttu-id="4e6a9-139">如果使用 /29 子網路，它就會分割成兩個 /30 子網路。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-139">If a /29 subnet is used, it will be split into two /30 subnets.</span></span> 
  * <span data-ttu-id="4e6a9-140">第一個 /30 子網路將用於主要連結，而第二個 /30 子網路將用於次要連結。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-140">The first /30 subnet will be used for the primary link and the second /30 subnet will be used for the secondary link.</span></span>
  * <span data-ttu-id="4e6a9-141">針對每個 /30 子網路，您必須在您的路由器上使用 /30 子網路的第一個 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-141">For each of the /30 subnets, you must use the first IP address of the /30 subnet on your router.</span></span> <span data-ttu-id="4e6a9-142">Microsoft 會使用 /30 子網路的第二個 IP 位址來設定 BGP 工作階段。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-142">Microsoft will use the second IP address of the /30 subnet to set up a BGP session.</span></span>
  * <span data-ttu-id="4e6a9-143">您必須設定兩個 BGP 工作階段，我們的 [可用性 SLA](https://azure.microsoft.com/support/legal/sla/) 才會有效。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-143">You must set up both BGP sessions for our [availability SLA](https://azure.microsoft.com/support/legal/sla/) to be valid.</span></span>

## <a name="public-ip-address-requirement"></a><span data-ttu-id="4e6a9-144">公用 IP 位址需求</span><span class="sxs-lookup"><span data-stu-id="4e6a9-144">Public IP address requirement</span></span>

### <a name="private-peering"></a><span data-ttu-id="4e6a9-145">私人對等互連</span><span class="sxs-lookup"><span data-stu-id="4e6a9-145">Private Peering</span></span>

<span data-ttu-id="4e6a9-146">您可以選擇使用公用或私人 IPv4 位址進行私人對等互連。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-146">You can choose to use public or private IPv4 addresses for private peering.</span></span> <span data-ttu-id="4e6a9-147">我們會提供流量的端對端隔離，因此在私人對等互連的情況下不可能發生位址與其他客戶重疊。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-147">We provide end-to-end isolation of your traffic so overlapping of addresses with other customers is not possible in case of private peering.</span></span> <span data-ttu-id="4e6a9-148">這些位址不會向網際網路公告。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-148">These addresses are not advertised to Internet.</span></span> 

### <a name="public-peering"></a><span data-ttu-id="4e6a9-149">公用對等互連</span><span class="sxs-lookup"><span data-stu-id="4e6a9-149">Public Peering</span></span>

<span data-ttu-id="4e6a9-150">Azure 公用對等路徑可讓您連接到裝載於 Azure 中的所有服務的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-150">The Azure public peering path enables you to connect to all services hosted in Azure over their public IP addresses.</span></span> <span data-ttu-id="4e6a9-151">其中包括 [ExpessRoute 常見問題集](expressroute-faqs.md) 列出的服務，以及由 ISV 裝載於 Microsoft Azure 上的任何服務。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-151">These include services listed in the [ExpessRoute FAQ](expressroute-faqs.md) and any services hosted by ISVs on Microsoft Azure.</span></span> <span data-ttu-id="4e6a9-152">連線到公用對等的 Microsoft Azure 服務時，一律是從您的網路出發到 Microsoft 網路。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-152">Connectivity to Microsoft Azure services on public peering is always initiated from your network into the Microsoft network.</span></span> <span data-ttu-id="4e6a9-153">您必須將公用 IP 位址使用於目的地為 Microsoft 網路的流量。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-153">You must use Public IP addresses for the traffic destined to Microsoft network.</span></span>

### <a name="microsoft-peering"></a><span data-ttu-id="4e6a9-154">Microsoft 對等互連</span><span class="sxs-lookup"><span data-stu-id="4e6a9-154">Microsoft Peering</span></span>

<span data-ttu-id="4e6a9-155">Microsoft 對等路徑可讓您連接到不支援透過 Azure 公用對等路徑存取的 Microsoft 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-155">The Microsoft peering path lets you connect to Microsoft cloud services that are not supported through the Azure public peering path.</span></span> <span data-ttu-id="4e6a9-156">服務清單包括 Office 365 服務，例如 Exchange Online、SharePoint Online、商務用 Skype 和 Dynamics 365。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-156">The list of services includes Office 365 services, such as Exchange Online, SharePoint Online, Skype for Business, and Dynamics 365.</span></span> <span data-ttu-id="4e6a9-157">Microsoft 支援在 Microsoft 對等上的雙向連線能力。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-157">Microsoft supports bi-directional connectivity on the Microsoft peering.</span></span> <span data-ttu-id="4e6a9-158">以 Microsoft 雲端服務為目的地的流量，必須使用有效的公用 IPv4 位址，才能進入 Microsoft 網路。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-158">Traffic destined to Microsoft cloud services must use valid public IPv4 addresses before they enter the Microsoft network.</span></span>

<span data-ttu-id="4e6a9-159">確定您的 IP 位址和 AS 號碼已在下列其中一個登錄中註冊。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-159">Make sure that your IP address and AS number are registered to you in one of the registries listed below.</span></span>

* [<span data-ttu-id="4e6a9-160">ARIN</span><span class="sxs-lookup"><span data-stu-id="4e6a9-160">ARIN</span></span>](https://www.arin.net/)
* [<span data-ttu-id="4e6a9-161">APNIC</span><span class="sxs-lookup"><span data-stu-id="4e6a9-161">APNIC</span></span>](https://www.apnic.net/)
* [<span data-ttu-id="4e6a9-162">AFRINIC</span><span class="sxs-lookup"><span data-stu-id="4e6a9-162">AFRINIC</span></span>](https://www.afrinic.net/)
* [<span data-ttu-id="4e6a9-163">LACNIC</span><span class="sxs-lookup"><span data-stu-id="4e6a9-163">LACNIC</span></span>](http://www.lacnic.net/)
* [<span data-ttu-id="4e6a9-164">RIPENCC</span><span class="sxs-lookup"><span data-stu-id="4e6a9-164">RIPENCC</span></span>](https://www.ripe.net/)
* [<span data-ttu-id="4e6a9-165">RADB</span><span class="sxs-lookup"><span data-stu-id="4e6a9-165">RADB</span></span>](http://www.radb.net/)
* [<span data-ttu-id="4e6a9-166">ALTDB</span><span class="sxs-lookup"><span data-stu-id="4e6a9-166">ALTDB</span></span>](http://altdb.net/)

> [!IMPORTANT]
> <span data-ttu-id="4e6a9-167">透過 ExpressRoute 向 Microsoft 公告的公用 IP 位址不得向網際網路公告。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-167">Public IP addresses advertised to Microsoft over ExpressRoute must not be advertised to the Internet.</span></span> <span data-ttu-id="4e6a9-168">這可能會中斷其他 Microsoft 服務的連線。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-168">This may break connectivity to other Microsoft services.</span></span> <span data-ttu-id="4e6a9-169">不過，您的網路中伺服器用來與 Microsoft 內部 O365 端點進行通訊的公用 IP 位址可透過 ExpressRoute 公告。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-169">However, Public IP addresses used by servers in your network that communicate with O365 endpoints within Microsoft may be advertised over ExpressRoute.</span></span> 
> 
> 

## <a name="dynamic-route-exchange"></a><span data-ttu-id="4e6a9-170">動態路由交換</span><span class="sxs-lookup"><span data-stu-id="4e6a9-170">Dynamic route exchange</span></span>

<span data-ttu-id="4e6a9-171">路由交換將會透過 eBGP 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-171">Routing exchange will be over eBGP protocol.</span></span> <span data-ttu-id="4e6a9-172">MSEEs 與您的路由器之間會建立 EBGP 工作階段。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-172">EBGP sessions are established between the MSEEs and your routers.</span></span> <span data-ttu-id="4e6a9-173">不一定需要驗證 BGP 工作階段。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-173">Authentication of BGP sessions is not a requirement.</span></span> <span data-ttu-id="4e6a9-174">如有必要，也可以設定 MD5 雜湊。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-174">If required, an MD5 hash can be configured.</span></span> <span data-ttu-id="4e6a9-175">如需設定 BGP 工作階段的資訊，請參閱[設定路由](expressroute-howto-routing-classic.md)和[線路佈建工作流程和線路狀態](expressroute-workflows.md)。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-175">See the [Configure routing](expressroute-howto-routing-classic.md) and [Circuit provisioning workflows and circuit states](expressroute-workflows.md) for information about configuring BGP sessions.</span></span>

## <a name="autonomous-system-numbers"></a><span data-ttu-id="4e6a9-176">自發系統號碼</span><span class="sxs-lookup"><span data-stu-id="4e6a9-176">Autonomous System numbers</span></span>

<span data-ttu-id="4e6a9-177">Microsoft 將使用 AS 12076 進行 Azure 公用、Azure 私人和 Microsoft 對等互連。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-177">Microsoft will use AS 12076 for Azure public, Azure private and Microsoft peering.</span></span> <span data-ttu-id="4e6a9-178">我們已保留 65515 至 65520 的 ASN，以供內部使用。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-178">We have reserved ASNs from 65515 to 65520 for internal use.</span></span> <span data-ttu-id="4e6a9-179">同時支援 16 和 32 位元號碼。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-179">Both 16 and 32 bit AS numbers are supported.</span></span>

<span data-ttu-id="4e6a9-180">資料傳輸對稱沒有任何相關需求。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-180">There are no requirements around data transfer symmetry.</span></span> <span data-ttu-id="4e6a9-181">轉送與返回路徑可能會周遊不同的路由器配對。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-181">The forward and return paths may traverse different router pairs.</span></span> <span data-ttu-id="4e6a9-182">相同的路由必須從橫跨多個屬於您的循環配對的任一端公告。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-182">Identical routes must be advertised from either sides across multiple circuit pairs belonging you.</span></span> <span data-ttu-id="4e6a9-183">路由計量不需要完全相同。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-183">Route metrics are not required to be identical.</span></span>

## <a name="route-aggregation-and-prefix-limits"></a><span data-ttu-id="4e6a9-184">路由彙總與前置詞限制</span><span class="sxs-lookup"><span data-stu-id="4e6a9-184">Route aggregation and prefix limits</span></span>

<span data-ttu-id="4e6a9-185">我們支援透過 Azure 私人對等互連向我們公告最多 4000 個前置詞。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-185">We support up to 4000 prefixes advertised to us through the Azure private peering.</span></span> <span data-ttu-id="4e6a9-186">如果已啟用 ExpressRoute 進階附加元件，則可增加至 10,000 個前置詞。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-186">This can be increased up to 10,000 prefixes if the ExpressRoute premium add-on is enabled.</span></span> <span data-ttu-id="4e6a9-187">我們接受每個 BGP 工作階段最多 200 個前置詞進行 Azure 公用和 Microsoft 對等互連。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-187">We accept up to 200 prefixes per BGP session for Azure public and Microsoft peering.</span></span> 

<span data-ttu-id="4e6a9-188">如果前置詞數目超過此限制，則會捨棄 BGP 工作階段。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-188">The BGP session will be dropped if the number of prefixes exceeds the limit.</span></span> <span data-ttu-id="4e6a9-189">我們只會接受私人對等互連連結上的預設路由。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-189">We will accept default routes on the private peering link only.</span></span> <span data-ttu-id="4e6a9-190">提供者必須從 Azure 公用和 Microsoft 對等互連路徑中篩選出預設路由和私人 IP 位址 (RFC 1918)。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-190">Provider must filter out default route and private IP addresses (RFC 1918) from the Azure public and Microsoft peering paths.</span></span> 

## <a name="transit-routing-and-cross-region-routing"></a><span data-ttu-id="4e6a9-191">傳輸路由和跨區域路由</span><span class="sxs-lookup"><span data-stu-id="4e6a9-191">Transit routing and cross-region routing</span></span>

<span data-ttu-id="4e6a9-192">ExpressRoute 不能設定為傳輸路由器。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-192">ExpressRoute cannot be configured as transit routers.</span></span> <span data-ttu-id="4e6a9-193">您必須依賴連線提供者的傳輸路由服務。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-193">You will have to rely on your connectivity provider for transit routing services.</span></span>

## <a name="advertising-default-routes"></a><span data-ttu-id="4e6a9-194">公告預設路由</span><span class="sxs-lookup"><span data-stu-id="4e6a9-194">Advertising default routes</span></span>

<span data-ttu-id="4e6a9-195">只有 Azure 私人對等互連工作階段允許預設路由。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-195">Default routes are permitted only on Azure private peering sessions.</span></span> <span data-ttu-id="4e6a9-196">在這種情況下，我們會將所有流量從相關聯的虛擬網路路由傳送到您的網路。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-196">In such a case, we will route all traffic from the associated virtual networks to your network.</span></span> <span data-ttu-id="4e6a9-197">在私人對等互連中公告預設路由，將會導致來自 Azure 的網際網路路徑遭到封鎖。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-197">Advertising default routes into private peering will result in the internet path from Azure being blocked.</span></span> <span data-ttu-id="4e6a9-198">您必須依賴您的公司網路邊緣，為 Azure 中裝載的服務往返路由傳送網際網路的流量。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-198">You must rely on your corporate edge to route traffic from and to the internet for services hosted in Azure.</span></span> 

 <span data-ttu-id="4e6a9-199">若要能夠連接其他 Azure 服務和基礎結構服務，您必須確定已備妥下列其中一個項目︰</span><span class="sxs-lookup"><span data-stu-id="4e6a9-199">To enable connectivity to other Azure services and infrastructure services, you must make sure one of the following items is in place:</span></span>

* <span data-ttu-id="4e6a9-200">啟用 Azure 公用對等互連以將流量路由傳送至公用端點</span><span class="sxs-lookup"><span data-stu-id="4e6a9-200">Azure public peering is enabled to route traffic to public endpoints</span></span>
* <span data-ttu-id="4e6a9-201">您可使用使用者定義的路由，讓需要網際網路連線的每個子網路進行網際網路連線。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-201">You use user-defined routing to allow internet connectivity for every subnet requiring Internet connectivity.</span></span>

> [!NOTE]
> <span data-ttu-id="4e6a9-202">公告預設路由會中斷 Windows 和其他 VM 授權啟用。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-202">Advertising default routes will break Windows and other VM license activation.</span></span> <span data-ttu-id="4e6a9-203">請依照 [這裡](http://blogs.msdn.com/b/mast/archive/2015/05/20/use-azure-custom-routes-to-enable-kms-activation-with-forced-tunneling.aspx) 的指示來解決這個問題。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-203">Follow instructions [here](http://blogs.msdn.com/b/mast/archive/2015/05/20/use-azure-custom-routes-to-enable-kms-activation-with-forced-tunneling.aspx) to work around this.</span></span>
> 
> 

## <a name="support-for-bgp-communities-preview"></a><span data-ttu-id="4e6a9-204">BGP 社群支援 (預覽)</span><span class="sxs-lookup"><span data-stu-id="4e6a9-204">Support for BGP communities (Preview)</span></span>

<span data-ttu-id="4e6a9-205">本節提供 BGP 社群如何搭配 ExpressRoute 使用的概觀。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-205">This section provides an overview of how BGP communities will be used with ExpressRoute.</span></span> <span data-ttu-id="4e6a9-206">Microsoft 將會公告公用和 Microsoft 對等互連路徑中的路由並為路由標記適當的社群值。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-206">Microsoft will advertise routes in the public and Microsoft peering paths with routes tagged with appropriate community values.</span></span> <span data-ttu-id="4e6a9-207">這麼做的基本原理和社群值的詳細資料如下所述。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-207">The rationale for doing so and the details on community values are described below.</span></span> <span data-ttu-id="4e6a9-208">不過，Microsoft 不接受任何標記至向 Microsoft 公告之路由的社群值。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-208">Microsoft, however, will not honor any community values tagged to routes advertised to Microsoft.</span></span>

<span data-ttu-id="4e6a9-209">如果您要在地理政治區域內的任何一個對等互連位置透過 ExpressRoute 連接到 Microsoft，您必須能夠存取地理政治界限內所有區域中的所有 Microsoft 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-209">If you are connecting to Microsoft through ExpressRoute at any one peering location within a geopolitical region, you will have access to all Microsoft cloud services across all regions within the geopolitical boundary.</span></span> 

<span data-ttu-id="4e6a9-210">例如，如果您在阿姆斯特丹透過 ExpressRoute 連接到 Microsoft，您必須能夠存取在北歐和西歐裝載的所有 Microsoft 雲端服務。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-210">For example, if you connected to Microsoft in Amsterdam through ExpressRoute, you will have access to all Microsoft cloud services hosted in North Europe and West Europe.</span></span> 

<span data-ttu-id="4e6a9-211">如需地理政治地區、相關聯的 Azure 區域和對應的 ExpressRoute 對等互連位置的詳細清單，請參閱 [ExpressRoute 合作夥伴和對等互連位置](expressroute-locations.md) 網頁。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-211">Refer to the [ExpressRoute partners and peering locations](expressroute-locations.md) page for a detailed list of geopolitical regions, associated Azure regions, and corresponding ExpressRoute peering locations.</span></span>

<span data-ttu-id="4e6a9-212">您可以針對每個地理政治區域購買多個 ExpressRoute 循環。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-212">You can purchase more than one ExpressRoute circuit per geopolitical region.</span></span> <span data-ttu-id="4e6a9-213">如果擁有多個連線，您即可因為異地備援而有明顯的高可用性優勢。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-213">Having multiple connections offers you significant benefits on high availability due to geo-redundancy.</span></span> <span data-ttu-id="4e6a9-214">具有多個 ExpressRoute 循環的情況下，您會從 Microsoft 收到同一組有關公用對等互連和 Microsoft 對等互連路徑的前置詞。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-214">In cases where you have multiple ExpressRoute circuits, you will receive the same set of prefixes advertised from Microsoft on the public peering and Microsoft peering paths.</span></span> <span data-ttu-id="4e6a9-215">這表示您將會有多個路徑可從您的網路連到 Microsoft。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-215">This means you will have multiple paths from your network into Microsoft.</span></span> <span data-ttu-id="4e6a9-216">這可能會導致在您的網路中做出次佳的路由決策。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-216">This can potentially cause sub-optimal routing decisions to be made within your network.</span></span> <span data-ttu-id="4e6a9-217">因此，您可能會遇到次佳的不同服務連線體驗。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-217">As a result, you may experience sub-optimal connectivity experiences to different services.</span></span> 

<span data-ttu-id="4e6a9-218">Microsoft 會以適當的 BGP 社群值標記透過公用對等互連和 Microsoft 對等互連公告的前置詞，表示前置詞裝載於的區域。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-218">Microsoft will tag prefixes advertised through public peering and Microsoft peering with appropriate BGP community values indicating the region the prefixes are hosted in.</span></span> <span data-ttu-id="4e6a9-219">您可以依賴社群值來做出適當的路由決策，以提供 [最佳路由給客戶](expressroute-optimize-routing.md)。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-219">You can rely on the community values to make appropriate routing decisions to offer [optimal routing to customers](expressroute-optimize-routing.md).</span></span>

| <span data-ttu-id="4e6a9-220">**地緣政治區域**</span><span class="sxs-lookup"><span data-stu-id="4e6a9-220">**Geopolitical Region**</span></span> | <span data-ttu-id="4e6a9-221">**Microsoft Azure 區域**</span><span class="sxs-lookup"><span data-stu-id="4e6a9-221">**Microsoft Azure region**</span></span> | <span data-ttu-id="4e6a9-222">**BGP 社群值**</span><span class="sxs-lookup"><span data-stu-id="4e6a9-222">**BGP community value**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4e6a9-223">**北美洲**</span><span class="sxs-lookup"><span data-stu-id="4e6a9-223">**North America**</span></span> | | |
| <span data-ttu-id="4e6a9-224">美國東部</span><span class="sxs-lookup"><span data-stu-id="4e6a9-224">East US</span></span> |<span data-ttu-id="4e6a9-225">12076:51004</span><span class="sxs-lookup"><span data-stu-id="4e6a9-225">12076:51004</span></span> | |
| <span data-ttu-id="4e6a9-226">美國東部 2</span><span class="sxs-lookup"><span data-stu-id="4e6a9-226">East US 2</span></span> |<span data-ttu-id="4e6a9-227">12076:51005</span><span class="sxs-lookup"><span data-stu-id="4e6a9-227">12076:51005</span></span> | |
| <span data-ttu-id="4e6a9-228">美國西部</span><span class="sxs-lookup"><span data-stu-id="4e6a9-228">West US</span></span> |<span data-ttu-id="4e6a9-229">12076:51006</span><span class="sxs-lookup"><span data-stu-id="4e6a9-229">12076:51006</span></span> | |
| <span data-ttu-id="4e6a9-230">美國西部 2</span><span class="sxs-lookup"><span data-stu-id="4e6a9-230">West US 2</span></span> |<span data-ttu-id="4e6a9-231">12076:51026</span><span class="sxs-lookup"><span data-stu-id="4e6a9-231">12076:51026</span></span> | |
| <span data-ttu-id="4e6a9-232">美國中西部</span><span class="sxs-lookup"><span data-stu-id="4e6a9-232">West Central US</span></span> |<span data-ttu-id="4e6a9-233">12076:51027</span><span class="sxs-lookup"><span data-stu-id="4e6a9-233">12076:51027</span></span> | |
| <span data-ttu-id="4e6a9-234">美國中北部</span><span class="sxs-lookup"><span data-stu-id="4e6a9-234">North Central US</span></span> |<span data-ttu-id="4e6a9-235">12076:51007</span><span class="sxs-lookup"><span data-stu-id="4e6a9-235">12076:51007</span></span> | |
| <span data-ttu-id="4e6a9-236">美國中南部</span><span class="sxs-lookup"><span data-stu-id="4e6a9-236">South Central US</span></span> |<span data-ttu-id="4e6a9-237">12076:51008</span><span class="sxs-lookup"><span data-stu-id="4e6a9-237">12076:51008</span></span> | |
| <span data-ttu-id="4e6a9-238">美國中部</span><span class="sxs-lookup"><span data-stu-id="4e6a9-238">Central US</span></span> |<span data-ttu-id="4e6a9-239">12076:51009</span><span class="sxs-lookup"><span data-stu-id="4e6a9-239">12076:51009</span></span> | |
| <span data-ttu-id="4e6a9-240">加拿大中部</span><span class="sxs-lookup"><span data-stu-id="4e6a9-240">Canada Central</span></span> |<span data-ttu-id="4e6a9-241">12076:51020</span><span class="sxs-lookup"><span data-stu-id="4e6a9-241">12076:51020</span></span> | |
| <span data-ttu-id="4e6a9-242">加拿大東部</span><span class="sxs-lookup"><span data-stu-id="4e6a9-242">Canada East</span></span> |<span data-ttu-id="4e6a9-243">12076:51021</span><span class="sxs-lookup"><span data-stu-id="4e6a9-243">12076:51021</span></span> | |
| <span data-ttu-id="4e6a9-244">**南美洲**</span><span class="sxs-lookup"><span data-stu-id="4e6a9-244">**South America**</span></span> | | |
| <span data-ttu-id="4e6a9-245">巴西南部</span><span class="sxs-lookup"><span data-stu-id="4e6a9-245">Brazil South</span></span> |<span data-ttu-id="4e6a9-246">12076:51014</span><span class="sxs-lookup"><span data-stu-id="4e6a9-246">12076:51014</span></span> | |
| <span data-ttu-id="4e6a9-247">**歐洲**</span><span class="sxs-lookup"><span data-stu-id="4e6a9-247">**Europe**</span></span> | | |
| <span data-ttu-id="4e6a9-248">北歐</span><span class="sxs-lookup"><span data-stu-id="4e6a9-248">North Europe</span></span> |<span data-ttu-id="4e6a9-249">12076:51003</span><span class="sxs-lookup"><span data-stu-id="4e6a9-249">12076:51003</span></span> | |
| <span data-ttu-id="4e6a9-250">西歐</span><span class="sxs-lookup"><span data-stu-id="4e6a9-250">West Europe</span></span> |<span data-ttu-id="4e6a9-251">12076:51002</span><span class="sxs-lookup"><span data-stu-id="4e6a9-251">12076:51002</span></span> | |
| <span data-ttu-id="4e6a9-252">**亞太地區**</span><span class="sxs-lookup"><span data-stu-id="4e6a9-252">**Asia Pacific**</span></span> | | |
| <span data-ttu-id="4e6a9-253">東亞</span><span class="sxs-lookup"><span data-stu-id="4e6a9-253">East Asia</span></span> |<span data-ttu-id="4e6a9-254">12076:51010</span><span class="sxs-lookup"><span data-stu-id="4e6a9-254">12076:51010</span></span> | |
| <span data-ttu-id="4e6a9-255">東南亞</span><span class="sxs-lookup"><span data-stu-id="4e6a9-255">Southeast Asia</span></span> |<span data-ttu-id="4e6a9-256">12076:51011</span><span class="sxs-lookup"><span data-stu-id="4e6a9-256">12076:51011</span></span> | |
| <span data-ttu-id="4e6a9-257">**日本**</span><span class="sxs-lookup"><span data-stu-id="4e6a9-257">**Japan**</span></span> | | |
| <span data-ttu-id="4e6a9-258">日本東部</span><span class="sxs-lookup"><span data-stu-id="4e6a9-258">Japan East</span></span> |<span data-ttu-id="4e6a9-259">12076:51012</span><span class="sxs-lookup"><span data-stu-id="4e6a9-259">12076:51012</span></span> | |
| <span data-ttu-id="4e6a9-260">日本西部</span><span class="sxs-lookup"><span data-stu-id="4e6a9-260">Japan West</span></span> |<span data-ttu-id="4e6a9-261">12076:51013</span><span class="sxs-lookup"><span data-stu-id="4e6a9-261">12076:51013</span></span> | |
| <span data-ttu-id="4e6a9-262">**澳大利亞**</span><span class="sxs-lookup"><span data-stu-id="4e6a9-262">**Australia**</span></span> | | |
| <span data-ttu-id="4e6a9-263">澳洲東部</span><span class="sxs-lookup"><span data-stu-id="4e6a9-263">Australia East</span></span> |<span data-ttu-id="4e6a9-264">12076:51015</span><span class="sxs-lookup"><span data-stu-id="4e6a9-264">12076:51015</span></span> | |
| <span data-ttu-id="4e6a9-265">澳洲東南部</span><span class="sxs-lookup"><span data-stu-id="4e6a9-265">Australia Southeast</span></span> |<span data-ttu-id="4e6a9-266">12076:51016</span><span class="sxs-lookup"><span data-stu-id="4e6a9-266">12076:51016</span></span> | |
| <span data-ttu-id="4e6a9-267">**印度**</span><span class="sxs-lookup"><span data-stu-id="4e6a9-267">**India**</span></span> | | |
| <span data-ttu-id="4e6a9-268">印度南部</span><span class="sxs-lookup"><span data-stu-id="4e6a9-268">India South</span></span> |<span data-ttu-id="4e6a9-269">12076:51019</span><span class="sxs-lookup"><span data-stu-id="4e6a9-269">12076:51019</span></span> | |
| <span data-ttu-id="4e6a9-270">印度西部</span><span class="sxs-lookup"><span data-stu-id="4e6a9-270">India West</span></span> |<span data-ttu-id="4e6a9-271">12076:51018</span><span class="sxs-lookup"><span data-stu-id="4e6a9-271">12076:51018</span></span> | |
| <span data-ttu-id="4e6a9-272">印度中部</span><span class="sxs-lookup"><span data-stu-id="4e6a9-272">India Central</span></span> |<span data-ttu-id="4e6a9-273">12076:51017</span><span class="sxs-lookup"><span data-stu-id="4e6a9-273">12076:51017</span></span> | |

<span data-ttu-id="4e6a9-274">所有 Microsoft 公告的路由會都加上適當的社群值。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-274">All routes advertised from Microsoft will be tagged with the appropriate community value.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="4e6a9-275">全域前置詞會加上適當的社群值，而且只會在啟用 ExpressRoute 進階附加元件時公告。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-275">Global prefixes will be tagged with an appropriate community value and will be advertised only when ExpressRoute premium add-on is enabled.</span></span>
> 
> 

<span data-ttu-id="4e6a9-276">除了上述各項，Microsoft 也將根據其所屬的服務加上標記及前置詞。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-276">In addition to the above, Microsoft will also tag prefixes based on the service they belong to.</span></span> <span data-ttu-id="4e6a9-277">這只適用於 Microsoft 對等互連。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-277">This applies only to the Microsoft peering.</span></span> <span data-ttu-id="4e6a9-278">下表提供服務與 BGP 社群值的對應。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-278">The table below provides a mapping of service to BGP community value.</span></span>

| <span data-ttu-id="4e6a9-279">**服務**</span><span class="sxs-lookup"><span data-stu-id="4e6a9-279">**Service**</span></span> | <span data-ttu-id="4e6a9-280">**BGP 社群值**</span><span class="sxs-lookup"><span data-stu-id="4e6a9-280">**BGP community value**</span></span> |
| --- | --- |
| <span data-ttu-id="4e6a9-281">**Exchange**</span><span class="sxs-lookup"><span data-stu-id="4e6a9-281">**Exchange**</span></span> |<span data-ttu-id="4e6a9-282">12076:5010</span><span class="sxs-lookup"><span data-stu-id="4e6a9-282">12076:5010</span></span> |
| <span data-ttu-id="4e6a9-283">**SharePoint**</span><span class="sxs-lookup"><span data-stu-id="4e6a9-283">**SharePoint**</span></span> |<span data-ttu-id="4e6a9-284">12076:5020</span><span class="sxs-lookup"><span data-stu-id="4e6a9-284">12076:5020</span></span> |
| <span data-ttu-id="4e6a9-285">**商務用 Skype**</span><span class="sxs-lookup"><span data-stu-id="4e6a9-285">**Skype For Business**</span></span> |<span data-ttu-id="4e6a9-286">12076:5030</span><span class="sxs-lookup"><span data-stu-id="4e6a9-286">12076:5030</span></span> |
| <span data-ttu-id="4e6a9-287">**Dynamics 365**</span><span class="sxs-lookup"><span data-stu-id="4e6a9-287">**Dynamics 365**</span></span> |<span data-ttu-id="4e6a9-288">12076:5040</span><span class="sxs-lookup"><span data-stu-id="4e6a9-288">12076:5040</span></span> |
| <span data-ttu-id="4e6a9-289">**其他 Office 365 服務**</span><span class="sxs-lookup"><span data-stu-id="4e6a9-289">**Other Office 365 Services**</span></span> |<span data-ttu-id="4e6a9-290">12076:5100</span><span class="sxs-lookup"><span data-stu-id="4e6a9-290">12076:5100</span></span> |

> [!NOTE]
> <span data-ttu-id="4e6a9-291">Microsoft 不接受任何您在向 Microsoft 通告的路由上設定的 BGP 社群值。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-291">Microsoft does not honor any BGP community values that you set on the routes advertised to Microsoft.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="4e6a9-292">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4e6a9-292">Next steps</span></span>

* <span data-ttu-id="4e6a9-293">設定 ExpressRoute 連線。</span><span class="sxs-lookup"><span data-stu-id="4e6a9-293">Configure your ExpressRoute connection.</span></span>
  
  * <span data-ttu-id="4e6a9-294">[建立傳統部署模型的 ExpressRoute 線路](expressroute-howto-circuit-classic.md)或[使用 Azure Resource Manager 建立和修改 ExpressRoute 線路](expressroute-howto-circuit-arm.md)</span><span class="sxs-lookup"><span data-stu-id="4e6a9-294">[Create an ExpressRoute circuit for the classic deployment model](expressroute-howto-circuit-classic.md) or [Create and modify an ExpressRoute circuit using Azure Resource Manager](expressroute-howto-circuit-arm.md)</span></span>
  * <span data-ttu-id="4e6a9-295">[設定傳統部署模型的路由](expressroute-howto-routing-classic.md)或[設定 Resource Manager 部署模型的路由](expressroute-howto-routing-arm.md)</span><span class="sxs-lookup"><span data-stu-id="4e6a9-295">[Configure routing for the classic deployment model](expressroute-howto-routing-classic.md) or [Configure routing for the Resource Manager deployment model](expressroute-howto-routing-arm.md)</span></span>
  * <span data-ttu-id="4e6a9-296">[將傳統 VNet 連結至 ExpressRoute 線路](expressroute-howto-linkvnet-classic.md)或[將 Resource Manager VNet 連結至 ExpressRoute 線路](expressroute-howto-linkvnet-arm.md)</span><span class="sxs-lookup"><span data-stu-id="4e6a9-296">[Link a classic VNet to an ExpressRoute circuit](expressroute-howto-linkvnet-classic.md) or [Link a Resource Manager VNet to an ExpressRoute circuit](expressroute-howto-linkvnet-arm.md)</span></span>

