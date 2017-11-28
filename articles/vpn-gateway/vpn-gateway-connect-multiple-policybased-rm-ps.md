---
title: "連接 Azure VPN 閘道 toomultiple 內部以原則為基礎的 VPN 裝置： Azure 資源管理員： PowerShell |Microsoft 文件"
description: "這篇文章會引導您設定 Azure 路由式 VPN 閘道 toomultiple 原則式 VPN 裝置使用 Azure 資源管理員和 PowerShell。"
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/27/2017
ms.author: yushwang
ms.openlocfilehash: 866c78d96305207106a66cc3300c355e4b6bfbb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-azure-vpn-gateways-toomultiple-on-premises-policy-based-vpn-devices-using-powershell"></a><span data-ttu-id="ecf97-103">連接 Azure VPN 閘道 toomultiple 內部以原則為基礎的 VPN 裝置使用 PowerShell</span><span class="sxs-lookup"><span data-stu-id="ecf97-103">Connect Azure VPN gateways toomultiple on-premises policy-based VPN devices using PowerShell</span></span>

<span data-ttu-id="ecf97-104">這篇文章可協助您設定 Azure 路由式 VPN 閘道 tooconnect toomultiple 在內部部署原則式 VPN 裝置運用 S2S VPN 連線自訂 IPsec/IKE 原則。</span><span class="sxs-lookup"><span data-stu-id="ecf97-104">This article helps you configure an Azure route-based VPN gateway tooconnect toomultiple on-premises policy-based VPN devices leveraging custom IPsec/IKE policies on S2S VPN connections.</span></span>

## <a name="about-policy-based-and-route-based-vpn-gateways"></a><span data-ttu-id="ecf97-105">關於以原則為基礎的 VPN 閘道和以路由為基礎的 VPN 閘道</span><span class="sxs-lookup"><span data-stu-id="ecf97-105">About policy-based and route-based VPN gateways</span></span>

<span data-ttu-id="ecf97-106">原則-*與*路由式 VPN 裝置的 hello IPsec 流量選取器的連接上設定的方式不同：</span><span class="sxs-lookup"><span data-stu-id="ecf97-106">Policy- *vs.* route-based VPN devices differ in how hello IPsec traffic selectors are set on a connection:</span></span>

* <span data-ttu-id="ecf97-107">**以原則為基礎**VPN 裝置使用的前置詞，從這兩種方式的流量會加密/解密透過 IPsec 通道的網路 toodefine hello 組合。</span><span class="sxs-lookup"><span data-stu-id="ecf97-107">**Policy-based** VPN devices use hello combinations of prefixes from both networks toodefine how traffic is encrypted/decrypted through IPsec tunnels.</span></span> <span data-ttu-id="ecf97-108">它通常內建在執行封包篩選的防火牆裝置上。</span><span class="sxs-lookup"><span data-stu-id="ecf97-108">It is typically built on firewall devices that perform packet filtering.</span></span> <span data-ttu-id="ecf97-109">IPsec 通道加密和解密會新增 toohello 封包篩選處理引擎。</span><span class="sxs-lookup"><span data-stu-id="ecf97-109">IPsec tunnel encryption and decryption are added toohello packet filtering and processing engine.</span></span>
* <span data-ttu-id="ecf97-110">**路由式**VPN 裝置使用任何-any （萬用字元） 流量的選取器，可讓路由轉送/資料表和資料流導向 toodifferent IPsec 通道。</span><span class="sxs-lookup"><span data-stu-id="ecf97-110">**Route-based** VPN devices use any-to-any (wildcard) traffic selectors, and let routing/forwarding tables direct traffic toodifferent IPsec tunnels.</span></span> <span data-ttu-id="ecf97-111">它通常內建在路由器平台上，其中，每個 IPsec 通道都會建模為網路介面或 VTI (虛擬通道介面)。</span><span class="sxs-lookup"><span data-stu-id="ecf97-111">It is typically built on router platforms where each IPsec tunnel is modeled as a network interface or VTI (virtual tunnel interface).</span></span>

