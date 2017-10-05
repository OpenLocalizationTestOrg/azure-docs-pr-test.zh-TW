---
title: "跨單位連線的規劃和設計：Azure VPN 閘道| Microsoft Docs"
description: "深入了解跨單位、混合式和 VNet 對 VNet 連線的 VPN 閘道規劃與設計"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: d5aaab83-4e74-4484-8bf0-cc465811e757
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/27/2017
ms.author: cherylmc
ms.openlocfilehash: 0ebc3ef4a64432e993dd6ed69766bb64544fe433
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="planning-and-design-for-vpn-gateway"></a><span data-ttu-id="aa960-103">規劃與設計 VPN 閘道</span><span class="sxs-lookup"><span data-stu-id="aa960-103">Planning and design for VPN Gateway</span></span>

<span data-ttu-id="aa960-104">跨單位及 VNet 對 VNet 組態的規劃與設計有可能很簡單，也可能很複雜，需視您的網路需求而定。</span><span class="sxs-lookup"><span data-stu-id="aa960-104">Planning and designing your cross-premises and VNet-to-VNet configurations can be either simple, or complicated, depending on your networking needs.</span></span> <span data-ttu-id="aa960-105">本文將逐步引導您完成基本的規劃和設計考量。</span><span class="sxs-lookup"><span data-stu-id="aa960-105">This article walks you through basic planning and design considerations.</span></span>

## <span data-ttu-id="aa960-106"><a name="planning"></a>規劃</span><span class="sxs-lookup"><span data-stu-id="aa960-106"><a name="planning"></a>Planning</span></span>

### <span data-ttu-id="aa960-107"><a name="compare"></a>跨單位連線選項</span><span class="sxs-lookup"><span data-stu-id="aa960-107"><a name="compare"></a>Cross-premises connectivity options</span></span>

<span data-ttu-id="aa960-108">如果您想要將內部部署站台安全地連接到虛擬網路，可以使用下列三種不同方法：站對站、點對站及 ExpressRoute。</span><span class="sxs-lookup"><span data-stu-id="aa960-108">If you want to connect your on-premises sites securely to a virtual network, you have three different ways to do so: Site-to-Site, Point-to-Site, and ExpressRoute.</span></span> <span data-ttu-id="aa960-109">比較可使用的不同跨單位連線。</span><span class="sxs-lookup"><span data-stu-id="aa960-109">Compare the different cross-premises connections that are available.</span></span> <span data-ttu-id="aa960-110">您選擇的選項可能取決於各種不同的考量，例如：</span><span class="sxs-lookup"><span data-stu-id="aa960-110">The option you choose can depend on various considerations, such as:</span></span>

* <span data-ttu-id="aa960-111">您的方案需要哪種輸送量?</span><span class="sxs-lookup"><span data-stu-id="aa960-111">What kind of throughput does your solution require?</span></span>
* <span data-ttu-id="aa960-112">您想讓通訊透過經由安全 VPN 的公用網際網路或透過私人連線?</span><span class="sxs-lookup"><span data-stu-id="aa960-112">Do you want to communicate over the public Internet via secure VPN, or over a private connection?</span></span>
* <span data-ttu-id="aa960-113">您有可供使用的公用 IP 位址嗎?</span><span class="sxs-lookup"><span data-stu-id="aa960-113">Do you have a public IP address available to use?</span></span>
* <span data-ttu-id="aa960-114">您打算使用 VPN 裝置嗎?</span><span class="sxs-lookup"><span data-stu-id="aa960-114">Are you planning to use a VPN device?</span></span> <span data-ttu-id="aa960-115">如果是，它相容嗎？</span><span class="sxs-lookup"><span data-stu-id="aa960-115">If so, is it compatible?</span></span>
* <span data-ttu-id="aa960-116">您只連線幾台電腦或您想要網站持續連線?</span><span class="sxs-lookup"><span data-stu-id="aa960-116">Are you connecting just a few computers, or do you want a persistent connection for your site?</span></span>
* <span data-ttu-id="aa960-117">您想要建立的方案需要什麼類型的 VPN 閘道?</span><span class="sxs-lookup"><span data-stu-id="aa960-117">What type of VPN gateway is required for the solution you want to create?</span></span>
* <span data-ttu-id="aa960-118">您應該使用哪一種閘道 SKU？</span><span class="sxs-lookup"><span data-stu-id="aa960-118">Which gateway SKU should you use?</span></span>

