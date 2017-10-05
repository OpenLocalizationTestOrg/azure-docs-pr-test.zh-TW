---
title: "將 Azure VPN 閘道連線至多個內部部署以原則為基礎的 VPN 裝置：Azure Resource Manager：PowerShell | Microsoft Docs"
description: "本文引導您使用 Azure Resource Manager 和 PowerShell，將以 Azure 路由為基礎的 VPN 閘道設定為多個以原則為基礎的 VPN 裝置。"
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
ms.openlocfilehash: 17211379ec61891982a02efca6730ca0da87c1ef
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="connect-azure-vpn-gateways-to-multiple-on-premises-policy-based-vpn-devices-using-powershell"></a><span data-ttu-id="c93f1-103">使用 PowerShell 將 Azure VPN 閘道連線至多個內部部署以原則為基礎的 VPN 裝置</span><span class="sxs-lookup"><span data-stu-id="c93f1-103">Connect Azure VPN gateways to multiple on-premises policy-based VPN devices using PowerShell</span></span>

<span data-ttu-id="c93f1-104">本文將協助您運用 S2S VPN 連線上的自訂 IPsec/IKE 原則，設定以 Azure 路由為基礎的 VPN 閘道連線至多個內部部署以原則為基礎的 VPN 裝置。</span><span class="sxs-lookup"><span data-stu-id="c93f1-104">This article helps you configure an Azure route-based VPN gateway to connect to multiple on-premises policy-based VPN devices leveraging custom IPsec/IKE policies on S2S VPN connections.</span></span>

## <a name="about-policy-based-and-route-based-vpn-gateways"></a><span data-ttu-id="c93f1-105">關於以原則為基礎的 VPN 閘道和以路由為基礎的 VPN 閘道</span><span class="sxs-lookup"><span data-stu-id="c93f1-105">About policy-based and route-based VPN gateways</span></span>

<span data-ttu-id="c93f1-106">以原則為基礎的 VPN 裝置「與」以路由為基礎的 VPN 裝置，其差異在於如何於連線上設定 IPsec 流量選取器：</span><span class="sxs-lookup"><span data-stu-id="c93f1-106">Policy- *vs.* route-based VPN devices differ in how the IPsec traffic selectors are set on a connection:</span></span>

* <span data-ttu-id="c93f1-107">**以原則為基礎的** VPN 裝置使用這兩個網路的前置詞組合，定義如何透過 IPsec 通道來加密/解密流量。</span><span class="sxs-lookup"><span data-stu-id="c93f1-107">**Policy-based** VPN devices use the combinations of prefixes from both networks to define how traffic is encrypted/decrypted through IPsec tunnels.</span></span> <span data-ttu-id="c93f1-108">它通常內建在執行封包篩選的防火牆裝置上。</span><span class="sxs-lookup"><span data-stu-id="c93f1-108">It is typically built on firewall devices that perform packet filtering.</span></span> <span data-ttu-id="c93f1-109">IPsec 通道加密和解密會新增至封包篩選和處理引擎。</span><span class="sxs-lookup"><span data-stu-id="c93f1-109">IPsec tunnel encryption and decryption are added to the packet filtering and processing engine.</span></span>
* <span data-ttu-id="c93f1-110">**以路由為基礎的** VPN 裝置使用任何對任何 (萬用字元) 流量選取器，並讓路由/轉接資料表將流量導向到不同 IPsec 通道。</span><span class="sxs-lookup"><span data-stu-id="c93f1-110">**Route-based** VPN devices use any-to-any (wildcard) traffic selectors, and let routing/forwarding tables direct traffic to different IPsec tunnels.</span></span> <span data-ttu-id="c93f1-111">它通常內建在路由器平台上，其中，每個 IPsec 通道都會建模為網路介面或 VTI (虛擬通道介面)。</span><span class="sxs-lookup"><span data-stu-id="c93f1-111">It is typically built on router platforms where each IPsec tunnel is modeled as a network interface or VTI (virtual tunnel interface).</span></span>

