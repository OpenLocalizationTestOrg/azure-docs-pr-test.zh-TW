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
ms.openlocfilehash: 3d4587ba31d163384212eca88a7e2c0ba8f3b21f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="planning-and-design-for-vpn-gateway"></a><span data-ttu-id="4d44f-103">規劃與設計 VPN 閘道</span><span class="sxs-lookup"><span data-stu-id="4d44f-103">Planning and design for VPN Gateway</span></span>

<span data-ttu-id="4d44f-104">跨單位及 VNet 對 VNet 組態的規劃與設計有可能很簡單，也可能很複雜，需視您的網路需求而定。</span><span class="sxs-lookup"><span data-stu-id="4d44f-104">Planning and designing your cross-premises and VNet-to-VNet configurations can be either simple, or complicated, depending on your networking needs.</span></span> <span data-ttu-id="4d44f-105">本文將逐步引導您完成基本的規劃和設計考量。</span><span class="sxs-lookup"><span data-stu-id="4d44f-105">This article walks you through basic planning and design considerations.</span></span>

## <span data-ttu-id="4d44f-106"><a name="planning"></a>規劃</span><span class="sxs-lookup"><span data-stu-id="4d44f-106"><a name="planning"></a>Planning</span></span>

### <span data-ttu-id="4d44f-107"><a name="compare"></a>跨單位連線選項</span><span class="sxs-lookup"><span data-stu-id="4d44f-107"><a name="compare"></a>Cross-premises connectivity options</span></span>

<span data-ttu-id="4d44f-108">如果您想 tooconnect 內部網站安全地 tooa 虛擬網路，因此您有三個不同的方式 toodo： 站台間，點對站和 ExpressRoute。</span><span class="sxs-lookup"><span data-stu-id="4d44f-108">If you want tooconnect your on-premises sites securely tooa virtual network, you have three different ways toodo so: Site-to-Site, Point-to-Site, and ExpressRoute.</span></span> <span data-ttu-id="4d44f-109">比較 hello 不同的跨單位連線所提供。</span><span class="sxs-lookup"><span data-stu-id="4d44f-109">Compare hello different cross-premises connections that are available.</span></span> <span data-ttu-id="4d44f-110">hello 您選擇的選項可以根據各種因素而定，例如：</span><span class="sxs-lookup"><span data-stu-id="4d44f-110">hello option you choose can depend on various considerations, such as:</span></span>

* <span data-ttu-id="4d44f-111">您的方案需要哪種輸送量?</span><span class="sxs-lookup"><span data-stu-id="4d44f-111">What kind of throughput does your solution require?</span></span>
* <span data-ttu-id="4d44f-112">是否要 toocommunicate hello 透過公用網際網路，透過安全的 VPN 或私人連線嗎？</span><span class="sxs-lookup"><span data-stu-id="4d44f-112">Do you want toocommunicate over hello public Internet via secure VPN, or over a private connection?</span></span>
* <span data-ttu-id="4d44f-113">您有公用 IP 位址可用 toouse 嗎？</span><span class="sxs-lookup"><span data-stu-id="4d44f-113">Do you have a public IP address available toouse?</span></span>
* <span data-ttu-id="4d44f-114">您計劃 toouse VPN 裝置？</span><span class="sxs-lookup"><span data-stu-id="4d44f-114">Are you planning toouse a VPN device?</span></span> <span data-ttu-id="4d44f-115">如果是，它相容嗎？</span><span class="sxs-lookup"><span data-stu-id="4d44f-115">If so, is it compatible?</span></span>
* <span data-ttu-id="4d44f-116">您只連線幾台電腦或您想要網站持續連線?</span><span class="sxs-lookup"><span data-stu-id="4d44f-116">Are you connecting just a few computers, or do you want a persistent connection for your site?</span></span>
* <span data-ttu-id="4d44f-117">都需要哪些類型的 VPN 閘道想 toocreate hello 方案？</span><span class="sxs-lookup"><span data-stu-id="4d44f-117">What type of VPN gateway is required for hello solution you want toocreate?</span></span>
* <span data-ttu-id="4d44f-118">您應該使用哪一種閘道 SKU？</span><span class="sxs-lookup"><span data-stu-id="4d44f-118">Which gateway SKU should you use?</span></span>