### <span data-ttu-id="aa960-119"><a name="planningtable"></a>規劃表</span><span class="sxs-lookup"><span data-stu-id="aa960-119"><a name="planningtable"></a>Planning table</span></span>

<span data-ttu-id="aa960-120">下表可以協助您為您的解決方案決定最佳的連線選項。</span><span class="sxs-lookup"><span data-stu-id="aa960-120">The following table can help you decide the best connectivity option for your solution.</span></span>

[!INCLUDE [vpn-gateway-cross-premises](../../includes/vpn-gateway-cross-premises-include.md)]

### <span data-ttu-id="aa960-121"><a name="gwsku"></a>閘道 SKU</span><span class="sxs-lookup"><span data-stu-id="aa960-121"><a name="gwsku"></a>Gateway SKUs</span></span>

[!INCLUDE [vpn-gateway-table-gwtype-aggtput](../../includes/vpn-gateway-table-gwtype-aggtput-include.md)]

### <span data-ttu-id="aa960-122"><a name="wf"></a>工作流程</span><span class="sxs-lookup"><span data-stu-id="aa960-122"><a name="wf"></a>Workflow</span></span>

<span data-ttu-id="aa960-123">下列清單列出常見的雲端連線工作流程：</span><span class="sxs-lookup"><span data-stu-id="aa960-123">The following list outlines the common workflow for cloud connectivity:</span></span>

1. <span data-ttu-id="aa960-124">設計和規劃連線的拓撲，列出所有您想要連接的網路位址空間。</span><span class="sxs-lookup"><span data-stu-id="aa960-124">Design and plan your connectivity topology and list the address spaces for all networks you want to connect.</span></span>
2. <span data-ttu-id="aa960-125">建立 Azure 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="aa960-125">Create an Azure virtual network.</span></span> 
3. <span data-ttu-id="aa960-126">建立虛擬網路的 VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="aa960-126">Create a VPN gateway for the virtual network.</span></span>
4. <span data-ttu-id="aa960-127">建立及設定連接至內部網路或其他虛擬網路的連線 (視需要)。</span><span class="sxs-lookup"><span data-stu-id="aa960-127">Create and configure connections to on-premises networks or other virtual networks (as needed).</span></span>
5. <span data-ttu-id="aa960-128">建立並設定 Azure VPN 閘道的點對站連線 (視需要)。</span><span class="sxs-lookup"><span data-stu-id="aa960-128">Create and configure a Point-to-Site connection for your Azure VPN gateway (as needed).</span></span>

## <span data-ttu-id="aa960-129"><a name="design"></a>設計</span><span class="sxs-lookup"><span data-stu-id="aa960-129"><a name="design"></a>Design</span></span>
### <span data-ttu-id="aa960-130"><a name="topologies"></a>連線拓撲</span><span class="sxs-lookup"><span data-stu-id="aa960-130"><a name="topologies"></a>Connection topologies</span></span>

<span data-ttu-id="aa960-131">先來看看 [關於 VPN 閘道](vpn-gateway-about-vpngateways.md) 一文中的圖表。</span><span class="sxs-lookup"><span data-stu-id="aa960-131">Start by looking at the diagrams in the [About VPN Gateway](vpn-gateway-about-vpngateways.md) article.</span></span> <span data-ttu-id="aa960-132">本文包含基本圖表、每種拓撲的部署模型，以及您可以用來部署組態的可用部署工具。</span><span class="sxs-lookup"><span data-stu-id="aa960-132">The article contains basic diagrams, the deployment models for each topology, and the available deployment tools you can use to deploy your configuration.</span></span>

### <span data-ttu-id="aa960-133"><a name="designbasics"></a>設計基本概念</span><span class="sxs-lookup"><span data-stu-id="aa960-133"><a name="designbasics"></a>Design basics</span></span>

