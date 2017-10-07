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
# <a name="overview-of-3rd-party-vpn-device-configurations"></a>第三方 VPN 裝置組態的概觀
本文章提供連接 tooAzure VPN 閘道的內部部署 VPN 裝置組態的概觀。 hello 範例 Azure 虛擬網路和 VPN 閘道安裝程式將會使用的 tooconnect toodifferent 在內部部署 VPN 裝置以 hello 相同的參數。

## <a name="device-requirements"></a>裝置需求
Azure VPN 閘道會針對 S2S VPN 通道使用標準的 IPsec/IKE 通訊協定組合。 請參閱太[關於 VPN 裝置](vpn-gateway-about-vpn-devices.md)hello 詳細的 IPsec/IKE 通訊協定參數和 Azure VPN 閘道的預設密碼編譯演算法。 中所述，您可以選擇指定的密碼編譯演算法和金鑰長度為特定連線的 hello 確切組合[有關密碼編譯需求](vpn-gateway-about-compliance-crypto.md)。

## <a name ="singletunnel"></a>單一 VPN 通道
hello 第一個拓撲是由單一的 S2S VPN 通道，Azure VPN 閘道與內部部署 VPN 裝置之間所組成。 您可以選擇性地跨 hello VPN 通道設定 BGP。

![單一通道](./media/vpn-gateway-3rdparty-device-config-overview/singletunnel.png)

請參閱太[設定站對站連線](vpn-gateway-howto-site-to-site-resource-manager-portal.md)如需詳細的逐步指引。 hello 下列各節列出 hello 參數，並提供您快速入門範例 PowerShell 指令碼 toohelp。

### <a name="network-and-vpn-gateway-information"></a>網路和 VPN 閘道資訊
本節列出 hello 參數，如上述的 hello 範例。

| **參數**                | **值**                    |
| ---                          | ---                          |
| VNet 位址首碼        | 10.11.0.0/16<br>10.12.0.0/16 |
| Azure VPN 閘道 IP         | Azure VPN 閘道 IP         |
| 內部部署位址首碼 | 10.51.0.0/16<br>10.52.0.0/16 |
| 內部部署 VPN 裝置 IP    | 內部部署 VPN 裝置 IP    |
| *VNet BGP ASN                | 65010                        |
| *Azure BGP 對等 IP           | 10.12.255.30                 |
| *內部部署 BGP ASN         | 65050                        |
| *內部部署 BGP 對等 IP     | 10.52.255.254                |

* (*) 僅適用於 BGP 的選擇性參數

### <a name="sample-powershell-script"></a>範例 PowerShell 指令碼
[建立 S2S VPN 連線使用 PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md) hello 詳細指示。 本節提供範例指令碼 tooget 您已啟動。

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

### <a name ="policybased"></a> [選擇性] 搭配 "UsePolicyBasedTrafficSelectors" 使用自訂的 IPsec/IKE 原則
如果您的 VPN 裝置不支援 「 任何-到-any"流量選取器 （路由-基礎/VTI 為基礎的組態），您將需要 toocreate 自訂 IPsec/IKE 原則和設定 「 UsePolicyBasedTrafficSelectors"選項中所述[這篇文章](vpn-gateway-connect-multiple-policybased-rm-ps.md).

> [!IMPORTANT]
> 您需要 toocreate 順序 tooenable"UsePolicyBasedTrafficSelectors"hello 連線選項中的 IPsec/IKE 原則。

下列的 hello 範例指令碼會建立 IPsec/IKE 原則以 hello 下列演算法和參數：
* IKEv2：AES256、SHA384、DHGroup24
* IPsec：AES256、SHA1、PFS24、SA 存留期 7200 秒和 20480000KB (20GB)

然後 hello 原則套用，並且在 hello 連接上啟用 「 UesPolicyBasedTrafficSelectors"。

```powershell
$ipsecpolicy5 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption AES256 -IpsecIntegrity SHA1 -PfsGroup PFS24 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 20480000

$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw  = Get-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $False -IpsecPolicies $ipsecpolicy5 -UsePolicyBasedTrafficSelectors $True
```

### <a name ="bgp"></a>[選擇性] 在 S2S VPN 連線使用 BGP
您可以選擇性地在 hello 連接上使用 BGP。 請參閱[適用於 VPN 閘道的 BGP](vpn-gateway-bgp-resource-manager-ps.md)。 有兩個差異：

hello 在內部部署位址前置詞可以是單一主機位址、 hello 內部 BGP 對等體 IP 位址：

```powershell
New-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG1 -Location $Location1 -GatewayIpAddress $LNGIP5 -AddressPrefix $LNGPrefix50 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP5
```

您必須設定 「-EnableBGP 」 太 $True 建立 hello 連接時：

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $True
```

## <a name="next-steps"></a>後續步驟
請參閱[跨單位和 VNet 對 VNet 連線設定主動-主動 VPN 閘道](vpn-gateway-activeactive-rm-powershell.md)步驟 tooconfigure 主動-主動跨單位和 VNet 對 VNet 連線。