<span data-ttu-id="ecf97-112">hello 圖反白顯示 hello 兩個模型：</span><span class="sxs-lookup"><span data-stu-id="ecf97-112">hello following diagrams highlight hello two models:</span></span>

### <a name="policy-based-vpn-example"></a><span data-ttu-id="ecf97-113">以原則為基礎的 VPN 範例</span><span class="sxs-lookup"><span data-stu-id="ecf97-113">Policy-based VPN example</span></span>
![以原則為基礎](./media/vpn-gateway-connect-multiple-policybased-rm-ps/policybasedmultisite.png)

### <a name="route-based-vpn-example"></a><span data-ttu-id="ecf97-115">以路由為基礎的 VPN 範例</span><span class="sxs-lookup"><span data-stu-id="ecf97-115">Route-based VPN example</span></span>
![以路由為基礎](./media/vpn-gateway-connect-multiple-policybased-rm-ps/routebasedmultisite.png)

### <a name="azure-support-for-policy-based-vpn"></a><span data-ttu-id="ecf97-117">以原則為基礎的 VPN 的 Azure 支援</span><span class="sxs-lookup"><span data-stu-id="ecf97-117">Azure support for policy-based VPN</span></span>
<span data-ttu-id="ecf97-118">Azure 目前支援兩種 VPN 閘道模式：以路由為基礎的 VPN 閘道和以原則為基礎的 VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="ecf97-118">Currently, Azure supports both modes of VPN gateways: route-based VPN gateways and policy-based VPN gateways.</span></span> <span data-ttu-id="ecf97-119">它們內建在不同內部平台上，因而導致不同的規格：</span><span class="sxs-lookup"><span data-stu-id="ecf97-119">They are built on different internal platforms, which result in different specifications:</span></span>

|                          | <span data-ttu-id="ecf97-120">**PolicyBased VPN 閘道**</span><span class="sxs-lookup"><span data-stu-id="ecf97-120">**PolicyBased VPN Gateway**</span></span> | <span data-ttu-id="ecf97-121">**RouteBased VPN 閘道**</span><span class="sxs-lookup"><span data-stu-id="ecf97-121">**RouteBased VPN Gateway**</span></span>               |
| ---                      | ---                         | ---                                      |
| <span data-ttu-id="ecf97-122">**Azure 閘道 SKU**</span><span class="sxs-lookup"><span data-stu-id="ecf97-122">**Azure Gateway SKU**</span></span>    | <span data-ttu-id="ecf97-123">基本</span><span class="sxs-lookup"><span data-stu-id="ecf97-123">Basic</span></span>                       | <span data-ttu-id="ecf97-124">Basic、Standard、HighPerformance</span><span class="sxs-lookup"><span data-stu-id="ecf97-124">Basic, Standard, HighPerformance</span></span>         |
| <span data-ttu-id="ecf97-125">**IKE 版本**</span><span class="sxs-lookup"><span data-stu-id="ecf97-125">**IKE version**</span></span>          | <span data-ttu-id="ecf97-126">IKEv1</span><span class="sxs-lookup"><span data-stu-id="ecf97-126">IKEv1</span></span>                       | <span data-ttu-id="ecf97-127">IKEv2</span><span class="sxs-lookup"><span data-stu-id="ecf97-127">IKEv2</span></span>                                    |
| <span data-ttu-id="ecf97-128">**最大S2S 連線**</span><span class="sxs-lookup"><span data-stu-id="ecf97-128">**Max. S2S connections**</span></span> | <span data-ttu-id="ecf97-129">**1**</span><span class="sxs-lookup"><span data-stu-id="ecf97-129">**1**</span></span>                       | <span data-ttu-id="ecf97-130">基本/標準：10</span><span class="sxs-lookup"><span data-stu-id="ecf97-130">Basic/Standard: 10</span></span><br> <span data-ttu-id="ecf97-131">高效能：30</span><span class="sxs-lookup"><span data-stu-id="ecf97-131">HighPerformance: 30</span></span> |
|                          |                             |                                          |