<span data-ttu-id="aa960-134">下列各節將討論 VPN 閘道的基本概念。</span><span class="sxs-lookup"><span data-stu-id="aa960-134">The following sections discuss the VPN gateway basics.</span></span> 

#### <span data-ttu-id="aa960-135"><a name="servicelimits"></a>網路服務限制</span><span class="sxs-lookup"><span data-stu-id="aa960-135"><a name="servicelimits"></a>Networking services limits</span></span>

<span data-ttu-id="aa960-136">捲動表格以檢視[網路服務限制](../azure-subscription-service-limits.md#networking-limits)。</span><span class="sxs-lookup"><span data-stu-id="aa960-136">Scroll through the tables to view [networking services limits](../azure-subscription-service-limits.md#networking-limits).</span></span> <span data-ttu-id="aa960-137">上述限制可能會影響您的設計。</span><span class="sxs-lookup"><span data-stu-id="aa960-137">The limits listed may impact your design.</span></span>

#### <span data-ttu-id="aa960-138"><a name="subnets"></a>關於子網路</span><span class="sxs-lookup"><span data-stu-id="aa960-138"><a name="subnets"></a>About subnets</span></span>

<span data-ttu-id="aa960-139">當您建立連線時，必須考量您的子網路範圍。</span><span class="sxs-lookup"><span data-stu-id="aa960-139">When you are creating connections, you must consider your subnet ranges.</span></span> <span data-ttu-id="aa960-140">子網路位址範圍不能重疊。</span><span class="sxs-lookup"><span data-stu-id="aa960-140">You cannot have overlapping subnet address ranges.</span></span> <span data-ttu-id="aa960-141">當一個虛擬網路或內部部署位置包含的位址空間與其他位置重複時，就會發生子網路重疊的情況。</span><span class="sxs-lookup"><span data-stu-id="aa960-141">An overlapping subnet is when one virtual network or on-premises location contains the same address space that the other location contains.</span></span> <span data-ttu-id="aa960-142">這表示您需要請本機內部部署網路的網路工程師為您切割出一個範圍，以供您用於 Azure IP 位址空間/子網路。</span><span class="sxs-lookup"><span data-stu-id="aa960-142">This means that you need your network engineers for your local on-premises networks to carve out a range for you to use for your Azure IP addressing space/subnets.</span></span> <span data-ttu-id="aa960-143">您需要本機內部部署網路並未使用的位址空間。</span><span class="sxs-lookup"><span data-stu-id="aa960-143">You need address space that is not being used on the local on-premises network.</span></span>

<span data-ttu-id="aa960-144">使用 VNet 對 VNet 連線時，也要注意避免重疊的子網路。</span><span class="sxs-lookup"><span data-stu-id="aa960-144">Avoiding overlapping subnets is also important when you are working with VNet-to-VNet connections.</span></span> <span data-ttu-id="aa960-145">如果您的子網路重疊且 IP 位址同時存在於傳送端和目的地 VNet，VNet 對 VNet 連線就會失敗。</span><span class="sxs-lookup"><span data-stu-id="aa960-145">If your subnets overlap and an IP address exists in both the sending and destination VNets, VNet-to-VNet connections fail.</span></span> <span data-ttu-id="aa960-146">Azure 無法將資料路由傳送到另一個 VNet，因為目的地位址是傳送端 VNet 的一部分。</span><span class="sxs-lookup"><span data-stu-id="aa960-146">Azure can't route the data to the other VNet because the destination address is part of the sending VNet.</span></span>

<span data-ttu-id="aa960-147">「VPN 閘道」需要名為閘道子網路的特定子網路。</span><span class="sxs-lookup"><span data-stu-id="aa960-147">VPN Gateways require a specific subnet called a gateway subnet.</span></span> <span data-ttu-id="aa960-148">所有閘道子網路都必須命名為 GatewaySubnet 才能正常運作。</span><span class="sxs-lookup"><span data-stu-id="aa960-148">All gateway subnets must be named GatewaySubnet to work properly.</span></span> <span data-ttu-id="aa960-149">因此，請不要將閘道子網路命名為不同的名稱，也不要將 VM 或任何其他項目部署至閘道子網路。</span><span class="sxs-lookup"><span data-stu-id="aa960-149">Be sure not to name your gateway subnet a different name, and don't deploy VMs or anything else to the gateway subnet.</span></span> <span data-ttu-id="aa960-150">請參閱 [閘道子網路](vpn-gateway-about-vpn-gateway-settings.md#gwsub)。</span><span class="sxs-lookup"><span data-stu-id="aa960-150">See [Gateway Subnets](vpn-gateway-about-vpn-gateway-settings.md#gwsub).</span></span>

#### <span data-ttu-id="aa960-151"><a name="local"></a>關於區域網路閘道</span><span class="sxs-lookup"><span data-stu-id="aa960-151"><a name="local"></a>About local network gateways</span></span>

<span data-ttu-id="aa960-152">區域網路閘道通常是指您的內部部署位置。</span><span class="sxs-lookup"><span data-stu-id="aa960-152">The local network gateway typically refers to your on-premises location.</span></span> <span data-ttu-id="aa960-153">在傳統部署模型中，區域網路閘道被稱為「區域網路站台」。</span><span class="sxs-lookup"><span data-stu-id="aa960-153">In the classic deployment model, the local network gateway is referred to as a Local Network Site.</span></span> <span data-ttu-id="aa960-154">當您設定區域網路閘道時，您會賦予它名稱、指定內部部署 VPN 裝置的公用 IP 位址，以及指定位於內部部署位置中的位址首碼。</span><span class="sxs-lookup"><span data-stu-id="aa960-154">When you configure a local network gateway, you give it a name, specify the public IP address of the on-premises VPN device, and specify the address prefixes that are in the on-premises location.</span></span> <span data-ttu-id="aa960-155">Azure 會查看網路流量的目的地位址首碼、查閱您為區域網路閘道指定的組態，然後根據這些來路由傳送封包。</span><span class="sxs-lookup"><span data-stu-id="aa960-155">Azure looks at the destination address prefixes for network traffic, consults the configuration that you have specified for the local network gateway, and routes packets accordingly.</span></span> <span data-ttu-id="aa960-156">您可以視需要修改位址首碼。</span><span class="sxs-lookup"><span data-stu-id="aa960-156">You can modify the address prefixes as needed.</span></span> <span data-ttu-id="aa960-157">如需詳細資訊，請參閱[區域網路閘道](vpn-gateway-about-vpn-gateway-settings.md#lng)。</span><span class="sxs-lookup"><span data-stu-id="aa960-157">For more information, see [Local network gateways](vpn-gateway-about-vpn-gateway-settings.md#lng).</span></span>

#### <span data-ttu-id="aa960-158"><a name="gwtype"></a>關於閘道類型</span><span class="sxs-lookup"><span data-stu-id="aa960-158"><a name="gwtype"></a>About gateway types</span></span>

<span data-ttu-id="aa960-159">為拓撲選取正確的閘道類型相當重要。</span><span class="sxs-lookup"><span data-stu-id="aa960-159">Selecting the correct gateway type for your topology is critical.</span></span> <span data-ttu-id="aa960-160">如果您選取錯誤的類型，您的閘道將無法正常運作。</span><span class="sxs-lookup"><span data-stu-id="aa960-160">If you select the wrong type, your gateway won't work properly.</span></span> <span data-ttu-id="aa960-161">閘道類型會指定閘道本身如何連接以及為何它是 Resource Manager 部署模型的必要組態設定。</span><span class="sxs-lookup"><span data-stu-id="aa960-161">The gateway type specifies how the gateway itself connects and is a required configuration setting for the Resource Manager deployment model.</span></span>

<span data-ttu-id="aa960-162">閘道類型如下：</span><span class="sxs-lookup"><span data-stu-id="aa960-162">The gateway types are:</span></span>

* <span data-ttu-id="aa960-163">Vpn</span><span class="sxs-lookup"><span data-stu-id="aa960-163">Vpn</span></span>
* <span data-ttu-id="aa960-164">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="aa960-164">ExpressRoute</span></span>

#### <span data-ttu-id="aa960-165"><a name="connectiontype"></a>關於連線類型</span><span class="sxs-lookup"><span data-stu-id="aa960-165"><a name="connectiontype"></a>About connection types</span></span>

<span data-ttu-id="aa960-166">每個組態皆需要特定的連線類型。</span><span class="sxs-lookup"><span data-stu-id="aa960-166">Each configuration requires a specific connection type.</span></span> <span data-ttu-id="aa960-167">連線類型如下：</span><span class="sxs-lookup"><span data-stu-id="aa960-167">The connection types are:</span></span>

* <span data-ttu-id="aa960-168">IPsec</span><span class="sxs-lookup"><span data-stu-id="aa960-168">IPsec</span></span>
* <span data-ttu-id="aa960-169">Vnet2Vnet</span><span class="sxs-lookup"><span data-stu-id="aa960-169">Vnet2Vnet</span></span>
* <span data-ttu-id="aa960-170">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="aa960-170">ExpressRoute</span></span>
* <span data-ttu-id="aa960-171">VPNClient</span><span class="sxs-lookup"><span data-stu-id="aa960-171">VPNClient</span></span>

#### <span data-ttu-id="aa960-172"><a name="vpntype"></a>關於 VPN 類型</span><span class="sxs-lookup"><span data-stu-id="aa960-172"><a name="vpntype"></a>About VPN types</span></span>

<span data-ttu-id="aa960-173">每個組態都需要特定 VPN 類型。</span><span class="sxs-lookup"><span data-stu-id="aa960-173">Each configuration requires a specific VPN type.</span></span> <span data-ttu-id="aa960-174">如果您要結合兩個組態，例如建立連往相同 VNet 的站對站連線和點對站連線，您必須使用同時符合這兩個連線需求的 VPN 類型。</span><span class="sxs-lookup"><span data-stu-id="aa960-174">If you are combining two configurations, such as creating a Site-to-Site connection and a Point-to-Site connection to the same VNet, you must use a VPN type that satisfies both connection requirements.</span></span>

[!INCLUDE [vpn-gateway-vpntype](../../includes/vpn-gateway-vpntype-include.md)]

<span data-ttu-id="aa960-175">下表顯示 VPN 類型所對應的每一種連線組態。</span><span class="sxs-lookup"><span data-stu-id="aa960-175">The following tables show the VPN type as it maps to each connection configuration.</span></span> <span data-ttu-id="aa960-176">請確定閘道的 VPN 類型符合您想要建立的組態。</span><span class="sxs-lookup"><span data-stu-id="aa960-176">Make sure the VPN type for your gateway matches the configuration that you want to create.</span></span> 

[!INCLUDE [vpn-gateway-table-vpntype](../../includes/vpn-gateway-table-vpntype-include.md)]

### <span data-ttu-id="aa960-177"><a name="devices"></a>站對站連線的 VPN 裝置</span><span class="sxs-lookup"><span data-stu-id="aa960-177"><a name="devices"></a>VPN devices for Site-to-Site connections</span></span>

<span data-ttu-id="aa960-178">不論部署模型為何，若要設定站對站連線，您都需要下列項目︰</span><span class="sxs-lookup"><span data-stu-id="aa960-178">To configure a Site-to-Site connection, regardless of deployment model, you need the following items:</span></span>

* <span data-ttu-id="aa960-179">與 Azure VPN 閘道相容的 VPN 裝置</span><span class="sxs-lookup"><span data-stu-id="aa960-179">A VPN device that is compatible with Azure VPN gateways</span></span>
* <span data-ttu-id="aa960-180">不在 NAT 後方的公開 IPv4 IP 位址</span><span class="sxs-lookup"><span data-stu-id="aa960-180">A public-facing IPv4 IP address that is not behind a NAT</span></span>

<span data-ttu-id="aa960-181">您必須具備設定 VPN 裝置的經驗，或是有人可以為您設定裝置。</span><span class="sxs-lookup"><span data-stu-id="aa960-181">You need to have experience configuring your VPN device, or have someone that can configure the device for you.</span></span>

[!INCLUDE [vpn-gateway-configure-vpn-device-rm](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]

### <span data-ttu-id="aa960-182"><a name="forcedtunnel"></a>考量強制通道路由</span><span class="sxs-lookup"><span data-stu-id="aa960-182"><a name="forcedtunnel"></a>Consider forced tunnel routing</span></span>

<span data-ttu-id="aa960-183">對於多數組態，您可以設定強制通道。</span><span class="sxs-lookup"><span data-stu-id="aa960-183">For most configurations, you can configure forced tunneling.</span></span> <span data-ttu-id="aa960-184">強制通道可讓您透過站對站 VPN 通道，重新導向或「強制」所有網際網路繫結流量傳回內部部署位置，以便進行檢查和稽核。</span><span class="sxs-lookup"><span data-stu-id="aa960-184">Forced tunneling lets you redirect or "force" all Internet-bound traffic back to your on-premises location via a Site-to-Site VPN tunnel for inspection and auditing.</span></span> <span data-ttu-id="aa960-185">這是多數企業 IT 原則的重要安全性需求。</span><span class="sxs-lookup"><span data-stu-id="aa960-185">This is a critical security requirement for most enterprise IT policies.</span></span> 

<span data-ttu-id="aa960-186">若不使用強制通道，則 Azure 中來自 VM 的網際網路繫結流量會永遠從 Azure 網路基礎結構直接向外周遊到網際網路，而您無法選擇檢查或稽核流量。</span><span class="sxs-lookup"><span data-stu-id="aa960-186">Without forced tunneling, Internet-bound traffic from your VMs in Azure will always traverse from Azure network infrastructure directly out to the Internet, without the option to allow you to inspect or audit the traffic.</span></span> <span data-ttu-id="aa960-187">未經授權的網際網路存取可能會導致資訊洩漏或其他類型的安全性漏洞。</span><span class="sxs-lookup"><span data-stu-id="aa960-187">Unauthorized Internet access can potentially lead to information disclosure or other types of security breaches.</span></span>

<span data-ttu-id="aa960-188">可以在這兩種部署模型中使用不同的工具，設定強制通道的連線。</span><span class="sxs-lookup"><span data-stu-id="aa960-188">A forced tunneling connection can be configured in both deployment models and by using different tools.</span></span> <span data-ttu-id="aa960-189">如需詳細資訊，請參閱[設定強制通道](vpn-gateway-forced-tunneling-rm.md)。</span><span class="sxs-lookup"><span data-stu-id="aa960-189">For more information, see [Configure forced tunneling](vpn-gateway-forced-tunneling-rm.md).</span></span>

<span data-ttu-id="aa960-190">**強制通道圖表**</span><span class="sxs-lookup"><span data-stu-id="aa960-190">**Forced tunneling diagram**</span></span>

![Azure VPN 閘道強制通道圖表](./media/vpn-gateway-plan-design/forced-tunneling-diagram.png)

## <a name="next-steps"></a><span data-ttu-id="aa960-192">後續步驟</span><span class="sxs-lookup"><span data-stu-id="aa960-192">Next steps</span></span>

<span data-ttu-id="aa960-193">如需可協助您進行設計的詳細資訊，請參閱 [VPN 閘道常見問題集](vpn-gateway-vpn-faq.md)一文和[關於 VPN 閘道](vpn-gateway-about-vpngateways.md)一文。</span><span class="sxs-lookup"><span data-stu-id="aa960-193">See the [VPN Gateway FAQ](vpn-gateway-vpn-faq.md) and [About VPN Gateway](vpn-gateway-about-vpngateways.md) articles for more information to help you with your design.</span></span>

<span data-ttu-id="aa960-194">如需有關特定閘道設定的詳細資訊，請參閱 [關於 VPN 閘道設定](vpn-gateway-about-vpn-gateway-settings.md)。</span><span class="sxs-lookup"><span data-stu-id="aa960-194">For more information about specific gateway settings, see [About VPN Gateway Settings](vpn-gateway-about-vpn-gateway-settings.md).</span></span>