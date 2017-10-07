---
title: "aaaAbout 第 3 個合作對象 VPN 裝置組態 tooconnect tooAzure VPN 閘道 |Microsoft 文件"
description: "本文章提供連接 tooAzure VPN 閘道第 3 個合作對象 VPN 裝置組態的概觀。"
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
ms.openlocfilehash: 3bb4fc94bc625386c2d0a02e1dcbdeb38ee0665e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-3rd-party-vpn-device-configurations"></a><span data-ttu-id="b24e4-103">第三方 VPN 裝置組態的概觀</span><span class="sxs-lookup"><span data-stu-id="b24e4-103">Overview of 3rd party VPN device configurations</span></span>
<span data-ttu-id="b24e4-104">本文章提供連接 tooAzure VPN 閘道的內部部署 VPN 裝置組態的概觀。</span><span class="sxs-lookup"><span data-stu-id="b24e4-104">This article provides an overview of on-premises VPN device configurations for connecting tooAzure VPN gateways.</span></span> <span data-ttu-id="b24e4-105">hello 範例 Azure 虛擬網路和 VPN 閘道安裝程式將會使用的 tooconnect toodifferent 在內部部署 VPN 裝置以 hello 相同的參數。</span><span class="sxs-lookup"><span data-stu-id="b24e4-105">hello sample Azure virtual network and VPN gateway setup will be used tooconnect toodifferent on-premises VPN devices with hello same parameters.</span></span>

## <a name="device-requirements"></a><span data-ttu-id="b24e4-106">裝置需求</span><span class="sxs-lookup"><span data-stu-id="b24e4-106">Device requirements</span></span>
<span data-ttu-id="b24e4-107">Azure VPN 閘道會針對 S2S VPN 通道使用標準的 IPsec/IKE 通訊協定組合。</span><span class="sxs-lookup"><span data-stu-id="b24e4-107">Azure VPN gateways use standard IPsec/IKE protocol suites for S2S VPN tunnels.</span></span> <span data-ttu-id="b24e4-108">請參閱太[關於 VPN 裝置](vpn-gateway-about-vpn-devices.md)hello 詳細的 IPsec/IKE 通訊協定參數和 Azure VPN 閘道的預設密碼編譯演算法。</span><span class="sxs-lookup"><span data-stu-id="b24e4-108">Refer too[About VPN devices](vpn-gateway-about-vpn-devices.md) for hello detailed IPsec/IKE protocol parameters and default cryptographic algorithms for Azure VPN gateways.</span></span> <span data-ttu-id="b24e4-109">中所述，您可以選擇指定的密碼編譯演算法和金鑰長度為特定連線的 hello 確切組合[有關密碼編譯需求](vpn-gateway-about-compliance-crypto.md)。</span><span class="sxs-lookup"><span data-stu-id="b24e4-109">You can optionally specify hello exact combination of cryptographic algorithms and key strengths for a specific connection as described in [About cryptographic requirements](vpn-gateway-about-compliance-crypto.md).</span></span>

## <span data-ttu-id="b24e4-110"><a name ="singletunnel"></a>單一 VPN 通道</span><span class="sxs-lookup"><span data-stu-id="b24e4-110"><a name ="singletunnel"></a>Single VPN tunnel</span></span>
<span data-ttu-id="b24e4-111">hello 第一個拓撲是由單一的 S2S VPN 通道，Azure VPN 閘道與內部部署 VPN 裝置之間所組成。</span><span class="sxs-lookup"><span data-stu-id="b24e4-111">hello first topology consists of a single S2S VPN tunnel between an Azure VPN gateway and your on-premises VPN device.</span></span> <span data-ttu-id="b24e4-112">您可以選擇性地跨 hello VPN 通道設定 BGP。</span><span class="sxs-lookup"><span data-stu-id="b24e4-112">You can optionally configure BGP across hello VPN tunnel.</span></span>

![單一通道](./media/vpn-gateway-3rdparty-device-config-overview/singletunnel.png)

<span data-ttu-id="b24e4-114">請參閱太[設定站對站連線](vpn-gateway-howto-site-to-site-resource-manager-portal.md)如需詳細的逐步指引。</span><span class="sxs-lookup"><span data-stu-id="b24e4-114">Refer too[Configure site-to-site connection](vpn-gateway-howto-site-to-site-resource-manager-portal.md) for detailed, step-by-step guidance.</span></span> <span data-ttu-id="b24e4-115">hello 下列各節列出 hello 參數，並提供您快速入門範例 PowerShell 指令碼 toohelp。</span><span class="sxs-lookup"><span data-stu-id="b24e4-115">hello following sections list hello parameters and provide a sample PowerShell script toohelp you get started.</span></span>

### <a name="network-and-vpn-gateway-information"></a><span data-ttu-id="b24e4-116">網路和 VPN 閘道資訊</span><span class="sxs-lookup"><span data-stu-id="b24e4-116">Network and VPN gateway information</span></span>
<span data-ttu-id="b24e4-117">本節列出 hello 參數，如上述的 hello 範例。</span><span class="sxs-lookup"><span data-stu-id="b24e4-117">This section list hello parameters for hello examples above.</span></span>

