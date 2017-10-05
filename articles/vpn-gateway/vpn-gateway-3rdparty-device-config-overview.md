---
title: "關於連線到 Azure VPN 閘道的第三方 VPN 裝置組態 | Microsoft Docs"
description: "本文提供連線到 Azure VPN 閘道之第三方 VPN 裝置組態的概觀。"
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: 
ms.assetid: a8bfc955-de49-4172-95ac-5257e262d7ea
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/20/2017
ms.author: yushwang
ms.openlocfilehash: 72dab85bb882b05d72cef26bef70437695b70416
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="overview-of-3rd-party-vpn-device-configurations"></a><span data-ttu-id="980e2-103">第三方 VPN 裝置組態的概觀</span><span class="sxs-lookup"><span data-stu-id="980e2-103">Overview of 3rd party VPN device configurations</span></span>
<span data-ttu-id="980e2-104">本文提供連線到 Azure VPN 閘道之內部部署 VPN 裝置組態的概觀。</span><span class="sxs-lookup"><span data-stu-id="980e2-104">This article provides an overview of on-premises VPN device configurations for connecting to Azure VPN gateways.</span></span> <span data-ttu-id="980e2-105">範例 Azure 虛擬網路和 VPN 閘道安裝程式將用來以相同參數連線到不同的內部部署 VPN 裝置。</span><span class="sxs-lookup"><span data-stu-id="980e2-105">The sample Azure virtual network and VPN gateway setup will be used to connect to different on-premises VPN devices with the same parameters.</span></span>