<span data-ttu-id="ecf97-132">Hello 自訂 IPsec/IKE 原則，您現在可以設定 Azure 路由式 VPN 閘道 toouse 前置詞為基礎的傳輸選取器選項"**PolicyBasedTrafficSelectors**"，tooconnect tooon 內部以原則為基礎的 VPN 裝置。</span><span class="sxs-lookup"><span data-stu-id="ecf97-132">With hello custom IPsec/IKE policy, you can now configure Azure route-based VPN gateways toouse prefix-based traffic selectors with option "**PolicyBasedTrafficSelectors**", tooconnect tooon-premises policy-based VPN devices.</span></span> <span data-ttu-id="ecf97-133">這項功能可讓您從一個 Azure 虛擬網路的 tooconnect 和 VPN 閘道 toomultiple 內部原則式 VPN/防火牆裝置，從 hello 目前 Azure 原則式 VPN 閘道移除 hello 單一連線限制。</span><span class="sxs-lookup"><span data-stu-id="ecf97-133">This capability allows you tooconnect from an Azure virtual network and VPN gateway toomultiple on-premises policy-based VPN/firewall devices, removing hello single connection limit from hello current Azure policy-based VPN gateways.</span></span>

> [!IMPORTANT]
> 1. <span data-ttu-id="ecf97-134">tooenable 您在內部以原則為基礎的 VPN 裝置必須支援這種連線能力， **IKEv2** tooconnect toohello Azure 路由式 VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="ecf97-134">tooenable this connectivity, your on-premises policy-based VPN devices must support **IKEv2** tooconnect toohello Azure route-based VPN gateways.</span></span> <span data-ttu-id="ecf97-135">確認您的 VPN 裝置規格。</span><span class="sxs-lookup"><span data-stu-id="ecf97-135">Check your VPN device specifications.</span></span>
> 2. <span data-ttu-id="ecf97-136">使用這項機制透過以原則為基礎的 VPN 裝置連接的 hello 在內部部署網路只能連接 toohello Azure 虛擬網路。**它們無法傳輸 tooother 在內部部署網路，或透過虛擬網路 hello 相同 Azure VPN 閘道**。</span><span class="sxs-lookup"><span data-stu-id="ecf97-136">hello on-premises networks connecting through policy-based VPN devices with this mechanism can only connect toohello Azure virtual network; **they cannot transit tooother on-premises networks or virtual networks via hello same Azure VPN gateway**.</span></span>
> 3. <span data-ttu-id="ecf97-137">hello 組態選項是 hello 自訂 IPsec/IKE 連接原則的一部分。</span><span class="sxs-lookup"><span data-stu-id="ecf97-137">hello configuration option is part of hello custom IPsec/IKE connection policy.</span></span> <span data-ttu-id="ecf97-138">如果您啟用 hello 以原則為基礎的傳輸選取器選項，您必須指定 hello 完整的原則 （IPsec/IKE 加密及完整性演算法、 金鑰長度和 SA 存留時間）。</span><span class="sxs-lookup"><span data-stu-id="ecf97-138">If you enable hello policy-based traffic selector option, you must specify hello complete policy (IPsec/IKE encryption and integrity algorithms, key strengths, and SA lifetimes).</span></span>

<span data-ttu-id="ecf97-139">hello 下列圖表顯示為何透過 Azure VPN 閘道的傳輸路由不能使用 hello 以原則為基礎的選項：</span><span class="sxs-lookup"><span data-stu-id="ecf97-139">hello following diagram shows why transit routing via Azure VPN gateway doesn't work with hello policy-based option:</span></span>

![以原則為基礎的傳輸](./media/vpn-gateway-connect-multiple-policybased-rm-ps/policybasedtransit.png)