### <span data-ttu-id="4d44f-119"><a name="planningtable"></a>規劃表</span><span class="sxs-lookup"><span data-stu-id="4d44f-119"><a name="planningtable"></a>Planning table</span></span>

<span data-ttu-id="4d44f-120">下表中的 hello 可協助您決定為您的方案 hello 最佳連線選項。</span><span class="sxs-lookup"><span data-stu-id="4d44f-120">hello following table can help you decide hello best connectivity option for your solution.</span></span>

[!INCLUDE [vpn-gateway-cross-premises](../../includes/vpn-gateway-cross-premises-include.md)]

### <span data-ttu-id="4d44f-121"><a name="gwsku"></a>閘道 SKU</span><span class="sxs-lookup"><span data-stu-id="4d44f-121"><a name="gwsku"></a>Gateway SKUs</span></span>

[!INCLUDE [vpn-gateway-table-gwtype-aggtput](../../includes/vpn-gateway-table-gwtype-aggtput-include.md)]

### <span data-ttu-id="4d44f-122"><a name="wf"></a>工作流程</span><span class="sxs-lookup"><span data-stu-id="4d44f-122"><a name="wf"></a>Workflow</span></span>

<span data-ttu-id="4d44f-123">hello 下列清單會列出 hello 雲端連線。 常見的工作流程：</span><span class="sxs-lookup"><span data-stu-id="4d44f-123">hello following list outlines hello common workflow for cloud connectivity:</span></span>

1. <span data-ttu-id="4d44f-124">設計和計劃連線拓撲和清單 hello 位址空間的所有網路您想 tooconnect。</span><span class="sxs-lookup"><span data-stu-id="4d44f-124">Design and plan your connectivity topology and list hello address spaces for all networks you want tooconnect.</span></span>
2. <span data-ttu-id="4d44f-125">建立 Azure 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="4d44f-125">Create an Azure virtual network.</span></span> 
3. <span data-ttu-id="4d44f-126">建立 hello 虛擬網路的 VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="4d44f-126">Create a VPN gateway for hello virtual network.</span></span>
4. <span data-ttu-id="4d44f-127">建立並設定連接 tooon 內部部署網路或其他虛擬網路 （如有需要）。</span><span class="sxs-lookup"><span data-stu-id="4d44f-127">Create and configure connections tooon-premises networks or other virtual networks (as needed).</span></span>
5. <span data-ttu-id="4d44f-128">建立並設定 Azure VPN 閘道的點對站連線 (視需要)。</span><span class="sxs-lookup"><span data-stu-id="4d44f-128">Create and configure a Point-to-Site connection for your Azure VPN gateway (as needed).</span></span>

## <span data-ttu-id="4d44f-129"><a name="design"></a>設計</span><span class="sxs-lookup"><span data-stu-id="4d44f-129"><a name="design"></a>Design</span></span>
### <span data-ttu-id="4d44f-130"><a name="topologies"></a>連線拓撲</span><span class="sxs-lookup"><span data-stu-id="4d44f-130"><a name="topologies"></a>Connection topologies</span></span>