<span data-ttu-id="c93f1-112">下列各圖反白顯示兩個模型：</span><span class="sxs-lookup"><span data-stu-id="c93f1-112">The following diagrams highlight the two models:</span></span>

### <a name="policy-based-vpn-example"></a><span data-ttu-id="c93f1-113">以原則為基礎的 VPN 範例</span><span class="sxs-lookup"><span data-stu-id="c93f1-113">Policy-based VPN example</span></span>
![以原則為基礎](./media/vpn-gateway-connect-multiple-policybased-rm-ps/policybasedmultisite.png)

### <a name="route-based-vpn-example"></a><span data-ttu-id="c93f1-115">以路由為基礎的 VPN 範例</span><span class="sxs-lookup"><span data-stu-id="c93f1-115">Route-based VPN example</span></span>
![以路由為基礎](./media/vpn-gateway-connect-multiple-policybased-rm-ps/routebasedmultisite.png)

### <a name="azure-support-for-policy-based-vpn"></a><span data-ttu-id="c93f1-117">以原則為基礎的 VPN 的 Azure 支援</span><span class="sxs-lookup"><span data-stu-id="c93f1-117">Azure support for policy-based VPN</span></span>
<span data-ttu-id="c93f1-118">Azure 目前支援兩種 VPN 閘道模式：以路由為基礎的 VPN 閘道和以原則為基礎的 VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="c93f1-118">Currently, Azure supports both modes of VPN gateways: route-based VPN gateways and policy-based VPN gateways.</span></span> <span data-ttu-id="c93f1-119">它們內建在不同內部平台上，因而導致不同的規格：</span><span class="sxs-lookup"><span data-stu-id="c93f1-119">They are built on different internal platforms, which result in different specifications:</span></span>

|                          | <span data-ttu-id="c93f1-120">**PolicyBased VPN 閘道**</span><span class="sxs-lookup"><span data-stu-id="c93f1-120">**PolicyBased VPN Gateway**</span></span> | <span data-ttu-id="c93f1-121">**RouteBased VPN 閘道**</span><span class="sxs-lookup"><span data-stu-id="c93f1-121">**RouteBased VPN Gateway**</span></span>               |
| ---                      | ---                         | ---                                      |
| <span data-ttu-id="c93f1-122">**Azure 閘道 SKU**</span><span class="sxs-lookup"><span data-stu-id="c93f1-122">**Azure Gateway SKU**</span></span>    | <span data-ttu-id="c93f1-123">基本</span><span class="sxs-lookup"><span data-stu-id="c93f1-123">Basic</span></span>                       | <span data-ttu-id="c93f1-124">Basic、Standard、HighPerformance</span><span class="sxs-lookup"><span data-stu-id="c93f1-124">Basic, Standard, HighPerformance</span></span>         |
| <span data-ttu-id="c93f1-125">**IKE 版本**</span><span class="sxs-lookup"><span data-stu-id="c93f1-125">**IKE version**</span></span>          | <span data-ttu-id="c93f1-126">IKEv1</span><span class="sxs-lookup"><span data-stu-id="c93f1-126">IKEv1</span></span>                       | <span data-ttu-id="c93f1-127">IKEv2</span><span class="sxs-lookup"><span data-stu-id="c93f1-127">IKEv2</span></span>                                    |
| <span data-ttu-id="c93f1-128">**最大S2S 連線**</span><span class="sxs-lookup"><span data-stu-id="c93f1-128">**Max. S2S connections**</span></span> | <span data-ttu-id="c93f1-129">**1**</span><span class="sxs-lookup"><span data-stu-id="c93f1-129">**1**</span></span>                       | <span data-ttu-id="c93f1-130">基本/標準：10</span><span class="sxs-lookup"><span data-stu-id="c93f1-130">Basic/Standard: 10</span></span><br> <span data-ttu-id="c93f1-131">高效能：30</span><span class="sxs-lookup"><span data-stu-id="c93f1-131">HighPerformance: 30</span></span> |
|                          |                             |                                          |