<span data-ttu-id="ecf97-141">Hello 圖表所示，hello Azure VPN 閘道有流量從 hello 虛擬網路 tooeach hello 在內部部署網路首碼，但不 hello 跨連接前置詞的選取器。</span><span class="sxs-lookup"><span data-stu-id="ecf97-141">As shown in hello diagram, hello Azure VPN gateway has traffic selectors from hello virtual network tooeach of hello on-premises network prefixes, but not hello cross-connection prefixes.</span></span> <span data-ttu-id="ecf97-142">例如，在內部部署站台 2，3，站台與站台 4 可以每個分別通訊 tooVNet1，但無法連接透過 hello Azure VPN 閘道 tooeach 其他。</span><span class="sxs-lookup"><span data-stu-id="ecf97-142">For example, on-premises site 2, site 3, and site 4 can each communicate tooVNet1 respectively, but cannot connect via hello Azure VPN gateway tooeach other.</span></span> <span data-ttu-id="ecf97-143">hello 圖表會顯示 hello 跨連接都無法使用此設定下 hello Azure VPN 閘道的流量選取器。</span><span class="sxs-lookup"><span data-stu-id="ecf97-143">hello diagram shows hello cross-connect traffic selectors that are not available in hello Azure VPN gateway under this configuration.</span></span>

## <a name="configure-policy-based-traffic-selectors-on-a-connection"></a><span data-ttu-id="ecf97-144">在連線上設定以原則為基礎的流量選取器</span><span class="sxs-lookup"><span data-stu-id="ecf97-144">Configure policy-based traffic selectors on a connection</span></span>

<span data-ttu-id="ecf97-145">hello 中這篇文章依照指示 hello 相同範例中所述[設定 IPsec/IKE S2S 或 VNet 對 VNet 連線原則](vpn-gateway-ipsecikepolicy-rm-powershell.md)tooestablish S2S VPN 連線。</span><span class="sxs-lookup"><span data-stu-id="ecf97-145">hello instructions in this article follow hello same example as described in [Configure IPsec/IKE policy for S2S or VNet-to-VNet connections](vpn-gateway-ipsecikepolicy-rm-powershell.md) tooestablish a S2S VPN connection.</span></span> <span data-ttu-id="ecf97-146">Hello 下列圖表所示：</span><span class="sxs-lookup"><span data-stu-id="ecf97-146">This is shown in hello following diagram:</span></span>

![s2s-policy](./media/vpn-gateway-connect-multiple-policybased-rm-ps/s2spolicypb.png)

<span data-ttu-id="ecf97-148">hello 工作流程 tooenable 這種連線能力：</span><span class="sxs-lookup"><span data-stu-id="ecf97-148">hello workflow tooenable this connectivity:</span></span>
1. <span data-ttu-id="ecf97-149">建立 hello 虛擬網路、 VPN 閘道和跨單位連線的區域網路閘道</span><span class="sxs-lookup"><span data-stu-id="ecf97-149">Create hello virtual network, VPN gateway, and local network gateway for your cross-premises connection</span></span>
2. <span data-ttu-id="ecf97-150">建立 IPsec/IKE 原則</span><span class="sxs-lookup"><span data-stu-id="ecf97-150">Create an IPsec/IKE policy</span></span>
3. <span data-ttu-id="ecf97-151">當您建立 S2S 或 VNet 對 VNet 連線，套用 hello 原則和**啟用 hello 以原則為基礎的傳輸選取器**hello 連接上</span><span class="sxs-lookup"><span data-stu-id="ecf97-151">Apply hello policy when you create a S2S or VNet-to-VNet connection, and **enable hello policy-based traffic selectors** on hello connection</span></span>
4. <span data-ttu-id="ecf97-152">如果已經建立 hello 連線，您可以套用或更新 hello 原則 tooan 現有連線</span><span class="sxs-lookup"><span data-stu-id="ecf97-152">If hello connection is already created, you can apply or update hello policy tooan existing connection</span></span>

