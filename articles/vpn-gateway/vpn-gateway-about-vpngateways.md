---
title: "VPN 閘道概觀： 建立跨單位 VPN 連線 tooAzure 虛擬網路 |Microsoft 文件"
description: "此 VPN 閘道概觀說明 hello 方式 tooconnect tooAzure 虛擬網路透過 hello 網際網路使用 VPN 連線。 其中包含基本連接設定的圖表。"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 2358dd5a-cd76-42c3-baf3-2f35aadc64c8
ms.service: vpn-gateway
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/05/2017
ms.author: cherylmc
ms.openlocfilehash: 899270734270632a5b12d56021c924e977725a7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="about-vpn-gateway"></a><span data-ttu-id="d9d68-104">關於 VPN 閘道</span><span class="sxs-lookup"><span data-stu-id="d9d68-104">About VPN Gateway</span></span>

<span data-ttu-id="d9d68-105">VPN 閘道是一種虛擬網路閘道傳送加密的流量，跨公用連線 tooan 內部部署位置。</span><span class="sxs-lookup"><span data-stu-id="d9d68-105">A VPN gateway is a type of virtual network gateway that sends encrypted traffic across a public connection tooan on-premises location.</span></span> <span data-ttu-id="d9d68-106">您也可以使用透過 hello Microsoft 網路的 Azure 虛擬網路之間的 VPN 閘道 toosend 加密流量。</span><span class="sxs-lookup"><span data-stu-id="d9d68-106">You can also use VPN gateways toosend encrypted traffic between Azure virtual networks over hello Microsoft network.</span></span> <span data-ttu-id="d9d68-107">Azure 虛擬網路與內部部署網站之間 toosend 加密網路流量，您必須建立虛擬網路的 VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="d9d68-107">toosend encrypted network traffic between your Azure virtual network and your on-premises site, you must create a VPN gateway for your virtual network.</span></span>

<span data-ttu-id="d9d68-108">每個虛擬網路可以有只有一個 VPN 閘道，不過，您可以建立多個連線 toohello 相同的 VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="d9d68-108">Each virtual network can have only one VPN gateway, however, you can create multiple connections toohello same VPN gateway.</span></span> <span data-ttu-id="d9d68-109">例如，多站台連線設定。</span><span class="sxs-lookup"><span data-stu-id="d9d68-109">An example of this is a Multi-Site connection configuration.</span></span> <span data-ttu-id="d9d68-110">當您建立多個連線 toohello 相同的 VPN 閘道，所有 VPN 通道，包括點對站 Vpn，適用於 hello 閘道的共用 hello 頻寬。</span><span class="sxs-lookup"><span data-stu-id="d9d68-110">When you create multiple connections toohello same VPN gateway, all VPN tunnels, including Point-to-Site VPNs, share hello bandwidth that is available for hello gateway.</span></span>

### <span data-ttu-id="d9d68-111"><a name="whatis"></a>什麼是虛擬網路閘道？</span><span class="sxs-lookup"><span data-stu-id="d9d68-111"><a name="whatis"></a>What is a virtual network gateway?</span></span>

<span data-ttu-id="d9d68-112">虛擬網路閘道組成兩個或更多虛擬機器的部署稱為 hello GatewaySubnet tooa 特定子網路。</span><span class="sxs-lookup"><span data-stu-id="d9d68-112">A virtual network gateway is composed of two or more virtual machines that are deployed tooa specific subnet called hello GatewaySubnet.</span></span> <span data-ttu-id="d9d68-113">hello 位於的 hello 時建立 hello 虛擬網路閘道，GatewaySubnet 所建立的 Vm。</span><span class="sxs-lookup"><span data-stu-id="d9d68-113">hello VMs that are located in hello GatewaySubnet are created when you create hello virtual network gateway.</span></span> <span data-ttu-id="d9d68-114">虛擬網路閘道的 Vm 是已設定的 toocontain 路由表和閘道服務特定 toohello 閘道。</span><span class="sxs-lookup"><span data-stu-id="d9d68-114">Virtual network gateway VMs are configured toocontain routing tables and gateway services specific toohello gateway.</span></span> <span data-ttu-id="d9d68-115">您無法直接設定 hello 屬於 hello 虛擬網路閘道的 Vm，您絕對不要部署的其他資源 toohello GatewaySubnet。</span><span class="sxs-lookup"><span data-stu-id="d9d68-115">You can't directly configure hello VMs that are part of hello virtual network gateway and you should never deploy additional resources toohello GatewaySubnet.</span></span>