<span data-ttu-id="c93f1-132">您現在可以使用自訂 IPsec/IKE 原則，設定以 Azure 路由為基礎的 VPN 閘道搭配使用以前置詞為基礎的流量選取器與 "**PolicyBasedTrafficSelectors**" 選項，以連線至內部部署以原則為基礎的 VPN 裝置。</span><span class="sxs-lookup"><span data-stu-id="c93f1-132">With the custom IPsec/IKE policy, you can now configure Azure route-based VPN gateways to use prefix-based traffic selectors with option "**PolicyBasedTrafficSelectors**", to connect to on-premises policy-based VPN devices.</span></span> <span data-ttu-id="c93f1-133">這項功能可讓您從 Azure 虛擬網路和 VPN 閘道連線至多個內部部署以原則為基礎的 VPN/防火牆裝置，並從目前以 Azure 原則為基礎的 VPN 閘道移除單一連線限制。</span><span class="sxs-lookup"><span data-stu-id="c93f1-133">This capability allows you to connect from an Azure virtual network and VPN gateway to multiple on-premises policy-based VPN/firewall devices, removing the single connection limit from the current Azure policy-based VPN gateways.</span></span>

> [!IMPORTANT]
> 1. <span data-ttu-id="c93f1-134">若要啟用這個連線，內部部署以原則為基礎的 VPN 裝置必須支援 **IKEv2** 連線至以 Azure 路由為基礎的 VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="c93f1-134">To enable this connectivity, your on-premises policy-based VPN devices must support **IKEv2** to connect to the Azure route-based VPN gateways.</span></span> <span data-ttu-id="c93f1-135">確認您的 VPN 裝置規格。</span><span class="sxs-lookup"><span data-stu-id="c93f1-135">Check your VPN device specifications.</span></span>
> 2. <span data-ttu-id="c93f1-136">使用這種機制透過以原則為基礎的 VPN 裝置所連線的內部部署網路，只能連線至 Azure 虛擬網路；**其無法透過相同的 Azure VPN 閘道轉換到其他內部部署網路或虛擬網路**。</span><span class="sxs-lookup"><span data-stu-id="c93f1-136">The on-premises networks connecting through policy-based VPN devices with this mechanism can only connect to the Azure virtual network; **they cannot transit to other on-premises networks or virtual networks via the same Azure VPN gateway**.</span></span>
> 3. <span data-ttu-id="c93f1-137">設定選項是自訂 IPsec/IKE 連線原則的一部分。</span><span class="sxs-lookup"><span data-stu-id="c93f1-137">The configuration option is part of the custom IPsec/IKE connection policy.</span></span> <span data-ttu-id="c93f1-138">如果您啟用以原則為基礎的流量選取器選項，則必須指定完整原則 (IPsec/IKE 加密及完整性演算法、金鑰長度和 SA 存留期)。</span><span class="sxs-lookup"><span data-stu-id="c93f1-138">If you enable the policy-based traffic selector option, you must specify the complete policy (IPsec/IKE encryption and integrity algorithms, key strengths, and SA lifetimes).</span></span>

<span data-ttu-id="c93f1-139">下圖顯示透過 Azure VPN 閘道的轉換路由為何不適用於以原則為基礎的選項：</span><span class="sxs-lookup"><span data-stu-id="c93f1-139">The following diagram shows why transit routing via Azure VPN gateway doesn't work with the policy-based option:</span></span>

![以原則為基礎的傳輸](./media/vpn-gateway-connect-multiple-policybased-rm-ps/policybasedtransit.png)

<span data-ttu-id="c93f1-141">如圖所示，Azure VPN 閘道會有從虛擬網路到每個內部部署網路前置詞的流量選取器，但不是跨連線前置詞。</span><span class="sxs-lookup"><span data-stu-id="c93f1-141">As shown in the diagram, the Azure VPN gateway has traffic selectors from the virtual network to each of the on-premises network prefixes, but not the cross-connection prefixes.</span></span> <span data-ttu-id="c93f1-142">例如，內部部署網站 2、網站 3 和網站 4 分別可以與 VNet1 通訊，但無法透過 Azure VPN 閘道彼此連線。</span><span class="sxs-lookup"><span data-stu-id="c93f1-142">For example, on-premises site 2, site 3, and site 4 can each communicate to VNet1 respectively, but cannot connect via the Azure VPN gateway to each other.</span></span> <span data-ttu-id="c93f1-143">此圖顯示此設定下不適用於 Azure VPN 閘道的跨連線流量選取器。</span><span class="sxs-lookup"><span data-stu-id="c93f1-143">The diagram shows the cross-connect traffic selectors that are not available in the Azure VPN gateway under this configuration.</span></span>