## <a name="device-requirements"></a><span data-ttu-id="980e2-106">裝置需求</span><span class="sxs-lookup"><span data-stu-id="980e2-106">Device requirements</span></span>
<span data-ttu-id="980e2-107">Azure VPN 閘道會針對 S2S VPN 通道使用標準的 IPsec/IKE 通訊協定組合。</span><span class="sxs-lookup"><span data-stu-id="980e2-107">Azure VPN gateways use standard IPsec/IKE protocol suites for S2S VPN tunnels.</span></span> <span data-ttu-id="980e2-108">請參閱[關於 VPN 裝置](vpn-gateway-about-vpn-devices.md)，以取得詳細的 IPsec/IKE 通訊協定參數，以及 Azure VPN 閘道的預設密碼編譯演算法。</span><span class="sxs-lookup"><span data-stu-id="980e2-108">Refer to [About VPN devices](vpn-gateway-about-vpn-devices.md) for the detailed IPsec/IKE protocol parameters and default cryptographic algorithms for Azure VPN gateways.</span></span> <span data-ttu-id="980e2-109">您可以選擇性地針對特定連線指定密碼編譯演算法和金鑰長度的確切組合，如[關於密碼編譯需求](vpn-gateway-about-compliance-crypto.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="980e2-109">You can optionally specify the exact combination of cryptographic algorithms and key strengths for a specific connection as described in [About cryptographic requirements](vpn-gateway-about-compliance-crypto.md).</span></span>

## <span data-ttu-id="980e2-110"><a name ="singletunnel"></a>單一 VPN 通道</span><span class="sxs-lookup"><span data-stu-id="980e2-110"><a name ="singletunnel"></a>Single VPN tunnel</span></span>
<span data-ttu-id="980e2-111">第一個拓撲是由 Azure VPN 閘道與您內部部署 VPN 裝置之間的單一 S2S VPN 通道所組成。</span><span class="sxs-lookup"><span data-stu-id="980e2-111">The first topology consists of a single S2S VPN tunnel between an Azure VPN gateway and your on-premises VPN device.</span></span> <span data-ttu-id="980e2-112">您可以選擇透過 VPN 通道設定 BGP。</span><span class="sxs-lookup"><span data-stu-id="980e2-112">You can optionally configure BGP across the VPN tunnel.</span></span>

![單一通道](./media/vpn-gateway-3rdparty-device-config-overview/singletunnel.png)

<span data-ttu-id="980e2-114">請參閱[設定站對站連線](vpn-gateway-howto-site-to-site-resource-manager-portal.md)以取得詳細的逐步指引。</span><span class="sxs-lookup"><span data-stu-id="980e2-114">Refer to [Configure site-to-site connection](vpn-gateway-howto-site-to-site-resource-manager-portal.md) for detailed, step-by-step guidance.</span></span> <span data-ttu-id="980e2-115">下列各節會列出參數，並提供可協助您開始的範例 PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="980e2-115">The following sections list the parameters and provide a sample PowerShell script to help you get started.</span></span>

### <a name="network-and-vpn-gateway-information"></a><span data-ttu-id="980e2-116">網路和 VPN 閘道資訊</span><span class="sxs-lookup"><span data-stu-id="980e2-116">Network and VPN gateway information</span></span>
<span data-ttu-id="980e2-117">本節會列出適用於上述範例的參數。</span><span class="sxs-lookup"><span data-stu-id="980e2-117">This section list the parameters for the examples above.</span></span>

| <span data-ttu-id="980e2-118">**參數**</span><span class="sxs-lookup"><span data-stu-id="980e2-118">**Parameter**</span></span>                | <span data-ttu-id="980e2-119">**值**</span><span class="sxs-lookup"><span data-stu-id="980e2-119">**Value**</span></span>                    |
| ---                          | ---                          |
| <span data-ttu-id="980e2-120">VNet 位址首碼</span><span class="sxs-lookup"><span data-stu-id="980e2-120">VNet address prefixes</span></span>        | <span data-ttu-id="980e2-121">10.11.0.0/16</span><span class="sxs-lookup"><span data-stu-id="980e2-121">10.11.0.0/16</span></span><br><span data-ttu-id="980e2-122">10.12.0.0/16</span><span class="sxs-lookup"><span data-stu-id="980e2-122">10.12.0.0/16</span></span> |
| <span data-ttu-id="980e2-123">Azure VPN 閘道 IP</span><span class="sxs-lookup"><span data-stu-id="980e2-123">Azure VPN gateway IP</span></span>         | <span data-ttu-id="980e2-124">Azure VPN 閘道 IP</span><span class="sxs-lookup"><span data-stu-id="980e2-124">Azure VPN Gateway IP</span></span>         |
| <span data-ttu-id="980e2-125">內部部署位址首碼</span><span class="sxs-lookup"><span data-stu-id="980e2-125">On-premises address prefixes</span></span> | <span data-ttu-id="980e2-126">10.51.0.0/16</span><span class="sxs-lookup"><span data-stu-id="980e2-126">10.51.0.0/16</span></span><br><span data-ttu-id="980e2-127">10.52.0.0/16</span><span class="sxs-lookup"><span data-stu-id="980e2-127">10.52.0.0/16</span></span> |
| <span data-ttu-id="980e2-128">內部部署 VPN 裝置 IP</span><span class="sxs-lookup"><span data-stu-id="980e2-128">On-premises VPN device IP</span></span>    | <span data-ttu-id="980e2-129">內部部署 VPN 裝置 IP</span><span class="sxs-lookup"><span data-stu-id="980e2-129">On-premises VPN device IP</span></span>    |
| <span data-ttu-id="980e2-130">*VNet BGP ASN</span><span class="sxs-lookup"><span data-stu-id="980e2-130">*VNet BGP ASN</span></span>                | <span data-ttu-id="980e2-131">65010</span><span class="sxs-lookup"><span data-stu-id="980e2-131">65010</span></span>                        |
| <span data-ttu-id="980e2-132">*Azure BGP 對等 IP</span><span class="sxs-lookup"><span data-stu-id="980e2-132">*Azure BGP peer IP</span></span>           | <span data-ttu-id="980e2-133">10.12.255.30</span><span class="sxs-lookup"><span data-stu-id="980e2-133">10.12.255.30</span></span>                 |
| <span data-ttu-id="980e2-134">*內部部署 BGP ASN</span><span class="sxs-lookup"><span data-stu-id="980e2-134">*On-premises BGP ASN</span></span>         | <span data-ttu-id="980e2-135">65050</span><span class="sxs-lookup"><span data-stu-id="980e2-135">65050</span></span>                        |
| <span data-ttu-id="980e2-136">*內部部署 BGP 對等 IP</span><span class="sxs-lookup"><span data-stu-id="980e2-136">*On-premises BGP peer IP</span></span>     | <span data-ttu-id="980e2-137">10.52.255.254</span><span class="sxs-lookup"><span data-stu-id="980e2-137">10.52.255.254</span></span>                |

* <span data-ttu-id="980e2-138">(*) 僅適用於 BGP 的選擇性參數</span><span class="sxs-lookup"><span data-stu-id="980e2-138">(*) Optional parameters for BGP only</span></span>

### <a name="sample-powershell-script"></a><span data-ttu-id="980e2-139">範例 PowerShell 指令碼</span><span class="sxs-lookup"><span data-stu-id="980e2-139">Sample PowerShell script</span></span>
<span data-ttu-id="980e2-140">[使用 PowerShell 建立 S2S VPN 連線](vpn-gateway-create-site-to-site-rm-powershell.md)會提供詳細的指示。</span><span class="sxs-lookup"><span data-stu-id="980e2-140">[Create a S2S VPN connection using PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md) has the detailed instructions.</span></span> <span data-ttu-id="980e2-141">本節提供可協助您開始的範例指令碼。</span><span class="sxs-lookup"><span data-stu-id="980e2-141">This section provides a sample script to get you started.</span></span>

```powershell
# Declare your variables

$Sub1          = "Replace_With_Your_Subcription_Name"
$RG1           = "TestRG1"
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
$VNet1ASN      = 65010
$DNS1          = "8.8.8.8"
$GWName1       = "VNet1GW"
$GWIPName1     = "VNet1GWIP"
$GWIPconfName1 = "gwipconf1"
$Connection15  = "VNet1toSite5"
$LNGName5      = "Site5"
$LNGPrefix50   = "10.52.255.254/32"
$LNGPrefix51   = "10.51.0.0/16"
$LNGPrefix52   = "10.52.0.0/16"
$LNGIP5        = "Your_VPN_Device_IP"
$LNGASN5       = 65050
$BGPPeerIP5    = "10.52.255.254"

# Connect to your subscription and create a new resource group

Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1

# Create virtual network

$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1 $besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1

# Create VPN gateway

$gwpip1    = New-AzureRmPublicIpAddress -Name $GWIPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic
$vnet1     = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1   = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gwipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName1 -Subnet $subnet1 -PublicIpAddress $gwpip1

New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gwipconf1 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -Asn $VNet1ASN

# Create local network gateway

New-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG1 -Location $Location1 -GatewayIpAddress $LNGIP5 -AddressPrefix $LNGPrefix51,$LNGPrefix52 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP5

# Create the S2S VPN connection

$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw  = Get-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $False
```

### <span data-ttu-id="980e2-142"><a name ="policybased"></a> [選擇性] 搭配 "UsePolicyBasedTrafficSelectors" 使用自訂的 IPsec/IKE 原則</span><span class="sxs-lookup"><span data-stu-id="980e2-142"><a name ="policybased"></a> [Optional] Use custom IPsec/IKE policy with "UsePolicyBasedTrafficSelectors"</span></span>
<span data-ttu-id="980e2-143">如果您的 VPN 裝置不支援「任意-到-任意」的流量選取器 (路由式/VTI 式組態)，您必須建立自訂的 IPsec/IKE 原則並設定 "UsePolicyBasedTrafficSelectors" 選項，如[這篇文章](vpn-gateway-connect-multiple-policybased-rm-ps.md)所述。</span><span class="sxs-lookup"><span data-stu-id="980e2-143">If your VPN devices do not support "any-to-any" traffic selectors (route-based/VTI-based configuration), you will need to create a custom IPsec/IKE policy and configure "UsePolicyBasedTrafficSelectors" option as described in [this article](vpn-gateway-connect-multiple-policybased-rm-ps.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="980e2-144">您需要建立 IPsec/IKE 原則，才能在連線上啟用 "UsePolicyBasedTrafficSelectors" 選項。</span><span class="sxs-lookup"><span data-stu-id="980e2-144">You need to create an IPsec/IKE policy in order to enable "UsePolicyBasedTrafficSelectors" option on the connection.</span></span>

<span data-ttu-id="980e2-145">下列範例指令碼會使用下列演算法和參數來建立 IPsec/IKE 原則：</span><span class="sxs-lookup"><span data-stu-id="980e2-145">The sample script below creates an IPsec/IKE policy with the following algorithms and parameters:</span></span>
* <span data-ttu-id="980e2-146">IKEv2：AES256、SHA384、DHGroup24</span><span class="sxs-lookup"><span data-stu-id="980e2-146">IKEv2: AES256, SHA384, DHGroup24</span></span>
* <span data-ttu-id="980e2-147">IPsec：AES256、SHA1、PFS24、SA 存留期 7200 秒和 20480000KB (20GB)</span><span class="sxs-lookup"><span data-stu-id="980e2-147">IPsec: AES256, SHA1, PFS24, SA Lifetime 7200 seconds & 20480000KB (20GB)</span></span>

<span data-ttu-id="980e2-148">接著套用原則，並在連線上啟用 "UesPolicyBasedTrafficSelectors"。</span><span class="sxs-lookup"><span data-stu-id="980e2-148">It then applies the policy and enables "UesPolicyBasedTrafficSelectors" on the connection.</span></span>

```powershell
$ipsecpolicy5 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption AES256 -IpsecIntegrity SHA1 -PfsGroup PFS24 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 20480000

$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw  = Get-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $False -IpsecPolicies $ipsecpolicy5 -UsePolicyBasedTrafficSelectors $True
```

### <span data-ttu-id="980e2-149"><a name ="bgp"></a>[選擇性] 在 S2S VPN 連線使用 BGP</span><span class="sxs-lookup"><span data-stu-id="980e2-149"><a name ="bgp"></a>[Optional] Use BGP on S2S VPN connection</span></span>
<span data-ttu-id="980e2-150">您可以選擇性地在連線上使用 BGP。</span><span class="sxs-lookup"><span data-stu-id="980e2-150">You can optionally use BGP on the connection.</span></span> <span data-ttu-id="980e2-151">請參閱[適用於 VPN 閘道的 BGP](vpn-gateway-bgp-resource-manager-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="980e2-151">See [BGP for VPN gateway](vpn-gateway-bgp-resource-manager-ps.md).</span></span> <span data-ttu-id="980e2-152">有兩個差異：</span><span class="sxs-lookup"><span data-stu-id="980e2-152">There are two differences:</span></span>

<span data-ttu-id="980e2-153">內部部署位址首碼可以是單一主機位址，內部部署 BGP 對等 IP 位址：</span><span class="sxs-lookup"><span data-stu-id="980e2-153">The on-premises address prefixes can be a single host address, the on-premises BGP peer IP address:</span></span>

```powershell
New-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG1 -Location $Location1 -GatewayIpAddress $LNGIP5 -AddressPrefix $LNGPrefix50 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP5
```

<span data-ttu-id="980e2-154">您必須在建立連線時，將 "-EnableBGP" 設為 $True：</span><span class="sxs-lookup"><span data-stu-id="980e2-154">You must set "-EnableBGP" to $True when creating the connection:</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $True
```

## <a name="next-steps"></a><span data-ttu-id="980e2-155">後續步驟</span><span class="sxs-lookup"><span data-stu-id="980e2-155">Next steps</span></span>
<span data-ttu-id="980e2-156">如需設定主動-主動跨單位和 VNet 對 VNet 連線的步驟，請參閱[設定跨單位和 VNet 對 VNet 連線的主動-主動 VPN 閘道](vpn-gateway-activeactive-rm-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="980e2-156">See [Configuring Active-Active VPN Gateways for Cross-Premises and VNet-to-VNet Connections](vpn-gateway-activeactive-rm-powershell.md) for steps to configure active-active cross-premises and VNet-to-VNet connections.</span></span>