<span data-ttu-id="d9d68-116">當您建立虛擬網路閘道使用 hello 'Vpn' 的閘道類型時，它會建立特定類型的加密流量; 的虛擬網路閘道VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="d9d68-116">When you create a virtual network gateway using hello gateway type 'Vpn', it creates a specific type of virtual network gateway that encrypts traffic; a VPN gateway.</span></span> <span data-ttu-id="d9d68-117">VPN 閘道可能佔用 too45 分鐘 toocreate。</span><span class="sxs-lookup"><span data-stu-id="d9d68-117">A VPN gateway can take up too45 minutes toocreate.</span></span> <span data-ttu-id="d9d68-118">這是因為 hello VPN 閘道的 Vm hello 正在部署的 toohello GatewaySubnet 而設有 hello 您指定的設定。</span><span class="sxs-lookup"><span data-stu-id="d9d68-118">This is because hello VMs for hello VPN gateway are being deployed toohello GatewaySubnet and configured with hello settings that you specified.</span></span> <span data-ttu-id="d9d68-119">hello 您選取的閘道 SKU 決定的 vm 的強大功能 hello。</span><span class="sxs-lookup"><span data-stu-id="d9d68-119">hello Gateway SKU that you select determines how powerful hello VMs are.</span></span>

## <span data-ttu-id="d9d68-120"><a name="gwsku"></a>閘道 SKU</span><span class="sxs-lookup"><span data-stu-id="d9d68-120"><a name="gwsku"></a>Gateway SKUs</span></span>

[!INCLUDE [vpn-gateway-gwsku-include](../../includes/vpn-gateway-gwsku-include.md)]

## <span data-ttu-id="d9d68-121"><a name="configuring"></a>設定 VPN 閘道</span><span class="sxs-lookup"><span data-stu-id="d9d68-121"><a name="configuring"></a>Configuring a VPN Gateway</span></span>

<span data-ttu-id="d9d68-122">VPN 閘道連線需仰賴多個具有特定設定的資源。</span><span class="sxs-lookup"><span data-stu-id="d9d68-122">A VPN gateway connection relies on multiple resources that are configured with specific settings.</span></span> <span data-ttu-id="d9d68-123">大部分的 hello 資源可個別設定，但必須以特定順序，在某些情況下進行設定。</span><span class="sxs-lookup"><span data-stu-id="d9d68-123">Most of hello resources can be configured separately, although they must be configured in a certain order in some cases.</span></span>

### <span data-ttu-id="d9d68-124"><a name="settings"></a>設定</span><span class="sxs-lookup"><span data-stu-id="d9d68-124"><a name="settings"></a>Settings</span></span>

<span data-ttu-id="d9d68-125">您選擇的每個資源的 hello 設定是重大 toocreating 成功的連接。</span><span class="sxs-lookup"><span data-stu-id="d9d68-125">hello settings that you chose for each resource are critical toocreating a successful connection.</span></span> <span data-ttu-id="d9d68-126">如需 VPN 閘道個別資源和設定的資訊，請參閱 [關於 VPN 閘道設定](vpn-gateway-about-vpn-gateway-settings.md)。</span><span class="sxs-lookup"><span data-stu-id="d9d68-126">For information about individual resources and settings for VPN Gateway, see [About VPN Gateway settings](vpn-gateway-about-vpn-gateway-settings.md).</span></span> <span data-ttu-id="d9d68-127">hello 發行項包含資訊 toohelp 您了解閘道類型、 VPN 類型、 連接類型，閘道子網路、 區域網路閘道，以及各種其他您可能想 tooconsider 的資源設定。</span><span class="sxs-lookup"><span data-stu-id="d9d68-127">hello article contains information toohelp you understand gateway types, VPN types, connection types, gateway subnets, local network gateways, and various other resource settings that you may want tooconsider.</span></span>

### <span data-ttu-id="d9d68-128"><a name="tools"></a>部署工具</span><span class="sxs-lookup"><span data-stu-id="d9d68-128"><a name="tools"></a>Deployment tools</span></span>