## <a name="configure-policy-based-traffic-selectors-on-a-connection"></a><span data-ttu-id="c93f1-144">在連線上設定以原則為基礎的流量選取器</span><span class="sxs-lookup"><span data-stu-id="c93f1-144">Configure policy-based traffic selectors on a connection</span></span>

<span data-ttu-id="c93f1-145">本文中的指示遵循[設定 S2S 或 VNet 對 VNet 連線的 IPsec/IKE 原則](vpn-gateway-ipsecikepolicy-rm-powershell.md)中所述的相同範例，以建立 S2S VPN 連線。</span><span class="sxs-lookup"><span data-stu-id="c93f1-145">The instructions in this article follow the same example as described in [Configure IPsec/IKE policy for S2S or VNet-to-VNet connections](vpn-gateway-ipsecikepolicy-rm-powershell.md) to establish a S2S VPN connection.</span></span> <span data-ttu-id="c93f1-146">如下圖所示：</span><span class="sxs-lookup"><span data-stu-id="c93f1-146">This is shown in the following diagram:</span></span>

![s2s-policy](./media/vpn-gateway-connect-multiple-policybased-rm-ps/s2spolicypb.png)

<span data-ttu-id="c93f1-148">啟用這個連線的工作流程：</span><span class="sxs-lookup"><span data-stu-id="c93f1-148">The workflow to enable this connectivity:</span></span>
1. <span data-ttu-id="c93f1-149">建立跨單位連線的虛擬網路、VPN 閘道和區域網路閘道</span><span class="sxs-lookup"><span data-stu-id="c93f1-149">Create the virtual network, VPN gateway, and local network gateway for your cross-premises connection</span></span>
2. <span data-ttu-id="c93f1-150">建立 IPsec/IKE 原則</span><span class="sxs-lookup"><span data-stu-id="c93f1-150">Create an IPsec/IKE policy</span></span>
3. <span data-ttu-id="c93f1-151">如果您建立 S2S 或 VNet 對 VNet 連線，並在連線上**啟用以原則為基礎的流量選取器**，請套用原則。</span><span class="sxs-lookup"><span data-stu-id="c93f1-151">Apply the policy when you create a S2S or VNet-to-VNet connection, and **enable the policy-based traffic selectors** on the connection</span></span>
4. <span data-ttu-id="c93f1-152">如果已經建立連線，您可以套用原則，或將其更新為現有連線。</span><span class="sxs-lookup"><span data-stu-id="c93f1-152">If the connection is already created, you can apply or update the policy to an existing connection</span></span>

## <a name="enable-policy-based-traffic-selectors-on-a-connection"></a><span data-ttu-id="c93f1-153">在連線上啟用以原則為基礎的流量選取器</span><span class="sxs-lookup"><span data-stu-id="c93f1-153">Enable policy-based traffic selectors on a connection</span></span>