<span data-ttu-id="4d44f-131">先來看看 hello 中的 hello 圖表[有關 VPN 閘道](vpn-gateway-about-vpngateways.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="4d44f-131">Start by looking at hello diagrams in hello [About VPN Gateway](vpn-gateway-about-vpngateways.md) article.</span></span> <span data-ttu-id="4d44f-132">hello 發行項包含基本的圖表，每個拓撲，以及您可以使用 toodeploy 組態 hello 可用的部署工具的 hello 部署模型。</span><span class="sxs-lookup"><span data-stu-id="4d44f-132">hello article contains basic diagrams, hello deployment models for each topology, and hello available deployment tools you can use toodeploy your configuration.</span></span>

### <span data-ttu-id="4d44f-133"><a name="designbasics"></a>設計基本概念</span><span class="sxs-lookup"><span data-stu-id="4d44f-133"><a name="designbasics"></a>Design basics</span></span>

<span data-ttu-id="4d44f-134">hello 下列各節討論 hello VPN 閘道的基本概念。</span><span class="sxs-lookup"><span data-stu-id="4d44f-134">hello following sections discuss hello VPN gateway basics.</span></span> 

#### <span data-ttu-id="4d44f-135"><a name="servicelimits"></a>網路服務限制</span><span class="sxs-lookup"><span data-stu-id="4d44f-135"><a name="servicelimits"></a>Networking services limits</span></span>

<span data-ttu-id="4d44f-136">捲動 hello 資料表 tooview[網路服務限制](../azure-subscription-service-limits.md#networking-limits)。</span><span class="sxs-lookup"><span data-stu-id="4d44f-136">Scroll through hello tables tooview [networking services limits](../azure-subscription-service-limits.md#networking-limits).</span></span> <span data-ttu-id="4d44f-137">上述的 hello 限制可能會影響您的設計。</span><span class="sxs-lookup"><span data-stu-id="4d44f-137">hello limits listed may impact your design.</span></span>

#### <span data-ttu-id="4d44f-138"><a name="subnets"></a>關於子網路</span><span class="sxs-lookup"><span data-stu-id="4d44f-138"><a name="subnets"></a>About subnets</span></span>

<span data-ttu-id="4d44f-139">當您建立連線時，必須考量您的子網路範圍。</span><span class="sxs-lookup"><span data-stu-id="4d44f-139">When you are creating connections, you must consider your subnet ranges.</span></span> <span data-ttu-id="4d44f-140">子網路位址範圍不能重疊。</span><span class="sxs-lookup"><span data-stu-id="4d44f-140">You cannot have overlapping subnet address ranges.</span></span> <span data-ttu-id="4d44f-141">重疊的子網路時，一個虛擬網路或內部部署位置包含相同 hello 其他位置的位址空間包含的 hello。</span><span class="sxs-lookup"><span data-stu-id="4d44f-141">An overlapping subnet is when one virtual network or on-premises location contains hello same address space that hello other location contains.</span></span> <span data-ttu-id="4d44f-142">這表示的範圍，以針對您 toouse 您本機內部網路 toocarve 需要網路工程師，Azure ip 位址空間/子網路。</span><span class="sxs-lookup"><span data-stu-id="4d44f-142">This means that you need your network engineers for your local on-premises networks toocarve out a range for you toouse for your Azure IP addressing space/subnets.</span></span> <span data-ttu-id="4d44f-143">您需要不使用 hello 本機內部網路的位址空間。</span><span class="sxs-lookup"><span data-stu-id="4d44f-143">You need address space that is not being used on hello local on-premises network.</span></span>

<span data-ttu-id="4d44f-144">使用 VNet 對 VNet 連線時，也要注意避免重疊的子網路。</span><span class="sxs-lookup"><span data-stu-id="4d44f-144">Avoiding overlapping subnets is also important when you are working with VNet-to-VNet connections.</span></span> <span data-ttu-id="4d44f-145">如果您的子網路重疊的 IP 位址存在傳送 hello 和目的地的 Vnet，VNet 對 VNet 連線失敗。</span><span class="sxs-lookup"><span data-stu-id="4d44f-145">If your subnets overlap and an IP address exists in both hello sending and destination VNets, VNet-to-VNet connections fail.</span></span> <span data-ttu-id="4d44f-146">Azure 無法路由傳送 hello 資料 toohello 另一個 VNet 因為 hello 目的地位址是 hello 傳送 VNet 的一部分。</span><span class="sxs-lookup"><span data-stu-id="4d44f-146">Azure can't route hello data toohello other VNet because hello destination address is part of hello sending VNet.</span></span>

<span data-ttu-id="4d44f-147">「VPN 閘道」需要名為閘道子網路的特定子網路。</span><span class="sxs-lookup"><span data-stu-id="4d44f-147">VPN Gateways require a specific subnet called a gateway subnet.</span></span> <span data-ttu-id="4d44f-148">所有的閘道子網路必須命名為 GatewaySubnet toowork 正確。</span><span class="sxs-lookup"><span data-stu-id="4d44f-148">All gateway subnets must be named GatewaySubnet toowork properly.</span></span> <span data-ttu-id="4d44f-149">請務必不 tooname 您不同的閘道子網路名稱，而且不會部署到 Vm 或任何其他 toohello 閘道子網路。</span><span class="sxs-lookup"><span data-stu-id="4d44f-149">Be sure not tooname your gateway subnet a different name, and don't deploy VMs or anything else toohello gateway subnet.</span></span> <span data-ttu-id="4d44f-150">請參閱 [閘道子網路](vpn-gateway-about-vpn-gateway-settings.md#gwsub)。</span><span class="sxs-lookup"><span data-stu-id="4d44f-150">See [Gateway Subnets](vpn-gateway-about-vpn-gateway-settings.md#gwsub).</span></span>

#### <span data-ttu-id="4d44f-151"><a name="local"></a>關於區域網路閘道</span><span class="sxs-lookup"><span data-stu-id="4d44f-151"><a name="local"></a>About local network gateways</span></span>

<span data-ttu-id="4d44f-152">hello 區域網路閘道通常是指 tooyour 在內部部署位置。</span><span class="sxs-lookup"><span data-stu-id="4d44f-152">hello local network gateway typically refers tooyour on-premises location.</span></span> <span data-ttu-id="4d44f-153">Hello 傳統部署模型，在 hello 區域網路閘道會是參照的 tooas 本機網路站台。</span><span class="sxs-lookup"><span data-stu-id="4d44f-153">In hello classic deployment model, hello local network gateway is referred tooas a Local Network Site.</span></span> <span data-ttu-id="4d44f-154">當您設定區域網路閘道時，您會為它命名，指定 hello 公用 IP 位址的 hello 在內部部署 VPN 裝置，以及指定 hello 在內部部署位置中的 hello 位址首碼。</span><span class="sxs-lookup"><span data-stu-id="4d44f-154">When you configure a local network gateway, you give it a name, specify hello public IP address of hello on-premises VPN device, and specify hello address prefixes that are in hello on-premises location.</span></span> <span data-ttu-id="4d44f-155">Azure 會查看 hello 目的地位址首碼的網路流量、 參照您所指定的 hello 組態 hello 本機網路閘道，並據以路由傳送封包。</span><span class="sxs-lookup"><span data-stu-id="4d44f-155">Azure looks at hello destination address prefixes for network traffic, consults hello configuration that you have specified for hello local network gateway, and routes packets accordingly.</span></span> <span data-ttu-id="4d44f-156">您可以視需要修改 hello 位址前置詞。</span><span class="sxs-lookup"><span data-stu-id="4d44f-156">You can modify hello address prefixes as needed.</span></span> <span data-ttu-id="4d44f-157">如需詳細資訊，請參閱[區域網路閘道](vpn-gateway-about-vpn-gateway-settings.md#lng)。</span><span class="sxs-lookup"><span data-stu-id="4d44f-157">For more information, see [Local network gateways](vpn-gateway-about-vpn-gateway-settings.md#lng).</span></span>

#### <span data-ttu-id="4d44f-158"><a name="gwtype"></a>關於閘道類型</span><span class="sxs-lookup"><span data-stu-id="4d44f-158"><a name="gwtype"></a>About gateway types</span></span>

<span data-ttu-id="4d44f-159">選取您的拓撲的 hello 正確的閘道類型相當重要。</span><span class="sxs-lookup"><span data-stu-id="4d44f-159">Selecting hello correct gateway type for your topology is critical.</span></span> <span data-ttu-id="4d44f-160">如果您選取 hello 類型錯誤，您的閘道器就無法正常運作。</span><span class="sxs-lookup"><span data-stu-id="4d44f-160">If you select hello wrong type, your gateway won't work properly.</span></span> <span data-ttu-id="4d44f-161">hello 閘道類型指定 hello 閘道本身連接和 hello Resource Manager 部署模型的必要的組態設定的方式。</span><span class="sxs-lookup"><span data-stu-id="4d44f-161">hello gateway type specifies how hello gateway itself connects and is a required configuration setting for hello Resource Manager deployment model.</span></span>

<span data-ttu-id="4d44f-162">hello 閘道類型包括：</span><span class="sxs-lookup"><span data-stu-id="4d44f-162">hello gateway types are:</span></span>

* <span data-ttu-id="4d44f-163">Vpn</span><span class="sxs-lookup"><span data-stu-id="4d44f-163">Vpn</span></span>
* <span data-ttu-id="4d44f-164">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="4d44f-164">ExpressRoute</span></span>

#### <span data-ttu-id="4d44f-165"><a name="connectiontype"></a>關於連線類型</span><span class="sxs-lookup"><span data-stu-id="4d44f-165"><a name="connectiontype"></a>About connection types</span></span>

<span data-ttu-id="4d44f-166">每個組態皆需要特定的連線類型。</span><span class="sxs-lookup"><span data-stu-id="4d44f-166">Each configuration requires a specific connection type.</span></span> <span data-ttu-id="4d44f-167">hello 連線類型如下：</span><span class="sxs-lookup"><span data-stu-id="4d44f-167">hello connection types are:</span></span>

* <span data-ttu-id="4d44f-168">IPsec</span><span class="sxs-lookup"><span data-stu-id="4d44f-168">IPsec</span></span>
* <span data-ttu-id="4d44f-169">Vnet2Vnet</span><span class="sxs-lookup"><span data-stu-id="4d44f-169">Vnet2Vnet</span></span>
* <span data-ttu-id="4d44f-170">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="4d44f-170">ExpressRoute</span></span>
* <span data-ttu-id="4d44f-171">VPNClient</span><span class="sxs-lookup"><span data-stu-id="4d44f-171">VPNClient</span></span>

#### <span data-ttu-id="4d44f-172"><a name="vpntype"></a>關於 VPN 類型</span><span class="sxs-lookup"><span data-stu-id="4d44f-172"><a name="vpntype"></a>About VPN types</span></span>

<span data-ttu-id="4d44f-173">每個組態都需要特定 VPN 類型。</span><span class="sxs-lookup"><span data-stu-id="4d44f-173">Each configuration requires a specific VPN type.</span></span> <span data-ttu-id="4d44f-174">如果您要結合兩個組態，例如建立站對站連接和點對站連線 toohello 相同的 VNet，您必須使用符合這兩個連線需求的 VPN 類型。</span><span class="sxs-lookup"><span data-stu-id="4d44f-174">If you are combining two configurations, such as creating a Site-to-Site connection and a Point-to-Site connection toohello same VNet, you must use a VPN type that satisfies both connection requirements.</span></span>

[!INCLUDE [vpn-gateway-vpntype](../../includes/vpn-gateway-vpntype-include.md)]

<span data-ttu-id="4d44f-175">hello 下列表格顯示 hello VPN 類型為它所對應 tooeach 連接組態。</span><span class="sxs-lookup"><span data-stu-id="4d44f-175">hello following tables show hello VPN type as it maps tooeach connection configuration.</span></span> <span data-ttu-id="4d44f-176">請確定 hello 想 toocreate 您閘道的相符項目 hello 組態的 VPN 類型。</span><span class="sxs-lookup"><span data-stu-id="4d44f-176">Make sure hello VPN type for your gateway matches hello configuration that you want toocreate.</span></span> 

[!INCLUDE [vpn-gateway-table-vpntype](../../includes/vpn-gateway-table-vpntype-include.md)]

### <span data-ttu-id="4d44f-177"><a name="devices"></a>站對站連線的 VPN 裝置</span><span class="sxs-lookup"><span data-stu-id="4d44f-177"><a name="devices"></a>VPN devices for Site-to-Site connections</span></span>

<span data-ttu-id="4d44f-178">tooconfigure 網站-站台連線，不論部署模型，您需要下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="4d44f-178">tooconfigure a Site-to-Site connection, regardless of deployment model, you need hello following items:</span></span>

* <span data-ttu-id="4d44f-179">與 Azure VPN 閘道相容的 VPN 裝置</span><span class="sxs-lookup"><span data-stu-id="4d44f-179">A VPN device that is compatible with Azure VPN gateways</span></span>
* <span data-ttu-id="4d44f-180">不在 NAT 後方的公開 IPv4 IP 位址</span><span class="sxs-lookup"><span data-stu-id="4d44f-180">A public-facing IPv4 IP address that is not behind a NAT</span></span>

<span data-ttu-id="4d44f-181">您需要 toohave 體驗如何設定 VPN 裝置，或別人可為您設定裝置 hello。</span><span class="sxs-lookup"><span data-stu-id="4d44f-181">You need toohave experience configuring your VPN device, or have someone that can configure hello device for you.</span></span>

[!INCLUDE [vpn-gateway-configure-vpn-device-rm](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]

### <span data-ttu-id="4d44f-182"><a name="forcedtunnel"></a>考量強制通道路由</span><span class="sxs-lookup"><span data-stu-id="4d44f-182"><a name="forcedtunnel"></a>Consider forced tunnel routing</span></span>

<span data-ttu-id="4d44f-183">對於多數組態，您可以設定強制通道。</span><span class="sxs-lookup"><span data-stu-id="4d44f-183">For most configurations, you can configure forced tunneling.</span></span> <span data-ttu-id="4d44f-184">強制通道可讓您重新導向或 「 強制 」 所有網際網路繫結流量後 tooyour 在內部部署位置透過站對站 VPN 通道來檢查和稽核。</span><span class="sxs-lookup"><span data-stu-id="4d44f-184">Forced tunneling lets you redirect or "force" all Internet-bound traffic back tooyour on-premises location via a Site-to-Site VPN tunnel for inspection and auditing.</span></span> <span data-ttu-id="4d44f-185">這是多數企業 IT 原則的重要安全性需求。</span><span class="sxs-lookup"><span data-stu-id="4d44f-185">This is a critical security requirement for most enterprise IT policies.</span></span> 

<span data-ttu-id="4d44f-186">如果沒有強制通道，您在 Azure 中的 Vm 所傳來的網際網路繫結流量將一律周遊出 toohello 網際網路，而 hello 選項 tooallow 不直接的 Azure 網路基礎結構從您 tooinspect 或稽核 hello 流量。</span><span class="sxs-lookup"><span data-stu-id="4d44f-186">Without forced tunneling, Internet-bound traffic from your VMs in Azure will always traverse from Azure network infrastructure directly out toohello Internet, without hello option tooallow you tooinspect or audit hello traffic.</span></span> <span data-ttu-id="4d44f-187">Tooinformation 洩漏或其他類型的安全性漏洞，可能會導致未經授權的網際網路存取。</span><span class="sxs-lookup"><span data-stu-id="4d44f-187">Unauthorized Internet access can potentially lead tooinformation disclosure or other types of security breaches.</span></span>

<span data-ttu-id="4d44f-188">可以在這兩種部署模型中使用不同的工具，設定強制通道的連線。</span><span class="sxs-lookup"><span data-stu-id="4d44f-188">A forced tunneling connection can be configured in both deployment models and by using different tools.</span></span> <span data-ttu-id="4d44f-189">如需詳細資訊，請參閱[設定強制通道](vpn-gateway-forced-tunneling-rm.md)。</span><span class="sxs-lookup"><span data-stu-id="4d44f-189">For more information, see [Configure forced tunneling](vpn-gateway-forced-tunneling-rm.md).</span></span>

<span data-ttu-id="4d44f-190">**強制通道圖表**</span><span class="sxs-lookup"><span data-stu-id="4d44f-190">**Forced tunneling diagram**</span></span>

![Azure VPN 閘道強制通道圖表](./media/vpn-gateway-plan-design/forced-tunneling-diagram.png)

## <a name="next-steps"></a><span data-ttu-id="4d44f-192">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4d44f-192">Next steps</span></span>

<span data-ttu-id="4d44f-193">請參閱 hello [VPN 閘道常見問題集](vpn-gateway-vpn-faq.md)和[有關 VPN 閘道](vpn-gateway-about-vpngateways.md)文件的詳細資訊 toohelp 您與您的設計。</span><span class="sxs-lookup"><span data-stu-id="4d44f-193">See hello [VPN Gateway FAQ](vpn-gateway-vpn-faq.md) and [About VPN Gateway](vpn-gateway-about-vpngateways.md) articles for more information toohelp you with your design.</span></span>

<span data-ttu-id="4d44f-194">如需有關特定閘道設定的詳細資訊，請參閱 [關於 VPN 閘道設定](vpn-gateway-about-vpn-gateway-settings.md)。</span><span class="sxs-lookup"><span data-stu-id="4d44f-194">For more information about specific gateway settings, see [About VPN Gateway Settings](vpn-gateway-about-vpn-gateway-settings.md).</span></span>