## <a name="enable-policy-based-traffic-selectors-on-a-connection"></a><span data-ttu-id="ecf97-153">在連線上啟用以原則為基礎的流量選取器</span><span class="sxs-lookup"><span data-stu-id="ecf97-153">Enable policy-based traffic selectors on a connection</span></span>

<span data-ttu-id="ecf97-154">請確定您已完成[hello 設定 IPsec/IKE 原則文件的組件 3](vpn-gateway-ipsecikepolicy-rm-powershell.md)對此區段。</span><span class="sxs-lookup"><span data-stu-id="ecf97-154">Make sure you have completed [Part 3 of hello Configure IPsec/IKE policy article](vpn-gateway-ipsecikepolicy-rm-powershell.md) for this section.</span></span> <span data-ttu-id="ecf97-155">下列範例會使用 hello hello 相同的參數和步驟：</span><span class="sxs-lookup"><span data-stu-id="ecf97-155">hello following example uses hello same parameters and steps:</span></span>

### <a name="step-1---create-hello-virtual-network-vpn-gateway-and-local-network-gateway"></a><span data-ttu-id="ecf97-156">步驟 1-建立 hello 虛擬網路、 VPN 閘道與區域網路閘道</span><span class="sxs-lookup"><span data-stu-id="ecf97-156">Step 1 - Create hello virtual network, VPN gateway, and local network gateway</span></span>

#### <a name="1-declare-your-variables--connect-tooyour-subscription"></a><span data-ttu-id="ecf97-157">1.宣告變數和連接 tooyour 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="ecf97-157">1. Declare your variables & connect tooyour subscription</span></span>
<span data-ttu-id="ecf97-158">對於此練習，我們一開始先宣告我們的變數。</span><span class="sxs-lookup"><span data-stu-id="ecf97-158">For this exercise, we start by declaring our variables.</span></span> <span data-ttu-id="ecf97-159">設定用於生產環境時，請以您自己是確定 tooreplace hello 值。</span><span class="sxs-lookup"><span data-stu-id="ecf97-159">Be sure tooreplace hello values with your own when configuring for production.</span></span>