<span data-ttu-id="d9d68-129">您可以開始建立及設定使用組態工具，例如 hello Azure 入口網站的資源。</span><span class="sxs-lookup"><span data-stu-id="d9d68-129">You can start out creating and configuring resources using one configuration tool, such as hello Azure portal.</span></span> <span data-ttu-id="d9d68-130">您可以在之後決定 tooswitch tooanother 工具，例如 PowerShell tooconfigure 其他資源，或修改現有的資源時適用。</span><span class="sxs-lookup"><span data-stu-id="d9d68-130">You can later decide tooswitch tooanother tool, such as PowerShell, tooconfigure additional resources, or modify existing resources when applicable.</span></span> <span data-ttu-id="d9d68-131">目前，您無法在 hello Azure 入口網站中設定每個資源和資源設定。</span><span class="sxs-lookup"><span data-stu-id="d9d68-131">Currently, you can't configure every resource and resource setting in hello Azure portal.</span></span> <span data-ttu-id="d9d68-132">hello 文章中的每個連線的拓撲中的 hello 指示指定的特定組態工具會在需要時。</span><span class="sxs-lookup"><span data-stu-id="d9d68-132">hello instructions in hello articles for each connection topology specify when a specific configuration tool is needed.</span></span> 

### <span data-ttu-id="d9d68-133"><a name="models"></a>部署模型</span><span class="sxs-lookup"><span data-stu-id="d9d68-133"><a name="models"></a>Deployment model</span></span>

