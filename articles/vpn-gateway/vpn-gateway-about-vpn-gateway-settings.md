---
title: "跨單位 Azure 連線的 aaaVPN 閘道設定 |Microsoft 文件"
description: "了解 Azure 虛擬網路閘道的 VPN 閘道設定。"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: ae665bc5-0089-45d0-a0d5-bc0ab4e79899
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/26/2017
ms.author: cherylmc
ms.openlocfilehash: 01229d99fa37e30e00aa00f939f488d631b5593c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="about-vpn-gateway-configuration-settings"></a><span data-ttu-id="570f0-103">關於 VPN 閘道組態設定</span><span class="sxs-lookup"><span data-stu-id="570f0-103">About VPN Gateway configuration settings</span></span>

<span data-ttu-id="570f0-104">VPN 閘道是一種虛擬網路閘道，可透過公用連線在您的虛擬網路和內部部署位置之間傳送加密流量。</span><span class="sxs-lookup"><span data-stu-id="570f0-104">A VPN gateway is a type of virtual network gateway that sends encrypted traffic between your virtual network and your on-premises location across a public connection.</span></span> <span data-ttu-id="570f0-105">您也可以使用 hello Azure 骨幹上的虛擬網路之間的 VPN 閘道 toosend 流量。</span><span class="sxs-lookup"><span data-stu-id="570f0-105">You can also use a VPN gateway toosend traffic between virtual networks across hello Azure backbone.</span></span>