| <span data-ttu-id="b24e4-118">**參數**</span><span class="sxs-lookup"><span data-stu-id="b24e4-118">**Parameter**</span></span>                | <span data-ttu-id="b24e4-119">**值**</span><span class="sxs-lookup"><span data-stu-id="b24e4-119">**Value**</span></span>                    |
| ---                          | ---                          |
| <span data-ttu-id="b24e4-120">VNet 位址首碼</span><span class="sxs-lookup"><span data-stu-id="b24e4-120">VNet address prefixes</span></span>        | <span data-ttu-id="b24e4-121">10.11.0.0/16</span><span class="sxs-lookup"><span data-stu-id="b24e4-121">10.11.0.0/16</span></span><br><span data-ttu-id="b24e4-122">10.12.0.0/16</span><span class="sxs-lookup"><span data-stu-id="b24e4-122">10.12.0.0/16</span></span> |
| <span data-ttu-id="b24e4-123">Azure VPN 閘道 IP</span><span class="sxs-lookup"><span data-stu-id="b24e4-123">Azure VPN gateway IP</span></span>         | <span data-ttu-id="b24e4-124">Azure VPN 閘道 IP</span><span class="sxs-lookup"><span data-stu-id="b24e4-124">Azure VPN Gateway IP</span></span>         |
| <span data-ttu-id="b24e4-125">內部部署位址首碼</span><span class="sxs-lookup"><span data-stu-id="b24e4-125">On-premises address prefixes</span></span> | <span data-ttu-id="b24e4-126">10.51.0.0/16</span><span class="sxs-lookup"><span data-stu-id="b24e4-126">10.51.0.0/16</span></span><br><span data-ttu-id="b24e4-127">10.52.0.0/16</span><span class="sxs-lookup"><span data-stu-id="b24e4-127">10.52.0.0/16</span></span> |
| <span data-ttu-id="b24e4-128">內部部署 VPN 裝置 IP</span><span class="sxs-lookup"><span data-stu-id="b24e4-128">On-premises VPN device IP</span></span>    | <span data-ttu-id="b24e4-129">內部部署 VPN 裝置 IP</span><span class="sxs-lookup"><span data-stu-id="b24e4-129">On-premises VPN device IP</span></span>    |
| <span data-ttu-id="b24e4-130">*VNet BGP ASN</span><span class="sxs-lookup"><span data-stu-id="b24e4-130">*VNet BGP ASN</span></span>                | <span data-ttu-id="b24e4-131">65010</span><span class="sxs-lookup"><span data-stu-id="b24e4-131">65010</span></span>                        |
| <span data-ttu-id="b24e4-132">*Azure BGP 對等 IP</span><span class="sxs-lookup"><span data-stu-id="b24e4-132">*Azure BGP peer IP</span></span>           | <span data-ttu-id="b24e4-133">10.12.255.30</span><span class="sxs-lookup"><span data-stu-id="b24e4-133">10.12.255.30</span></span>                 |
| <span data-ttu-id="b24e4-134">*內部部署 BGP ASN</span><span class="sxs-lookup"><span data-stu-id="b24e4-134">*On-premises BGP ASN</span></span>         | <span data-ttu-id="b24e4-135">65050</span><span class="sxs-lookup"><span data-stu-id="b24e4-135">65050</span></span>                        |
| <span data-ttu-id="b24e4-136">*內部部署 BGP 對等 IP</span><span class="sxs-lookup"><span data-stu-id="b24e4-136">*On-premises BGP peer IP</span></span>     | <span data-ttu-id="b24e4-137">10.52.255.254</span><span class="sxs-lookup"><span data-stu-id="b24e4-137">10.52.255.254</span></span>                |

* <span data-ttu-id="b24e4-138">(*) 僅適用於 BGP 的選擇性參數</span><span class="sxs-lookup"><span data-stu-id="b24e4-138">(*) Optional parameters for BGP only</span></span>

### <a name="sample-powershell-script"></a><span data-ttu-id="b24e4-139">範例 PowerShell 指令碼</span><span class="sxs-lookup"><span data-stu-id="b24e4-139">Sample PowerShell script</span></span>
<span data-ttu-id="b24e4-140">[建立 S2S VPN 連線使用 PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md) hello 詳細指示。</span><span class="sxs-lookup"><span data-stu-id="b24e4-140">[Create a S2S VPN connection using PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md) has hello detailed instructions.</span></span> <span data-ttu-id="b24e4-141">本節提供範例指令碼 tooget 您已啟動。</span><span class="sxs-lookup"><span data-stu-id="b24e4-141">This section provides a sample script tooget you started.</span></span>

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

# Connect tooyour subscription and create a new resource group

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

# Create hello S2S VPN connection