<span data-ttu-id="d9d68-134">當您設定 VPN 閘道時，hello 採取的步驟取決於 hello 部署模型，您使用 toocreate 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="d9d68-134">When you configure a VPN gateway, hello steps you take depend on hello deployment model that you used toocreate your virtual network.</span></span> <span data-ttu-id="d9d68-135">比方說，如果您已建立您的 VNet 使用 hello 傳統部署模型，使用 hello 指導方針與指示 hello 傳統部署模型 toocreate 及設定 VPN 閘道設定。</span><span class="sxs-lookup"><span data-stu-id="d9d68-135">For example, if you created your VNet using hello classic deployment model, you use hello guidelines and instructions for hello classic deployment model toocreate and configure your VPN gateway settings.</span></span> <span data-ttu-id="d9d68-136">如需部署模型的詳細資訊，請參閱 [了解 Resource Manager 和傳統部署模型](../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="d9d68-136">For more information about deployment models, see [Understanding Resource Manager and classic deployment models](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>

## <span data-ttu-id="d9d68-137"><a name="diagrams"></a>連線拓撲圖表</span><span class="sxs-lookup"><span data-stu-id="d9d68-137"><a name="diagrams"></a>Connection topology diagrams</span></span>

<span data-ttu-id="d9d68-138">有不同的組態可用於 VPN 閘道連線的重要 tooknow 它。</span><span class="sxs-lookup"><span data-stu-id="d9d68-138">It's important tooknow that there are different configurations available for VPN gateway connections.</span></span> <span data-ttu-id="d9d68-139">您需要哪些設定最符合您需求的 toodetermine。</span><span class="sxs-lookup"><span data-stu-id="d9d68-139">You need toodetermine which configuration best fits your needs.</span></span> <span data-ttu-id="d9d68-140">在下列 hello 章節，您可以檢視 hello 遵循 VPN 閘道連線的相關資訊和拓撲圖表： hello 下列各節包含的資料表清單：</span><span class="sxs-lookup"><span data-stu-id="d9d68-140">In hello sections below, you can view information and topology diagrams about hello following VPN gateway connections: hello following sections contain tables which list:</span></span>

* <span data-ttu-id="d9d68-141">可用的部署模型</span><span class="sxs-lookup"><span data-stu-id="d9d68-141">Available deployment model</span></span>
* <span data-ttu-id="d9d68-142">可用的設定工具</span><span class="sxs-lookup"><span data-stu-id="d9d68-142">Available configuration tools</span></span>
* <span data-ttu-id="d9d68-143">帶您連結直接 tooan 文件： 如果有的話</span><span class="sxs-lookup"><span data-stu-id="d9d68-143">Links that take you directly tooan article, if available</span></span>

<span data-ttu-id="d9d68-144">使用 hello 圖表和描述 toohelp 選取 hello 連線拓撲 toomatch 您的需求。</span><span class="sxs-lookup"><span data-stu-id="d9d68-144">Use hello diagrams and descriptions toohelp select hello connection topology toomatch your requirements.</span></span> <span data-ttu-id="d9d68-145">hello 圖表顯示 hello 主要基準拓撲，但可能 toobuild 當做指導方針使用 hello 圖表更複雜的組態。</span><span class="sxs-lookup"><span data-stu-id="d9d68-145">hello diagrams show hello main baseline topologies, but it's possible toobuild more complex configurations using hello diagrams as a guideline.</span></span>

## <span data-ttu-id="d9d68-146"><a name="s2smulti"></a>站對站以及多網站 (IPsec/IKE VPN 通道)</span><span class="sxs-lookup"><span data-stu-id="d9d68-146"><a name="s2smulti"></a>Site-to-Site and Multi-Site (IPsec/IKE VPN tunnel)</span></span>

### <span data-ttu-id="d9d68-147"><a name="S2S"></a>站對站</span><span class="sxs-lookup"><span data-stu-id="d9d68-147"><a name="S2S"></a>Site-to-Site</span></span>

<span data-ttu-id="d9d68-148">網站間 (S2S) VPN 閘道連線是透過 IPsec/IKE (IKEv1 或 IKEv2) VPN 通道建立的連線。</span><span class="sxs-lookup"><span data-stu-id="d9d68-148">A Site-to-Site (S2S) VPN gateway connection is a connection over IPsec/IKE (IKEv1 or IKEv2) VPN tunnel.</span></span> <span data-ttu-id="d9d68-149">S2S 連線需要 VPN 裝置位於內部部署具有公用 IP 位址指派 tooit 並不位於 NAT 後方。</span><span class="sxs-lookup"><span data-stu-id="d9d68-149">A S2S connection requires a VPN device located on-premises that has a public IP address assigned tooit and is not located behind a NAT.</span></span> <span data-ttu-id="d9d68-150">S2S 連線可以用於跨單位與混合式組態。</span><span class="sxs-lookup"><span data-stu-id="d9d68-150">S2S connections can be used for cross-premises and hybrid configurations.</span></span>   

![Azure VPN 閘道站對站連接範例](./media/vpn-gateway-about-vpngateways/vpngateway-site-to-site-connection-diagram.png)

### <span data-ttu-id="d9d68-152"><a name="Multi"></a>多站台</span><span class="sxs-lookup"><span data-stu-id="d9d68-152"><a name="Multi"></a>Multi-Site</span></span>

<span data-ttu-id="d9d68-153">此連線類型是 hello 站對站連線的變化。</span><span class="sxs-lookup"><span data-stu-id="d9d68-153">This type of connection is a variation of hello Site-to-Site connection.</span></span> <span data-ttu-id="d9d68-154">您可以建立多個 VPN 連線從您的虛擬網路閘道，通常連接 toomultiple 內部部署站台。</span><span class="sxs-lookup"><span data-stu-id="d9d68-154">You create more than one VPN connection from your virtual network gateway, typically connecting toomultiple on-premises sites.</span></span> <span data-ttu-id="d9d68-155">處理多重連線時，您必須使用路由式 VPN 類型 (也就是使用傳統 VNet 時的動態閘道)。</span><span class="sxs-lookup"><span data-stu-id="d9d68-155">When working with multiple connections, you must use a RouteBased VPN type (known as a dynamic gateway when working with classic VNets).</span></span> <span data-ttu-id="d9d68-156">因為每個虛擬網路只能有一個 VPN 閘道，則所有透過 hello 閘道的連線共用 hello 可用的頻寬。</span><span class="sxs-lookup"><span data-stu-id="d9d68-156">Because each virtual network can only have one VPN gateway, all connections through hello gateway share hello available bandwidth.</span></span> <span data-ttu-id="d9d68-157">這通常稱為「多網站」連線。</span><span class="sxs-lookup"><span data-stu-id="d9d68-157">This is often called a "multi-site" connection.</span></span>

![Azure VPN 閘道多網站連接範例](./media/vpn-gateway-about-vpngateways/vpngateway-multisite-connection-diagram.png)

### <a name="deployment-models-and-methods-for-site-to-site-and-multi-site"></a><span data-ttu-id="d9d68-159">站對站和多網站的部署模型和方法</span><span class="sxs-lookup"><span data-stu-id="d9d68-159">Deployment models and methods for Site-to-Site and Multi-Site</span></span>

[!INCLUDE [vpn-gateway-table-site-to-site](../../includes/vpn-gateway-table-site-to-site-include.md)]

## <span data-ttu-id="d9d68-160"><a name="P2S"></a>點對站 (透過 SSTP 的 VPN)</span><span class="sxs-lookup"><span data-stu-id="d9d68-160"><a name="P2S"></a>Point-to-Site (VPN over SSTP)</span></span>

<span data-ttu-id="d9d68-161">點對站 (P2S) VPN 閘道，可讓您建立從個別的用戶端電腦的安全連線 tooyour 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="d9d68-161">A Point-to-Site (P2S) VPN gateway lets you create a secure connection tooyour virtual network from an individual client computer.</span></span> <span data-ttu-id="d9d68-162">當您想要 tooconnect tooyour 從遠端位置，例如當您從家裡或會議 telecommuting VNet，點對站 VPN 連線會很有用。</span><span class="sxs-lookup"><span data-stu-id="d9d68-162">Point-to-Site VPN connections are useful when you want tooconnect tooyour VNet from a remote location, such when you are telecommuting from home or a conference.</span></span> <span data-ttu-id="d9d68-163">您有只有少數的用戶端需要 tooconnect tooa VNet 時 P2S VPN 也很有用的方案 toouse，而不是站對站 VPN。</span><span class="sxs-lookup"><span data-stu-id="d9d68-163">A P2S VPN is also a useful solution toouse instead of a Site-to-Site VPN when you have only a few clients that need tooconnect tooa VNet.</span></span> 

<span data-ttu-id="d9d68-164">如同 S2S 連線，P2S 連線不需要內部部署公眾對應 IP 位址或 VPN 裝置。</span><span class="sxs-lookup"><span data-stu-id="d9d68-164">Unlike S2S connections, P2S connections do not require an on-premises public-facing IP address or a VPN device.</span></span> <span data-ttu-id="d9d68-165">P2S 連接只能使用透過 S2S 連線 hello 相同的 VPN 閘道，只要所有 hello 組態需求的兩個連線都相容。</span><span class="sxs-lookup"><span data-stu-id="d9d68-165">P2S connections can be used with S2S connections through hello same VPN gateway, as long as all hello configuration requirements for both connections are compatible.</span></span>

<span data-ttu-id="d9d68-166">使用 P2S hello 安全通訊端通道通訊協定 (SSTP)，這是 SSL 型 VPN 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="d9d68-166">P2S uses hello Secure Socket Tunneling Protocol (SSTP), which is an SSL-based VPN protocol.</span></span> <span data-ttu-id="d9d68-167">建立之 P2S VPN 連線從 hello 用戶端電腦。</span><span class="sxs-lookup"><span data-stu-id="d9d68-167">A P2S VPN connection is established by starting it from hello client computer.</span></span>

![Azure VPN 閘道點對站連接範例](./media/vpn-gateway-about-vpngateways/vpngateway-point-to-site-connection-diagram.png)

### <a name="deployment-models-and-methods-for-point-to-site"></a><span data-ttu-id="d9d68-169">點對站的部署模型和方法</span><span class="sxs-lookup"><span data-stu-id="d9d68-169">Deployment models and methods for Point-to-Site</span></span>

[!INCLUDE [vpn-gateway-table-point-to-site](../../includes/vpn-gateway-table-point-to-site-include.md)]

## <span data-ttu-id="d9d68-170"><a name="V2V"></a>VNet 對 VNet 連線 (IPsec/IKE VPN 通道)</span><span class="sxs-lookup"><span data-stu-id="d9d68-170"><a name="V2V"></a>VNet-to-VNet connections (IPsec/IKE VPN tunnel)</span></span>

<span data-ttu-id="d9d68-171">連接虛擬網路 tooanother 虛擬網路 (VNet 對 VNet) 是類似 tooconnecting VNet tooan 在內部部署站台位置。</span><span class="sxs-lookup"><span data-stu-id="d9d68-171">Connecting a virtual network tooanother virtual network (VNet-to-VNet) is similar tooconnecting a VNet tooan on-premises site location.</span></span> <span data-ttu-id="d9d68-172">這兩種連線類型使用的 VPN 閘道 tooprovide 採用 IPsec/IKE 的安全通道。</span><span class="sxs-lookup"><span data-stu-id="d9d68-172">Both connectivity types use a VPN gateway tooprovide a secure tunnel using IPsec/IKE.</span></span> <span data-ttu-id="d9d68-173">您甚至可以將多網站連線組態與 VNet 對 VNet 通訊結合。</span><span class="sxs-lookup"><span data-stu-id="d9d68-173">You can even combine VNet-to-VNet communication with multi-site connection configurations.</span></span> <span data-ttu-id="d9d68-174">這可讓您建立結合了跨單位連線與內部虛擬網路連線的網路拓撲。</span><span class="sxs-lookup"><span data-stu-id="d9d68-174">This lets you establish network topologies that combine cross-premises connectivity with inter-virtual network connectivity.</span></span>

<span data-ttu-id="d9d68-175">可以是您所連接的 Vnet hello:</span><span class="sxs-lookup"><span data-stu-id="d9d68-175">hello VNets you connect can be:</span></span>

* <span data-ttu-id="d9d68-176">在 hello 相同或不同區域</span><span class="sxs-lookup"><span data-stu-id="d9d68-176">in hello same or different regions</span></span>
* <span data-ttu-id="d9d68-177">在 hello 相同或不同的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="d9d68-177">in hello same or different subscriptions</span></span> 
* <span data-ttu-id="d9d68-178">在 hello 相同或不同的部署模型</span><span class="sxs-lookup"><span data-stu-id="d9d68-178">in hello same or different deployment models</span></span>

![Azure VPN 閘道 VNet tooVNet 連接範例](./media/vpn-gateway-about-vpngateways/vpngateway-vnet-to-vnet-connection-diagram.png)

### <a name="connections-between-deployment-models"></a><span data-ttu-id="d9d68-180">部署模型之間的連線</span><span class="sxs-lookup"><span data-stu-id="d9d68-180">Connections between deployment models</span></span>

<span data-ttu-id="d9d68-181">Azure 目前有兩種部署模型：傳統和 Resource Manager。</span><span class="sxs-lookup"><span data-stu-id="d9d68-181">Azure currently has two deployment models: classic and Resource Manager.</span></span> <span data-ttu-id="d9d68-182">如果您已使用 Azure 一段時間，則可能具有傳統 VNet 上執行的 Azure VM 和執行個體角色。</span><span class="sxs-lookup"><span data-stu-id="d9d68-182">If you have been using Azure for some time, you probably have Azure VMs and instance roles running in a classic VNet.</span></span> <span data-ttu-id="d9d68-183">較新的 VM 和角色執行個體可能會在 Resource Manager 中建立的 VNet 中執行。</span><span class="sxs-lookup"><span data-stu-id="d9d68-183">Your newer VMs and role instances may be running in a VNet created in Resource Manager.</span></span> <span data-ttu-id="d9d68-184">您可以在直接與資源在另一個 VNet toocommunicate 建立 hello Vnet tooallow 之間的連線 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="d9d68-184">You can create a connection between hello VNets tooallow hello resources in one VNet toocommunicate directly with resources in another.</span></span>

### <a name="vnet-peering"></a><span data-ttu-id="d9d68-185">VNet 對等互連</span><span class="sxs-lookup"><span data-stu-id="d9d68-185">VNet peering</span></span>

<span data-ttu-id="d9d68-186">您可能無法 toouse VNet 對等互連 toocreate 您的連接，只要您的虛擬網路會符合特定需求。</span><span class="sxs-lookup"><span data-stu-id="d9d68-186">You may be able toouse VNet peering toocreate your connection, as long as your virtual network meets certain requirements.</span></span> <span data-ttu-id="d9d68-187">VNet 對等互連不會使用虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="d9d68-187">VNet peering does not use a virtual network gateway.</span></span> <span data-ttu-id="d9d68-188">如需詳細資訊，請參閱 [VNet 對等互連](../virtual-network/virtual-network-peering-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="d9d68-188">For more information, see [VNet peering](../virtual-network/virtual-network-peering-overview.md).</span></span>

### <a name="deployment-models-and-methods-for-vnet-to-vnet"></a><span data-ttu-id="d9d68-189">VNet 對 VNet 的部署模型和方法</span><span class="sxs-lookup"><span data-stu-id="d9d68-189">Deployment models and methods for VNet-to-VNet</span></span>

[!INCLUDE [vpn-gateway-table-vnet-to-vnet](../../includes/vpn-gateway-table-vnet-to-vnet-include.md)]

## <span data-ttu-id="d9d68-190"><a name="ExpressRoute"></a>ExpressRoute (專用的私人連線)</span><span class="sxs-lookup"><span data-stu-id="d9d68-190"><a name="ExpressRoute"></a>ExpressRoute (dedicated private connection)</span></span>

<span data-ttu-id="d9d68-191">Microsoft Azure ExpressRoute 可讓您將您在內部部署網路擴充至 hello Microsoft 雲端中，透過連線服務提供者所提供的專用私人連接。</span><span class="sxs-lookup"><span data-stu-id="d9d68-191">Microsoft Azure ExpressRoute lets you extend your on-premises networks into hello Microsoft cloud over a dedicated private connection facilitated by a connectivity provider.</span></span> <span data-ttu-id="d9d68-192">透過 ExpressRoute，您可以建立連線 tooMicrosoft 雲端服務，例如 Microsoft Azure、 Office 365 和 CRM Online。</span><span class="sxs-lookup"><span data-stu-id="d9d68-192">With ExpressRoute, you can establish connections tooMicrosoft cloud services, such as Microsoft Azure, Office 365, and CRM Online.</span></span> <span data-ttu-id="d9d68-193">從任意點對任意點 (IP VPN) 網路、點對點乙太網路，或在共置設施上透過連線提供者的虛擬交叉連接，都可以進行連線。</span><span class="sxs-lookup"><span data-stu-id="d9d68-193">Connectivity can be from an any-to-any (IP VPN) network, a point-to-point Ethernet network, or a virtual cross-connection through a connectivity provider at a co-location facility.</span></span>

<span data-ttu-id="d9d68-194">ExpressRoute 連線不會經過 hello 公用網際網路。</span><span class="sxs-lookup"><span data-stu-id="d9d68-194">ExpressRoute connections do not go over hello public Internet.</span></span> <span data-ttu-id="d9d68-195">這可讓 ExpressRoute 連線 toooffer 詳細可靠性、 速度、 延遲更少和較高的安全性比一般連線透過網際網路 hello。</span><span class="sxs-lookup"><span data-stu-id="d9d68-195">This allows ExpressRoute connections toooffer more reliability, faster speeds, lower latencies, and higher security than typical connections over hello Internet.</span></span>

<span data-ttu-id="d9d68-196">ExpressRoute 連線不會使用 VPN 閘道，但是會以虛擬網路閘道做為其必要組態的一部分。</span><span class="sxs-lookup"><span data-stu-id="d9d68-196">An ExpressRoute connection does not use a VPN gateway, although it does use a virtual network gateway as part of its required configuration.</span></span> <span data-ttu-id="d9d68-197">ExpressRoute 連線，在 hello 虛擬網路閘道被設定為使用 'ExpressRoute'，而不是 'Vpn' hello 閘道類型。</span><span class="sxs-lookup"><span data-stu-id="d9d68-197">In an ExpressRoute connection, hello virtual network gateway is configured with hello gateway type 'ExpressRoute', rather than 'Vpn'.</span></span> <span data-ttu-id="d9d68-198">如需 ExpressRoute 的詳細資訊，請參閱 hello [ExpressRoute 技術概觀](../expressroute/expressroute-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="d9d68-198">For more information about ExpressRoute, see hello [ExpressRoute technical overview](../expressroute/expressroute-introduction.md).</span></span>

## <span data-ttu-id="d9d68-199"><a name="coexisting"></a>站對站及 ExpressRoute 並存連線</span><span class="sxs-lookup"><span data-stu-id="d9d68-199"><a name="coexisting"></a>Site-to-Site and ExpressRoute coexisting connections</span></span>

<span data-ttu-id="d9d68-200">ExpressRoute 是直接從您的 WAN 專用連線 (不透過 hello 公用網際網路) tooMicrosoft 服務，包括 Azure。</span><span class="sxs-lookup"><span data-stu-id="d9d68-200">ExpressRoute is a direct, dedicated connection from your WAN (not over hello public Internet) tooMicrosoft Services, including Azure.</span></span> <span data-ttu-id="d9d68-201">站對站 VPN 流量的傳輸會透過 hello 加密公用網際網路。</span><span class="sxs-lookup"><span data-stu-id="d9d68-201">Site-to-Site VPN traffic travels encrypted over hello public Internet.</span></span> <span data-ttu-id="d9d68-202">要能 tooconfigure 站對站 VPN 和 ExpressRoute 連線 hello 相同虛擬網路有多項優點。</span><span class="sxs-lookup"><span data-stu-id="d9d68-202">Being able tooconfigure Site-to-Site VPN and ExpressRoute connections for hello same virtual network has several advantages.</span></span>

<span data-ttu-id="d9d68-203">您可以設定站對站 VPN，安全的容錯移轉路徑做為 ExpressRoute，或使用站對站 Vpn tooconnect toosites 不是您網路的一部分，但透過 ExpressRoute 連接。</span><span class="sxs-lookup"><span data-stu-id="d9d68-203">You can configure a Site-to-Site VPN as a secure failover path for ExpressRoute, or use Site-to-Site VPNs tooconnect toosites that are not part of your network, but that are connected through ExpressRoute.</span></span> <span data-ttu-id="d9d68-204">請注意，此設定需要兩個虛擬網路閘道的 hello 相同虛擬網路，另一個使用 hello 閘道類型 'Vpn' hello 'ExpressRoute' 利用 hello 閘道類型。</span><span class="sxs-lookup"><span data-stu-id="d9d68-204">Notice that this configuration requires two virtual network gateways for hello same virtual network, one using hello gateway type 'Vpn', and hello other using hello gateway type 'ExpressRoute'.</span></span>

![ExpressRoute 和 VPN 閘道並存連接範例](./media/vpn-gateway-about-vpngateways/expressroute-vpngateway-coexisting-connections-diagram.png)

### <a name="deployment-models-and-methods-for-s2s-and-expressroute"></a><span data-ttu-id="d9d68-206">S2S 和 ExpressRoute 的部署模型和方法</span><span class="sxs-lookup"><span data-stu-id="d9d68-206">Deployment models and methods for S2S and ExpressRoute</span></span>

[!INCLUDE [vpn-gateway-table-coexist](../../includes/vpn-gateway-table-coexist-include.md)]

## <a name="pricing"></a><span data-ttu-id="d9d68-207">價格</span><span class="sxs-lookup"><span data-stu-id="d9d68-207">Pricing</span></span>

[!INCLUDE [vpn-gateway-about-pricing-include](../../includes/vpn-gateway-about-pricing-include.md)]

<span data-ttu-id="d9d68-208">如需 VPN 閘道之閘道 SKU 的詳細資訊，請參閱[閘道 SKU](vpn-gateway-about-vpn-gateway-settings.md#gwsku)。</span><span class="sxs-lookup"><span data-stu-id="d9d68-208">For more information about gateway SKUs for VPN Gateway, see [Gateway SKUs](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span></span>

## <span data-ttu-id="d9d68-209"><a name="faq"></a>常見問題集</span><span class="sxs-lookup"><span data-stu-id="d9d68-209"><a name="faq"></a>FAQ</span></span>

<span data-ttu-id="d9d68-210">常見問題集疑問 VPN 閘道的詳細資訊，請參閱 hello [VPN 閘道常見問題集](vpn-gateway-vpn-faq.md)。</span><span class="sxs-lookup"><span data-stu-id="d9d68-210">For frequently asked questions about VPN gateway, see hello [VPN Gateway FAQ](vpn-gateway-vpn-faq.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d9d68-211">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d9d68-211">Next steps</span></span>

- <span data-ttu-id="d9d68-212">規劃您的 VPN 閘道設定。</span><span class="sxs-lookup"><span data-stu-id="d9d68-212">Plan your VPN gateway configuration.</span></span> <span data-ttu-id="d9d68-213">請參閱 [VPN 閘道的規劃與設計](vpn-gateway-plan-design.md)。</span><span class="sxs-lookup"><span data-stu-id="d9d68-213">See [VPN Gateway Planning and Design](vpn-gateway-plan-design.md).</span></span>
- <span data-ttu-id="d9d68-214">檢視 hello [VPN 閘道常見問題集](vpn-gateway-vpn-faq.md)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="d9d68-214">View hello [VPN Gateway FAQ](vpn-gateway-vpn-faq.md) for additional information.</span></span>
- <span data-ttu-id="d9d68-215">檢視 hello[訂用帳戶和服務限制](../azure-subscription-service-limits.md#networking-limits)。</span><span class="sxs-lookup"><span data-stu-id="d9d68-215">View hello [Subscription and service limits](../azure-subscription-service-limits.md#networking-limits).</span></span>
- <span data-ttu-id="d9d68-216">深入了解一些 hello 另一個索引鍵[網路功能](../networking/networking-overview.md)的 Azure。</span><span class="sxs-lookup"><span data-stu-id="d9d68-216">Learn about some of hello other key [networking capabilities](../networking/networking-overview.md) of Azure.</span></span>