<span data-ttu-id="570f0-106">VPN 閘道連線依賴 hello 設定多個資源，其中每一個都包含可設定的設定。</span><span class="sxs-lookup"><span data-stu-id="570f0-106">A VPN gateway connection relies on hello configuration of multiple resources, each of which contains configurable settings.</span></span> <span data-ttu-id="570f0-107">本文章中的 hello 各節將討論 hello 資源和 tooa Resource Manager 部署模型中建立虛擬網路的 VPN 閘道與相關聯的設定。</span><span class="sxs-lookup"><span data-stu-id="570f0-107">hello sections in this article discuss hello resources and settings that relate tooa VPN gateway for a virtual network created in Resource Manager deployment model.</span></span> <span data-ttu-id="570f0-108">您可以找到 hello 中每個連線解決方案說明和拓撲圖表[有關 VPN 閘道](vpn-gateway-about-vpngateways.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="570f0-108">You can find descriptions and topology diagrams for each connection solution in hello [About VPN Gateway](vpn-gateway-about-vpngateways.md) article.</span></span>

## <span data-ttu-id="570f0-109"><a name="gwtype"></a>閘道類型</span><span class="sxs-lookup"><span data-stu-id="570f0-109"><a name="gwtype"></a>Gateway types</span></span>

<span data-ttu-id="570f0-110">每個虛擬網路只能有一個各類型的虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="570f0-110">Each virtual network can only have one virtual network gateway of each type.</span></span> <span data-ttu-id="570f0-111">當您建立虛擬網路閘道時，您必須確定 hello 閘道類型正確設定。</span><span class="sxs-lookup"><span data-stu-id="570f0-111">When you are creating a virtual network gateway, you must make sure that hello gateway type is correct for your configuration.</span></span>

<span data-ttu-id="570f0-112">hello-gatewaytype 的授權提供值如下：</span><span class="sxs-lookup"><span data-stu-id="570f0-112">hello available values for -GatewayType are:</span></span>

* <span data-ttu-id="570f0-113">Vpn</span><span class="sxs-lookup"><span data-stu-id="570f0-113">Vpn</span></span>
* <span data-ttu-id="570f0-114">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="570f0-114">ExpressRoute</span></span>

<span data-ttu-id="570f0-115">VPN 閘道需要 hello `-GatewayType` *Vpn*。</span><span class="sxs-lookup"><span data-stu-id="570f0-115">A VPN gateway requires hello `-GatewayType` *Vpn*.</span></span>

<span data-ttu-id="570f0-116">範例：</span><span class="sxs-lookup"><span data-stu-id="570f0-116">Example:</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig -GatewayType Vpn `
-VpnType RouteBased
```

## <span data-ttu-id="570f0-117"><a name="gwsku"></a>閘道 SKU</span><span class="sxs-lookup"><span data-stu-id="570f0-117"><a name="gwsku"></a>Gateway SKUs</span></span>

[!INCLUDE [vpn-gateway-gwsku-include](../../includes/vpn-gateway-gwsku-include.md)]

### <a name="configure-hello-gateway-sku"></a><span data-ttu-id="570f0-118">設定 hello 閘道 SKU</span><span class="sxs-lookup"><span data-stu-id="570f0-118">Configure hello gateway SKU</span></span>

#### <a name="azure-portal"></a><span data-ttu-id="570f0-119">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="570f0-119">Azure portal</span></span>

<span data-ttu-id="570f0-120">如果您使用 hello Azure 入口網站 toocreate 資源管理員虛擬網路閘道，您可以使用 hello 下拉式清單中選取 hello 閘道 SKU。</span><span class="sxs-lookup"><span data-stu-id="570f0-120">If you use hello Azure portal toocreate a Resource Manager virtual network gateway, you can select hello gateway SKU by using hello dropdown.</span></span> <span data-ttu-id="570f0-121">hello 選項，您會看到對應 toohello 閘道類型和您選取的 VPN 類型。</span><span class="sxs-lookup"><span data-stu-id="570f0-121">hello options you are presented with correspond toohello Gateway type and VPN type that you select.</span></span>

#### <a name="powershell"></a><span data-ttu-id="570f0-122">PowerShell</span><span class="sxs-lookup"><span data-stu-id="570f0-122">PowerShell</span></span>

<span data-ttu-id="570f0-123">hello 下列 PowerShell 範例會指定 hello `-GatewaySku` VpnGw1 為。</span><span class="sxs-lookup"><span data-stu-id="570f0-123">hello following PowerShell example specifies hello `-GatewaySku` as VpnGw1.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig -GatewaySku VpnGw1 `
-GatewayType Vpn -VpnType RouteBased
```

#### <span data-ttu-id="570f0-124"><a name="resize"></a>變更閘道 SKU (調整閘道 SKU 大小)</span><span class="sxs-lookup"><span data-stu-id="570f0-124"><a name="resize"></a>Change (resize) a gateway SKU</span></span>

<span data-ttu-id="570f0-125">如果您的閘道 SKU tooa 想 tooupgrade 功能更強大的 SKU，您可以使用 hello `Resize-AzureRmVirtualNetworkGateway` PowerShell cmdlet。</span><span class="sxs-lookup"><span data-stu-id="570f0-125">If you want tooupgrade your gateway SKU tooa more powerful SKU, you can use hello `Resize-AzureRmVirtualNetworkGateway` PowerShell cmdlet.</span></span> <span data-ttu-id="570f0-126">您也可以降級 hello 閘道 SKU 大小使用這個指令程式。</span><span class="sxs-lookup"><span data-stu-id="570f0-126">You can also downgrade hello gateway SKU size using this cmdlet.</span></span>

<span data-ttu-id="570f0-127">下列 PowerShell 範例 hello 顯示閘道 SKU 正在調整大小 tooVpnGw2。</span><span class="sxs-lookup"><span data-stu-id="570f0-127">hello following PowerShell example shows a gateway SKU being resized tooVpnGw2.</span></span>

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku VpnGw2
```

## <span data-ttu-id="570f0-128"><a name="connectiontype"></a>連線類型</span><span class="sxs-lookup"><span data-stu-id="570f0-128"><a name="connectiontype"></a>Connection types</span></span>

<span data-ttu-id="570f0-129">在 hello Resource Manager 部署模型，每個組態會需要特定虛擬網路閘道的連線類型。</span><span class="sxs-lookup"><span data-stu-id="570f0-129">In hello Resource Manager deployment model, each configuration requires a specific virtual network gateway connection type.</span></span> <span data-ttu-id="570f0-130">hello 可用的資源管理員 PowerShell 值`-ConnectionType`是：</span><span class="sxs-lookup"><span data-stu-id="570f0-130">hello available Resource Manager PowerShell values for `-ConnectionType` are:</span></span>

* <span data-ttu-id="570f0-131">IPsec</span><span class="sxs-lookup"><span data-stu-id="570f0-131">IPsec</span></span>
* <span data-ttu-id="570f0-132">Vnet2Vnet</span><span class="sxs-lookup"><span data-stu-id="570f0-132">Vnet2Vnet</span></span>
* <span data-ttu-id="570f0-133">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="570f0-133">ExpressRoute</span></span>
* <span data-ttu-id="570f0-134">VPNClient</span><span class="sxs-lookup"><span data-stu-id="570f0-134">VPNClient</span></span>

<span data-ttu-id="570f0-135">在 hello 下列 PowerShell 範例，我們會建立需要 hello 連接類型的 S2S 連線*IPsec*。</span><span class="sxs-lookup"><span data-stu-id="570f0-135">In hello following PowerShell example, we create a S2S connection that requires hello connection type *IPsec*.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name localtovon -ResourceGroupName testrg `
-Location 'West US' -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
-ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
```

## <span data-ttu-id="570f0-136"><a name="vpntype"></a>VPN 類型</span><span class="sxs-lookup"><span data-stu-id="570f0-136"><a name="vpntype"></a>VPN types</span></span>

<span data-ttu-id="570f0-137">當您建立 VPN 閘道設定的 hello 虛擬網路閘道時，您必須指定的 VPN 類型。</span><span class="sxs-lookup"><span data-stu-id="570f0-137">When you create hello virtual network gateway for a VPN gateway configuration, you must specify a VPN type.</span></span> <span data-ttu-id="570f0-138">hello 您選擇的 VPN 類型取決於 hello 連線拓撲的 toocreate。</span><span class="sxs-lookup"><span data-stu-id="570f0-138">hello VPN type that you choose depends on hello connection topology that you want toocreate.</span></span> <span data-ttu-id="570f0-139">例如，P2S 連線需要 RouteBased VPN 類型。</span><span class="sxs-lookup"><span data-stu-id="570f0-139">For example, a P2S connection requires a RouteBased VPN type.</span></span> <span data-ttu-id="570f0-140">VPN 類型而且可以根據您使用的 hello 硬體。</span><span class="sxs-lookup"><span data-stu-id="570f0-140">A VPN type can also depend on hello hardware that you are using.</span></span> <span data-ttu-id="570f0-141">S2S 組態需要 VPN 裝置。</span><span class="sxs-lookup"><span data-stu-id="570f0-141">S2S configurations require a VPN device.</span></span> <span data-ttu-id="570f0-142">有些 VPN 裝置僅支援特定 VPN 類型。</span><span class="sxs-lookup"><span data-stu-id="570f0-142">Some VPN devices only support a certain VPN type.</span></span>

<span data-ttu-id="570f0-143">hello 您所選取的 VPN 類型必須符合您想要 toocreate hello 解決方案的所有 hello 連線需求。</span><span class="sxs-lookup"><span data-stu-id="570f0-143">hello VPN type you select must satisfy all hello connection requirements for hello solution you want toocreate.</span></span> <span data-ttu-id="570f0-144">例如，如果您想 toocreate S2S VPN 閘道連線和 P2S VPN 閘道連線的 hello 相同虛擬網路，您會使用 VPN 類型*RouteBased*因為 P2S 需要 RouteBased VPN 類型。</span><span class="sxs-lookup"><span data-stu-id="570f0-144">For example, if you want toocreate a S2S VPN gateway connection and a P2S VPN gateway connection for hello same virtual network, you would use VPN type *RouteBased* because P2S requires a RouteBased VPN type.</span></span> <span data-ttu-id="570f0-145">您也需要 tooverify VPN 裝置支援 RouteBased VPN 連線。</span><span class="sxs-lookup"><span data-stu-id="570f0-145">You would also need tooverify that your VPN device supported a RouteBased VPN connection.</span></span> 

<span data-ttu-id="570f0-146">一旦建立虛擬網路閘道之後，您無法變更 hello VPN 類型。</span><span class="sxs-lookup"><span data-stu-id="570f0-146">Once a virtual network gateway has been created, you can't change hello VPN type.</span></span> <span data-ttu-id="570f0-147">您有 toodelete hello 虛擬網路閘道，並建立新的連線。</span><span class="sxs-lookup"><span data-stu-id="570f0-147">You have toodelete hello virtual network gateway and create a new one.</span></span> <span data-ttu-id="570f0-148">有兩種 VPN 類型：</span><span class="sxs-lookup"><span data-stu-id="570f0-148">There are two VPN types:</span></span>

[!INCLUDE [vpn-gateway-vpntype](../../includes/vpn-gateway-vpntype-include.md)]

<span data-ttu-id="570f0-149">hello 下列 PowerShell 範例會指定 hello`-VpnType`為*RouteBased*。</span><span class="sxs-lookup"><span data-stu-id="570f0-149">hello following PowerShell example specifies hello `-VpnType` as *RouteBased*.</span></span> <span data-ttu-id="570f0-150">當您建立閘道時，您必須確定該 hello-VpnType 是正確的組態。</span><span class="sxs-lookup"><span data-stu-id="570f0-150">When you are creating a gateway, you must make sure that hello -VpnType is correct for your configuration.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig `
-GatewayType Vpn -VpnType RouteBased
```

## <span data-ttu-id="570f0-151"><a name="requirements"></a>閘道需求</span><span class="sxs-lookup"><span data-stu-id="570f0-151"><a name="requirements"></a>Gateway requirements</span></span>

[!INCLUDE [vpn-gateway-table-requirements](../../includes/vpn-gateway-table-requirements-include.md)]

## <span data-ttu-id="570f0-152"><a name="gwsub"></a>閘道子網路</span><span class="sxs-lookup"><span data-stu-id="570f0-152"><a name="gwsub"></a>Gateway subnet</span></span>

<span data-ttu-id="570f0-153">建立 VPN 閘道之前，您必須先建立閘道子網路。</span><span class="sxs-lookup"><span data-stu-id="570f0-153">Before you create a VPN gateway, you must create a gateway subnet.</span></span> <span data-ttu-id="570f0-154">hello 閘道子網路包含 hello 的 IP 位址的 hello 虛擬網路閘道的 Vm 和服務使用。</span><span class="sxs-lookup"><span data-stu-id="570f0-154">hello gateway subnet contains hello IP addresses that hello virtual network gateway VMs and services use.</span></span> <span data-ttu-id="570f0-155">當您建立虛擬網路閘道時，閘道 Vm 已部署的 toohello 閘道子網路並且使用設定所需的 hello VPN 閘道設定。</span><span class="sxs-lookup"><span data-stu-id="570f0-155">When you create your virtual network gateway, gateway VMs are deployed toohello gateway subnet and configured with hello required VPN gateway settings.</span></span> <span data-ttu-id="570f0-156">您必須永遠不會部署任何項目 （例如，其他 Vm） else toohello 閘道子網路。</span><span class="sxs-lookup"><span data-stu-id="570f0-156">You must never deploy anything else (for example, additional VMs) toohello gateway subnet.</span></span> <span data-ttu-id="570f0-157">hello 閘道子網路必須命名為 'GatewaySubnet' toowork 正確。</span><span class="sxs-lookup"><span data-stu-id="570f0-157">hello gateway subnet must be named 'GatewaySubnet' toowork properly.</span></span> <span data-ttu-id="570f0-158">命名 hello 閘道子網路 'GatewaySubnet' 可讓 Azure 知道這是 hello 子網路 toodeploy hello 虛擬網路閘道的 Vm 和服務。</span><span class="sxs-lookup"><span data-stu-id="570f0-158">Naming hello gateway subnet 'GatewaySubnet' lets Azure know that this is hello subnet toodeploy hello virtual network gateway VMs and services to.</span></span>

<span data-ttu-id="570f0-159">當您建立 hello 閘道子網路時，您可以指定包含 hello hello 子網路的 IP 位址數目。</span><span class="sxs-lookup"><span data-stu-id="570f0-159">When you create hello gateway subnet, you specify hello number of IP addresses that hello subnet contains.</span></span> <span data-ttu-id="570f0-160">hello 閘道子網路中的 hello IP 位址是配置的 toohello 閘道 Vm，閘道服務。</span><span class="sxs-lookup"><span data-stu-id="570f0-160">hello IP addresses in hello gateway subnet are allocated toohello gateway VMs and gateway services.</span></span> <span data-ttu-id="570f0-161">有些組態需要的 IP 位址比其他組態多。</span><span class="sxs-lookup"><span data-stu-id="570f0-161">Some configurations require more IP addresses than others.</span></span> <span data-ttu-id="570f0-162">查看 hello 設定您想 toocreate，並確認您想要 toocreate hello 閘道子網路會符合這些需求的 hello 指示。</span><span class="sxs-lookup"><span data-stu-id="570f0-162">Look at hello instructions for hello configuration that you want toocreate and verify that hello gateway subnet you want toocreate meets those requirements.</span></span> <span data-ttu-id="570f0-163">此外，您可能想 toomake 確定您的閘道子網路包含足夠的 IP 位址 tooaccommodate 可能未來其他設定。</span><span class="sxs-lookup"><span data-stu-id="570f0-163">Additionally, you may want toomake sure your gateway subnet contains enough IP addresses tooaccommodate possible future additional configurations.</span></span> <span data-ttu-id="570f0-164">雖然您可以建立像 /29 這麼小的閘道子網路，但建議您建立 /28 或更大 (/28、/27、/26 等) 的閘道子網路。</span><span class="sxs-lookup"><span data-stu-id="570f0-164">While you can create a gateway subnet as small as /29, we recommend that you create a gateway subnet of /28 or larger (/28, /27, /26 etc.).</span></span> <span data-ttu-id="570f0-165">這樣一來，如果您將功能加入在 hello 未來，您將不會有 tootear 閘道，然後刪除並重新建立 hello 閘道子網路 tooallow 更多 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="570f0-165">That way, if you add functionality in hello future, you won't have tootear your gateway, then delete and recreate hello gateway subnet tooallow for more IP addresses.</span></span>

<span data-ttu-id="570f0-166">hello 下列資源管理員 PowerShell 範例會示範名為 GatewaySubnet 閘道子網路。</span><span class="sxs-lookup"><span data-stu-id="570f0-166">hello following Resource Manager PowerShell example shows a gateway subnet named GatewaySubnet.</span></span> <span data-ttu-id="570f0-167">您可以看到 hello CIDR 標記法指定 /27，即允許足夠的 IP 位址，對於多數組態目前存在的。</span><span class="sxs-lookup"><span data-stu-id="570f0-167">You can see hello CIDR notation specifies a /27, which allows for enough IP addresses for most configurations that currently exist.</span></span>

```powershell
Add-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.0.3.0/27
```

[!INCLUDE [vpn-gateway-no-nsg](../../includes/vpn-gateway-no-nsg-include.md)]

## <span data-ttu-id="570f0-168"><a name="lng"></a>區域網路閘道</span><span class="sxs-lookup"><span data-stu-id="570f0-168"><a name="lng"></a>Local network gateways</span></span>

<span data-ttu-id="570f0-169">在建立 VPN 閘道設定時，hello 區域網路閘道通常代表您在內部部署位置。</span><span class="sxs-lookup"><span data-stu-id="570f0-169">When creating a VPN gateway configuration, hello local network gateway often represents your on-premises location.</span></span> <span data-ttu-id="570f0-170">在 hello 傳統部署模型中，hello 區域網路閘道已參考的 tooas 本機站台。</span><span class="sxs-lookup"><span data-stu-id="570f0-170">In hello classic deployment model, hello local network gateway was referred tooas a Local Site.</span></span> 

<span data-ttu-id="570f0-171">您指定 hello 區域網路閘道的名稱、 hello hello 在內部部署 VPN 裝置，公用 IP 位址，並指定 hello 都位於 hello 在內部部署位置的位址首碼。</span><span class="sxs-lookup"><span data-stu-id="570f0-171">You give hello local network gateway a name, hello public IP address of hello on-premises VPN device, and specify hello address prefixes that are located on hello on-premises location.</span></span> <span data-ttu-id="570f0-172">Azure 會查看網路流量的 hello 目的地位址前置詞、 參照 hello 設定您所指定區域網路閘道，並據以路由傳送封包。</span><span class="sxs-lookup"><span data-stu-id="570f0-172">Azure looks at hello destination address prefixes for network traffic, consults hello configuration that you have specified for your local network gateway, and routes packets accordingly.</span></span> <span data-ttu-id="570f0-173">您也可以針對使用 VPN 閘道連線的 VNet 對 VNet 組態指定區域網路閘道。</span><span class="sxs-lookup"><span data-stu-id="570f0-173">You also specify local network gateways for VNet-to-VNet configurations that use a VPN gateway connection.</span></span>

<span data-ttu-id="570f0-174">hello 下列 PowerShell 範例會建立新的區域網路閘道：</span><span class="sxs-lookup"><span data-stu-id="570f0-174">hello following PowerShell example creates a new local network gateway:</span></span>

```powershell
New-AzureRmLocalNetworkGateway -Name LocalSite -ResourceGroupName testrg `
-Location 'West US' -GatewayIpAddress '23.99.221.164' -AddressPrefix '10.5.51.0/24'
```

<span data-ttu-id="570f0-175">有時候您需要 toomodify hello 區域網路閘道設定。</span><span class="sxs-lookup"><span data-stu-id="570f0-175">Sometimes you need toomodify hello local network gateway settings.</span></span> <span data-ttu-id="570f0-176">例如，當您加入或修改 hello 位址範圍，或如果 hello hello VPN 裝置 IP 位址變更。</span><span class="sxs-lookup"><span data-stu-id="570f0-176">For example, when you add or modify hello address range, or if hello IP address of hello VPN device changes.</span></span> <span data-ttu-id="570f0-177">傳統的 vnet，您可以變更這些設定 hello hello 區域網路 頁面上的傳統入口網站中。</span><span class="sxs-lookup"><span data-stu-id="570f0-177">For a classic VNet, you can change these settings in hello classic portal on hello Local Networks page.</span></span> <span data-ttu-id="570f0-178">針對 Resource Manager，請參閱 [使用 PowerShell 修改區域網路閘道設定](vpn-gateway-modify-local-network-gateway.md)。</span><span class="sxs-lookup"><span data-stu-id="570f0-178">For Resource Manager, see [Modify local network gateway settings using PowerShell](vpn-gateway-modify-local-network-gateway.md).</span></span>

## <span data-ttu-id="570f0-179"><a name="resources"></a>REST API 和 PowerShell Cmdlet</span><span class="sxs-lookup"><span data-stu-id="570f0-179"><a name="resources"></a>REST APIs and PowerShell cmdlets</span></span>

<span data-ttu-id="570f0-180">如需其他技術資源與特定語法需求時使用 REST Api、 PowerShell cmdlet 或 Azure CLI VPN 閘道的設定，請參閱 hello 下列頁面：</span><span class="sxs-lookup"><span data-stu-id="570f0-180">For additional technical resources and specific syntax requirements when using REST APIs, PowerShell cmdlets, or Azure CLI for VPN Gateway configurations, see hello following pages:</span></span>

| <span data-ttu-id="570f0-181">**傳統**</span><span class="sxs-lookup"><span data-stu-id="570f0-181">**Classic**</span></span> | <span data-ttu-id="570f0-182">**資源管理員**</span><span class="sxs-lookup"><span data-stu-id="570f0-182">**Resource Manager**</span></span> |
| --- | --- |
| [<span data-ttu-id="570f0-183">PowerShell</span><span class="sxs-lookup"><span data-stu-id="570f0-183">PowerShell</span></span>](/powershell/module/azure#networking) |[<span data-ttu-id="570f0-184">PowerShell</span><span class="sxs-lookup"><span data-stu-id="570f0-184">PowerShell</span></span>](/powershell/module/azurerm.network#vpn) |
| [<span data-ttu-id="570f0-185">REST API</span><span class="sxs-lookup"><span data-stu-id="570f0-185">REST API</span></span>](https://msdn.microsoft.com/library/jj154113) |[<span data-ttu-id="570f0-186">REST API</span><span class="sxs-lookup"><span data-stu-id="570f0-186">REST API</span></span>](/rest/api/network/virtualnetworkgateways) |
| <span data-ttu-id="570f0-187">不支援</span><span class="sxs-lookup"><span data-stu-id="570f0-187">Not supported</span></span> | [<span data-ttu-id="570f0-188">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="570f0-188">Azure CLI</span></span>](/cli/azure/network/vnet-gateway)|

## <a name="next-steps"></a><span data-ttu-id="570f0-189">後續步驟</span><span class="sxs-lookup"><span data-stu-id="570f0-189">Next steps</span></span>

<span data-ttu-id="570f0-190">如需有關可用連線組態的詳細資訊，請參閱[關於 VPN 閘道](vpn-gateway-about-vpngateways.md)。</span><span class="sxs-lookup"><span data-stu-id="570f0-190">For more information about available connection configurations, see [About VPN Gateway](vpn-gateway-about-vpngateways.md).</span></span>