$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw  = Get-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $False
```

### <span data-ttu-id="b24e4-142"><a name ="policybased"></a> [選擇性] 搭配 "UsePolicyBasedTrafficSelectors" 使用自訂的 IPsec/IKE 原則</span><span class="sxs-lookup"><span data-stu-id="b24e4-142"><a name ="policybased"></a> [Optional] Use custom IPsec/IKE policy with "UsePolicyBasedTrafficSelectors"</span></span>
<span data-ttu-id="b24e4-143">如果您的 VPN 裝置不支援 「 任何-到-any"流量選取器 （路由-基礎/VTI 為基礎的組態），您將需要 toocreate 自訂 IPsec/IKE 原則和設定 「 UsePolicyBasedTrafficSelectors"選項中所述[這篇文章](vpn-gateway-connect-multiple-policybased-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="b24e4-143">If your VPN devices do not support "any-to-any" traffic selectors (route-based/VTI-based configuration), you will need toocreate a custom IPsec/IKE policy and configure "UsePolicyBasedTrafficSelectors" option as described in [this article](vpn-gateway-connect-multiple-policybased-rm-ps.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b24e4-144">您需要 toocreate 順序 tooenable"UsePolicyBasedTrafficSelectors"hello 連線選項中的 IPsec/IKE 原則。</span><span class="sxs-lookup"><span data-stu-id="b24e4-144">You need toocreate an IPsec/IKE policy in order tooenable "UsePolicyBasedTrafficSelectors" option on hello connection.</span></span>

<span data-ttu-id="b24e4-145">下列的 hello 範例指令碼會建立 IPsec/IKE 原則以 hello 下列演算法和參數：</span><span class="sxs-lookup"><span data-stu-id="b24e4-145">hello sample script below creates an IPsec/IKE policy with hello following algorithms and parameters:</span></span>
* <span data-ttu-id="b24e4-146">IKEv2：AES256、SHA384、DHGroup24</span><span class="sxs-lookup"><span data-stu-id="b24e4-146">IKEv2: AES256, SHA384, DHGroup24</span></span>
* <span data-ttu-id="b24e4-147">IPsec：AES256、SHA1、PFS24、SA 存留期 7200 秒和 20480000KB (20GB)</span><span class="sxs-lookup"><span data-stu-id="b24e4-147">IPsec: AES256, SHA1, PFS24, SA Lifetime 7200 seconds & 20480000KB (20GB)</span></span>

<span data-ttu-id="b24e4-148">然後 hello 原則套用，並且在 hello 連接上啟用 「 UesPolicyBasedTrafficSelectors"。</span><span class="sxs-lookup"><span data-stu-id="b24e4-148">It then applies hello policy and enables "UesPolicyBasedTrafficSelectors" on hello connection.</span></span>

```powershell
$ipsecpolicy5 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption AES256 -IpsecIntegrity SHA1 -PfsGroup PFS24 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 20480000

$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw  = Get-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $False -IpsecPolicies $ipsecpolicy5 -UsePolicyBasedTrafficSelectors $True
```

### <span data-ttu-id="b24e4-149"><a name ="bgp"></a>[選擇性] 在 S2S VPN 連線使用 BGP</span><span class="sxs-lookup"><span data-stu-id="b24e4-149"><a name ="bgp"></a>[Optional] Use BGP on S2S VPN connection</span></span>
<span data-ttu-id="b24e4-150">您可以選擇性地在 hello 連接上使用 BGP。</span><span class="sxs-lookup"><span data-stu-id="b24e4-150">You can optionally use BGP on hello connection.</span></span> <span data-ttu-id="b24e4-151">請參閱[適用於 VPN 閘道的 BGP](vpn-gateway-bgp-resource-manager-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="b24e4-151">See [BGP for VPN gateway](vpn-gateway-bgp-resource-manager-ps.md).</span></span> <span data-ttu-id="b24e4-152">有兩個差異：</span><span class="sxs-lookup"><span data-stu-id="b24e4-152">There are two differences:</span></span>

<span data-ttu-id="b24e4-153">hello 在內部部署位址前置詞可以是單一主機位址、 hello 內部 BGP 對等體 IP 位址：</span><span class="sxs-lookup"><span data-stu-id="b24e4-153">hello on-premises address prefixes can be a single host address, hello on-premises BGP peer IP address:</span></span>

```powershell
New-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG1 -Location $Location1 -GatewayIpAddress $LNGIP5 -AddressPrefix $LNGPrefix50 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP5
```

<span data-ttu-id="b24e4-154">您必須設定 「-EnableBGP 」 太 $True 建立 hello 連接時：</span><span class="sxs-lookup"><span data-stu-id="b24e4-154">You must set "-EnableBGP" too$True when creating hello connection:</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $True
```

## <a name="next-steps"></a><span data-ttu-id="b24e4-155">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b24e4-155">Next steps</span></span>
<span data-ttu-id="b24e4-156">請參閱[跨單位和 VNet 對 VNet 連線設定主動-主動 VPN 閘道](vpn-gateway-activeactive-rm-powershell.md)步驟 tooconfigure 主動-主動跨單位和 VNet 對 VNet 連線。</span><span class="sxs-lookup"><span data-stu-id="b24e4-156">See [Configuring Active-Active VPN Gateways for Cross-Premises and VNet-to-VNet Connections](vpn-gateway-activeactive-rm-powershell.md) for steps tooconfigure active-active cross-premises and VNet-to-VNet connections.</span></span>