```powershell
$Sub1          = "<YourSubscriptionName>"
$RG1           = "TestPolicyRG1"
$Location1     = "East US 2"
$VNetName1     = "TestVNet1"
$FESubName1    = "FrontEnd"
$BESubName1    = "Backend"
$GWSubName1    = "GatewaySubnet"
$VNetPrefix11  = "10.11.0.0/16"
$VNetPrefix12  = "10.12.0.0/16"
$FESubPrefix1  = "10.11.0.0/24"
$BESubPrefix1  = "10.12.0.0/24"
$GWSubPrefix1  = "10.12.255.0/27"
$DNS1          = "8.8.8.8"
$GWName1       = "VNet1GW"
$GW1IPName1    = "VNet1GWIP1"
$GW1IPconf1    = "gw1ipconf1"
$Connection16  = "VNet1toSite6"

$LNGName6      = "Site6"
$LNGPrefix61   = "10.61.0.0/16"
$LNGPrefix62   = "10.62.0.0/16"
$LNGIP6        = "131.107.72.22"
```
<span data-ttu-id="ecf97-160">toouse hello 資源管理員 cmdlet，請確定切換 tooPowerShell 模式。</span><span class="sxs-lookup"><span data-stu-id="ecf97-160">toouse hello Resource Manager cmdlets, make sure you switch tooPowerShell mode.</span></span> <span data-ttu-id="ecf97-161">如需詳細資訊，請參閱 [搭配使用 Windows PowerShell 與 Resource Manager](../powershell-azure-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="ecf97-161">For more information, see [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="ecf97-162">開啟 PowerShell 主控台並連接 tooyour 帳戶。</span><span class="sxs-lookup"><span data-stu-id="ecf97-162">Open your PowerShell console and connect tooyour account.</span></span> <span data-ttu-id="ecf97-163">使用下列範例 toohelp 您連接的 hello:</span><span class="sxs-lookup"><span data-stu-id="ecf97-163">Use hello following sample toohelp you connect:</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="2-create-hello-virtual-network-vpn-gateway-and-local-network-gateway"></a><span data-ttu-id="ecf97-164">2.建立 hello 虛擬網路、 VPN 閘道與區域網路閘道</span><span class="sxs-lookup"><span data-stu-id="ecf97-164">2. Create hello virtual network, VPN gateway, and local network gateway</span></span>
<span data-ttu-id="ecf97-165">下列範例中的 hello 建立 hello 虛擬網路，TestVNet1 三個的子網路與 hello VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="ecf97-165">hello following example creates hello virtual network, TestVNet1 with three subnets, and hello VPN gateway.</span></span> <span data-ttu-id="ecf97-166">替代值時，務必一律將您的閘道子網路特定命名為 GatewaySubnet。</span><span class="sxs-lookup"><span data-stu-id="ecf97-166">When substituting values, it's important that you always name your gateway subnet specifically 'GatewaySubnet'.</span></span> <span data-ttu-id="ecf97-167">如果您將其命名為其他名稱，閘道建立會失敗。</span><span class="sxs-lookup"><span data-stu-id="ecf97-167">If you name it something else, your gateway creation fails.</span></span>

```powershell
$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1
$besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1

$gw1pip1    = New-AzureRmPublicIpAddress -Name $GW1IPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic
$vnet1      = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1    = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gw1ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW1IPconf1 -Subnet $subnet1 -PublicIpAddress $gw1pip1

New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gw1ipconf1 -GatewayType Vpn -VpnType RouteBased -GatewaySku HighPerformance

New-AzureRmLocalNetworkGateway -Name $LNGName6 -ResourceGroupName $RG1 -Location $Location1 -GatewayIpAddress $LNGIP6 -AddressPrefix $LNGPrefix61,$LNGPrefix62
```

### <a name="step-2---create-a-s2s-vpn-connection-with-an-ipsecike-policy"></a><span data-ttu-id="ecf97-168">步驟 2 - 使用 IPsec/IKE 原則建立 S2S VPN 連線</span><span class="sxs-lookup"><span data-stu-id="ecf97-168">Step 2 - Create a S2S VPN connection with an IPsec/IKE policy</span></span>

#### <a name="1-create-an-ipsecike-policy"></a><span data-ttu-id="ecf97-169">1.建立 IPsec/IKE 原則</span><span class="sxs-lookup"><span data-stu-id="ecf97-169">1. Create an IPsec/IKE policy</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ecf97-170">您需要 toocreate 順序 tooenable"UsePolicyBasedTrafficSelectors"hello 連線選項中的 IPsec/IKE 原則。</span><span class="sxs-lookup"><span data-stu-id="ecf97-170">You need toocreate an IPsec/IKE policy in order tooenable "UsePolicyBasedTrafficSelectors" option on hello connection.</span></span>

<span data-ttu-id="ecf97-171">hello 下列範例會建立一個 IPsec/IKE 原則使用這些演算法和參數：</span><span class="sxs-lookup"><span data-stu-id="ecf97-171">hello following example creates an IPsec/IKE policy with these algorithms and parameters:</span></span>
* <span data-ttu-id="ecf97-172">IKEv2：AES256、SHA384、DHGroup24</span><span class="sxs-lookup"><span data-stu-id="ecf97-172">IKEv2: AES256, SHA384, DHGroup24</span></span>
* <span data-ttu-id="ecf97-173">IPsec：AES256、SHA256、PFS24、SA 存留期 3600 秒和 2048KB</span><span class="sxs-lookup"><span data-stu-id="ecf97-173">IPsec: AES256, SHA256, PFS24, SA Lifetime 3600 seconds & 2048KB</span></span>

```powershell
$ipsecpolicy6 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption AES256 -IpsecIntegrity SHA256 -PfsGroup PFS24 -SALifeTimeSeconds 3600 -SADataSizeKilobytes 2048
```

#### <a name="2-create-hello-s2s-vpn-connection-with-policy-based-traffic-selectors-and-ipsecike-policy"></a><span data-ttu-id="ecf97-174">2.使用以原則為基礎的傳輸選取器與 IPsec/IKE 原則建立 hello S2S VPN 連線</span><span class="sxs-lookup"><span data-stu-id="ecf97-174">2. Create hello S2S VPN connection with policy-based traffic selectors and IPsec/IKE policy</span></span>
<span data-ttu-id="ecf97-175">建立 S2S VPN 連線並套用 hello hello 先前步驟中建立的 IPsec/IKE 原則。</span><span class="sxs-lookup"><span data-stu-id="ecf97-175">Create an S2S VPN connection and apply hello IPsec/IKE policy created in hello previous step.</span></span> <span data-ttu-id="ecf97-176">請留意 hello 額外的參數"-UsePolicyBasedTrafficSelectors $True 」 可讓以原則為基礎的流量 hello 連接上的選取器。</span><span class="sxs-lookup"><span data-stu-id="ecf97-176">Be aware of hello additional parameter "-UsePolicyBasedTrafficSelectors $True"  which enables policy-based traffic selectors on hello connection.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng6 = Get-AzureRmLocalNetworkGateway  -Name $LNGName6 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng6 -Location $Location1 -ConnectionType IPsec -UsePolicyBasedTrafficSelectors $True -IpsecPolicies $ipsecpolicy6 -SharedKey 'AzureA1b2C3'
```

<span data-ttu-id="ecf97-177">完成 hello 步驟之後，將會使用 hello IPsec/IKE 原則定義，hello S2S VPN 連線，並將其啟用以原則為基礎的流量 hello 連接上的選取器中。</span><span class="sxs-lookup"><span data-stu-id="ecf97-177">After completing hello steps, hello S2S VPN connection will use hello IPsec/IKE policy defined, and enable policy-based traffic selectors on hello connection.</span></span> <span data-ttu-id="ecf97-178">您可以重複相同步驟 tooadd 多個連線 tooadditional 內部以原則為基礎的 VPN 裝置從 hello hello 相同 Azure VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="ecf97-178">You can repeat hello same steps tooadd more connections tooadditional on-premises policy-based VPN devices from hello same Azure VPN gateway.</span></span>

## <a name="update-policy-based-traffic-selectors-for-a-connection"></a><span data-ttu-id="ecf97-179">更新連線的以原則為基礎的流量選取器</span><span class="sxs-lookup"><span data-stu-id="ecf97-179">Update policy-based traffic selectors for a connection</span></span>
<span data-ttu-id="ecf97-180">hello 最後一節顯示如何 tooupdate hello 以原則為基礎的傳輸選取器選項現有 S2S VPN 連線。</span><span class="sxs-lookup"><span data-stu-id="ecf97-180">hello last section shows you how tooupdate hello policy-based traffic selectors option for an existing  S2S VPN connection.</span></span>

### <a name="1-get-hello-connection"></a><span data-ttu-id="ecf97-181">1.取得 hello 連線</span><span class="sxs-lookup"><span data-stu-id="ecf97-181">1. Get hello connection</span></span>
<span data-ttu-id="ecf97-182">收到 hello 連接資源。</span><span class="sxs-lookup"><span data-stu-id="ecf97-182">Get hello connection resource.</span></span>

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1
```

### <a name="2-check-hello-policy-based-traffic-selectors-option"></a><span data-ttu-id="ecf97-183">2.核取 hello 以原則為基礎的傳輸選取器選項</span><span class="sxs-lookup"><span data-stu-id="ecf97-183">2. Check hello policy-based traffic selectors option</span></span>
<span data-ttu-id="ecf97-184">hello 下列一行顯示 hello 以原則為基礎的傳輸選取器是否會用於 hello 連接：</span><span class="sxs-lookup"><span data-stu-id="ecf97-184">hello following line shows whether hello policy-based traffic selectors are used for hello connection:</span></span>

```powershell
$connection6.UsePolicyBasedTrafficSelectors
```

<span data-ttu-id="ecf97-185">如果 hello 一行傳回的"**True**"，然後以原則為基礎的傳輸選取器會在 hello 連線上設定; 否則會傳回"**False**。 」</span><span class="sxs-lookup"><span data-stu-id="ecf97-185">If hello line returns "**True**", then policy-based traffic selectors are configured on hello connection; otherwise it returns "**False**."</span></span>

### <a name="3-update-hello-policy-based-traffic-selectors-on-a-connection"></a><span data-ttu-id="ecf97-186">3.更新的連接上的 hello 以原則為基礎的傳輸選取器</span><span class="sxs-lookup"><span data-stu-id="ecf97-186">3. Update hello policy-based traffic selectors on a connection</span></span>
<span data-ttu-id="ecf97-187">一旦您取得 hello 連接資源，您可以啟用或停用 hello 選項。</span><span class="sxs-lookup"><span data-stu-id="ecf97-187">Once you obtain hello connection resource, you can enable or disable hello option.</span></span>

#### <a name="disable-usepolicybasedtrafficselectors"></a><span data-ttu-id="ecf97-188">停用 UsePolicyBasedTrafficSelectors</span><span class="sxs-lookup"><span data-stu-id="ecf97-188">Disable UsePolicyBasedTrafficSelectors</span></span>
<span data-ttu-id="ecf97-189">hello 下列範例會停用 hello 以原則為基礎的傳輸選取器選項，但保留 hello IPsec/IKE 原則保持不變：</span><span class="sxs-lookup"><span data-stu-id="ecf97-189">hello following example disables hello policy-based traffic selectors option, but leaves hello IPsec/IKE policy unchanged:</span></span>

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -UsePolicyBasedTrafficSelectors $False
```

#### <a name="enable-usepolicybasedtrafficselectors"></a><span data-ttu-id="ecf97-190">啟用 UsePolicyBasedTrafficSelectors</span><span class="sxs-lookup"><span data-stu-id="ecf97-190">Enable UsePolicyBasedTrafficSelectors</span></span>
<span data-ttu-id="ecf97-191">hello 下列範例會啟用 hello 以原則為基礎的傳輸選取器選項，但保留 hello IPsec/IKE 原則保持不變：</span><span class="sxs-lookup"><span data-stu-id="ecf97-191">hello following example enables hello policy-based traffic selectors option, but leaves hello IPsec/IKE policy unchanged:</span></span>

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -UsePolicyBasedTrafficSelectors $True
```

## <a name="next-steps"></a><span data-ttu-id="ecf97-192">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ecf97-192">Next steps</span></span>
<span data-ttu-id="ecf97-193">一旦完成您的連線，您可以將虛擬機器 tooyour 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="ecf97-193">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="ecf97-194">請參閱 [建立網站的虛擬機器](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 以取得相關步驟。</span><span class="sxs-lookup"><span data-stu-id="ecf97-194">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span></span>

<span data-ttu-id="ecf97-195">如需自訂 IPsec/IKE 原則的詳細資訊，也請檢閱[設定 S2S VPN 或 VNet 對 VNet 連線的 IPsec/IKE 原則](vpn-gateway-ipsecikepolicy-rm-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="ecf97-195">Also review [Configure IPsec/IKE policy for S2S VPN or VNet-to-VNet connections](vpn-gateway-ipsecikepolicy-rm-powershell.md) for more details on custom IPsec/IKE policies.</span></span>