<span data-ttu-id="c93f1-154">請確定您已針對本節完成[設定 IPsec/IKE 原則文章的第 3 部分](vpn-gateway-ipsecikepolicy-rm-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="c93f1-154">Make sure you have completed [Part 3 of the Configure IPsec/IKE policy article](vpn-gateway-ipsecikepolicy-rm-powershell.md) for this section.</span></span> <span data-ttu-id="c93f1-155">下列範例會使用相同的參數和步驟：</span><span class="sxs-lookup"><span data-stu-id="c93f1-155">The following example uses the same parameters and steps:</span></span>

### <a name="step-1---create-the-virtual-network-vpn-gateway-and-local-network-gateway"></a><span data-ttu-id="c93f1-156">步驟1 - 建立虛擬網路、VPN 閘道和區域網路閘道</span><span class="sxs-lookup"><span data-stu-id="c93f1-156">Step 1 - Create the virtual network, VPN gateway, and local network gateway</span></span>

#### <a name="1-declare-your-variables--connect-to-your-subscription"></a><span data-ttu-id="c93f1-157">1.宣告變數，並連線到您的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="c93f1-157">1. Declare your variables & connect to your subscription</span></span>
<span data-ttu-id="c93f1-158">對於此練習，我們一開始先宣告我們的變數。</span><span class="sxs-lookup"><span data-stu-id="c93f1-158">For this exercise, we start by declaring our variables.</span></span> <span data-ttu-id="c93f1-159">請務必在設定生產環境時，使用您自己的值來取代該值。</span><span class="sxs-lookup"><span data-stu-id="c93f1-159">Be sure to replace the values with your own when configuring for production.</span></span>

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
<span data-ttu-id="c93f1-160">請確定您切換為 PowerShell 模式以使用 Resource Manager Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="c93f1-160">To use the Resource Manager cmdlets, make sure you switch to PowerShell mode.</span></span> <span data-ttu-id="c93f1-161">如需詳細資訊，請參閱 [搭配使用 Windows PowerShell 與 Resource Manager](../powershell-azure-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="c93f1-161">For more information, see [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="c93f1-162">開啟 PowerShell 主控台並連接到您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="c93f1-162">Open your PowerShell console and connect to your account.</span></span> <span data-ttu-id="c93f1-163">使用下列範例來協助您連接：</span><span class="sxs-lookup"><span data-stu-id="c93f1-163">Use the following sample to help you connect:</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="2-create-the-virtual-network-vpn-gateway-and-local-network-gateway"></a><span data-ttu-id="c93f1-164">2.建立虛擬網路、VPN 閘道和區域網路閘道</span><span class="sxs-lookup"><span data-stu-id="c93f1-164">2. Create the virtual network, VPN gateway, and local network gateway</span></span>
<span data-ttu-id="c93f1-165">下列範例會建立有三個子網路的虛擬網路 TestVNet1 和 VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="c93f1-165">The following example creates the virtual network, TestVNet1 with three subnets, and the VPN gateway.</span></span> <span data-ttu-id="c93f1-166">替代值時，務必一律將您的閘道子網路特定命名為 GatewaySubnet。</span><span class="sxs-lookup"><span data-stu-id="c93f1-166">When substituting values, it's important that you always name your gateway subnet specifically 'GatewaySubnet'.</span></span> <span data-ttu-id="c93f1-167">如果您將其命名為其他名稱，閘道建立會失敗。</span><span class="sxs-lookup"><span data-stu-id="c93f1-167">If you name it something else, your gateway creation fails.</span></span>

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

### <a name="step-2---create-a-s2s-vpn-connection-with-an-ipsecike-policy"></a><span data-ttu-id="c93f1-168">步驟 2 - 使用 IPsec/IKE 原則建立 S2S VPN 連線</span><span class="sxs-lookup"><span data-stu-id="c93f1-168">Step 2 - Create a S2S VPN connection with an IPsec/IKE policy</span></span>

#### <a name="1-create-an-ipsecike-policy"></a><span data-ttu-id="c93f1-169">1.建立 IPsec/IKE 原則</span><span class="sxs-lookup"><span data-stu-id="c93f1-169">1. Create an IPsec/IKE policy</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c93f1-170">您需要建立 IPsec/IKE 原則，才能在連線上啟用 "UsePolicyBasedTrafficSelectors" 選項。</span><span class="sxs-lookup"><span data-stu-id="c93f1-170">You need to create an IPsec/IKE policy in order to enable "UsePolicyBasedTrafficSelectors" option on the connection.</span></span>

<span data-ttu-id="c93f1-171">下列範例會使用這些演算法和參數來建立 IPsec/IKE 原則：</span><span class="sxs-lookup"><span data-stu-id="c93f1-171">The following example creates an IPsec/IKE policy with these algorithms and parameters:</span></span>
* <span data-ttu-id="c93f1-172">IKEv2：AES256、SHA384、DHGroup24</span><span class="sxs-lookup"><span data-stu-id="c93f1-172">IKEv2: AES256, SHA384, DHGroup24</span></span>
* <span data-ttu-id="c93f1-173">IPsec：AES256、SHA256、PFS24、SA 存留期 3600 秒和 2048KB</span><span class="sxs-lookup"><span data-stu-id="c93f1-173">IPsec: AES256, SHA256, PFS24, SA Lifetime 3600 seconds & 2048KB</span></span>

```powershell
$ipsecpolicy6 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption AES256 -IpsecIntegrity SHA256 -PfsGroup PFS24 -SALifeTimeSeconds 3600 -SADataSizeKilobytes 2048
```

#### <a name="2-create-the-s2s-vpn-connection-with-policy-based-traffic-selectors-and-ipsecike-policy"></a><span data-ttu-id="c93f1-174">2.使用以原則為基礎的流量選取器和 IPsec/IKE 原則來建立 S2S VPN 連線</span><span class="sxs-lookup"><span data-stu-id="c93f1-174">2. Create the S2S VPN connection with policy-based traffic selectors and IPsec/IKE policy</span></span>
<span data-ttu-id="c93f1-175">建立 S2S VPN 連線，並套用前面步驟所建立的 IPsec/IKE 原則。</span><span class="sxs-lookup"><span data-stu-id="c93f1-175">Create an S2S VPN connection and apply the IPsec/IKE policy created in the previous step.</span></span> <span data-ttu-id="c93f1-176">請注意，使用額外參數 "-UsePolicyBasedTrafficSelectors $True"，可在連線上啟用以原則為基礎的流量選取器。</span><span class="sxs-lookup"><span data-stu-id="c93f1-176">Be aware of the additional parameter "-UsePolicyBasedTrafficSelectors $True"  which enables policy-based traffic selectors on the connection.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng6 = Get-AzureRmLocalNetworkGateway  -Name $LNGName6 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng6 -Location $Location1 -ConnectionType IPsec -UsePolicyBasedTrafficSelectors $True -IpsecPolicies $ipsecpolicy6 -SharedKey 'AzureA1b2C3'
```

<span data-ttu-id="c93f1-177">完成步驟後，S2S VPN 連線將會使用所定義的 IPsec/IKE 原則，並在連線上啟用以原則為基礎的流量選取器。</span><span class="sxs-lookup"><span data-stu-id="c93f1-177">After completing the steps, the S2S VPN connection will use the IPsec/IKE policy defined, and enable policy-based traffic selectors on the connection.</span></span> <span data-ttu-id="c93f1-178">您可以重複相同的步驟，以從相同的 Azure VPN 閘道將更多的連線新增至其他內部部署以原則為基礎的 VPN 裝置。</span><span class="sxs-lookup"><span data-stu-id="c93f1-178">You can repeat the same steps to add more connections to additional on-premises policy-based VPN devices from the same Azure VPN gateway.</span></span>

## <a name="update-policy-based-traffic-selectors-for-a-connection"></a><span data-ttu-id="c93f1-179">更新連線的以原則為基礎的流量選取器</span><span class="sxs-lookup"><span data-stu-id="c93f1-179">Update policy-based traffic selectors for a connection</span></span>
<span data-ttu-id="c93f1-180">最後一節將示範如何更新現有 S2S VPN 連線的以原則為基礎的流量選取器選項。</span><span class="sxs-lookup"><span data-stu-id="c93f1-180">The last section shows you how to update the policy-based traffic selectors option for an existing  S2S VPN connection.</span></span>

### <a name="1-get-the-connection"></a><span data-ttu-id="c93f1-181">1.取得連線</span><span class="sxs-lookup"><span data-stu-id="c93f1-181">1. Get the connection</span></span>
<span data-ttu-id="c93f1-182">取得連線資源。</span><span class="sxs-lookup"><span data-stu-id="c93f1-182">Get the connection resource.</span></span>

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1
```

### <a name="2-check-the-policy-based-traffic-selectors-option"></a><span data-ttu-id="c93f1-183">2.檢查以原則為基礎的流量選取器選項</span><span class="sxs-lookup"><span data-stu-id="c93f1-183">2. Check the policy-based traffic selectors option</span></span>
<span data-ttu-id="c93f1-184">下行將說明是否將以原則為基礎的流量選取器用於連線：</span><span class="sxs-lookup"><span data-stu-id="c93f1-184">The following line shows whether the policy-based traffic selectors are used for the connection:</span></span>

```powershell
$connection6.UsePolicyBasedTrafficSelectors
```

<span data-ttu-id="c93f1-185">如果該行傳回 "**True**"，則已在連線上設定以原則為基礎的流量選取器；否則，它會傳回 "**False**"。</span><span class="sxs-lookup"><span data-stu-id="c93f1-185">If the line returns "**True**", then policy-based traffic selectors are configured on the connection; otherwise it returns "**False**."</span></span>

### <a name="3-update-the-policy-based-traffic-selectors-on-a-connection"></a><span data-ttu-id="c93f1-186">3.更新連線上的以原則為基礎的流量選取器</span><span class="sxs-lookup"><span data-stu-id="c93f1-186">3. Update the policy-based traffic selectors on a connection</span></span>
<span data-ttu-id="c93f1-187">在您取得連線資源之後，即可啟用或停用此選項。</span><span class="sxs-lookup"><span data-stu-id="c93f1-187">Once you obtain the connection resource, you can enable or disable the option.</span></span>

#### <a name="disable-usepolicybasedtrafficselectors"></a><span data-ttu-id="c93f1-188">停用 UsePolicyBasedTrafficSelectors</span><span class="sxs-lookup"><span data-stu-id="c93f1-188">Disable UsePolicyBasedTrafficSelectors</span></span>
<span data-ttu-id="c93f1-189">下列範例會停用以原則為基礎的流量選取器選項，但 IPsec/IKE 原則保留不變：</span><span class="sxs-lookup"><span data-stu-id="c93f1-189">The following example disables the policy-based traffic selectors option, but leaves the IPsec/IKE policy unchanged:</span></span>

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -UsePolicyBasedTrafficSelectors $False
```

#### <a name="enable-usepolicybasedtrafficselectors"></a><span data-ttu-id="c93f1-190">啟用 UsePolicyBasedTrafficSelectors</span><span class="sxs-lookup"><span data-stu-id="c93f1-190">Enable UsePolicyBasedTrafficSelectors</span></span>
<span data-ttu-id="c93f1-191">下列範例會啟用以原則為基礎的流量選取器選項，但 IPsec/IKE 原則保留不變：</span><span class="sxs-lookup"><span data-stu-id="c93f1-191">The following example enables the policy-based traffic selectors option, but leaves the IPsec/IKE policy unchanged:</span></span>

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -UsePolicyBasedTrafficSelectors $True
```

## <a name="next-steps"></a><span data-ttu-id="c93f1-192">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c93f1-192">Next steps</span></span>
<span data-ttu-id="c93f1-193">一旦完成您的連接，就可以將虛擬機器加入您的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="c93f1-193">Once your connection is complete, you can add virtual machines to your virtual networks.</span></span> <span data-ttu-id="c93f1-194">請參閱 [建立網站的虛擬機器](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 以取得相關步驟。</span><span class="sxs-lookup"><span data-stu-id="c93f1-194">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span></span>

<span data-ttu-id="c93f1-195">如需自訂 IPsec/IKE 原則的詳細資訊，也請檢閱[設定 S2S VPN 或 VNet 對 VNet 連線的 IPsec/IKE 原則](vpn-gateway-ipsecikepolicy-rm-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="c93f1-195">Also review [Configure IPsec/IKE policy for S2S VPN or VNet-to-VNet connections](vpn-gateway-ipsecikepolicy-rm-powershell.md) for more details on custom IPsec/IKE policies.</span></span>
