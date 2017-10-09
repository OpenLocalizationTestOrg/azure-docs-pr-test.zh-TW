---
title: "設定 VPN 閘道的主動-主動 S2S VPN 連線：Azure Resource Manager: PowerShell | Microsoft Docs"
description: "本文將逐步引導您使用 Azure Resource Manager 和 PowerShell 來設定與 Azure VPN 閘道的主動-主動連線。"
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 238cd9b3-f1ce-4341-b18e-7390935604fa
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/16/2017
ms.author: yushwang
ms.openlocfilehash: 964eedc7698e42bf0e082f0105845f2a339daf57
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-active-active-s2s-vpn-connections-with-azure-vpn-gateways"></a>設定 Azure VPN 閘道的主動-主動 S2S VPN 連線

這篇文章會引導您完成 hello 步驟 toocreate 主動-主動跨內部部署和使用 hello Resource Manager 部署模型和 PowerShell 的 VNet 對 VNet 連線。

## <a name="about-highly-available-cross-premises-connections"></a>關於高可用性跨單位連線
tooachieve 高可用性的跨單位和 VNet 對 VNet 連線能力，您應該部署多個 VPN 閘道，並建立您的網路與 Azure 之間的多個平行連接。 如需連線能力選項和拓撲的概觀，請參閱 [高可用性跨單位和 VNet 對 VNet 連線能力](vpn-gateway-highlyavailable.md) 。

本文章提供 hello 指示 tooset 主動-主動設定跨單位 VPN 連線和兩個虛擬網路之間的主動-主動連線：

* [第 1 部分 - 建立 Azure VPN 閘道並將它設定為主動-主動模式](#aagateway)
* [第 2 部分 - 建立主動-主動跨單位連線](#aacrossprem)
* [第 3 部分 - 建立主動-主動 VNet 對 VNet 連線](#aav2v)
* [第 4 部分 - 更新主動-主動和作用中-待命之間的現有閘道](#aaupdate)

您可以結合這些一起 toobuild 符合您需求的更複雜、 高可用性的網路拓撲。

> [!IMPORTANT]
> 請注意該 hello 主動 / 主動模式會使用下列 Sku 的唯一 hello: 
  * VpnGw1、VpnGw2、VpnGw3
  * HighPerformance (對於舊版 SKU)
> 
> 

## <a name ="aagateway"></a>第 1 部分 - 建立並設定主動-主動 VPN 閘道
hello 下列步驟將在主動 / 主動模式中設定 Azure VPN 閘道。 hello hello 主動-主動和作用中-待命閘道之間的主要差異：

* 您需要兩個公用 IP 位址與 toocreate 兩個閘道 IP 設定
* 您需要設定 hello EnableActiveActiveFeature 旗標
* hello 閘道 SKU 必須 VpnGw1、 VpnGw2、 VpnGw3 或高效能的分散式 (舊版 SKU)。

hello 其他屬性會 hello 與 hello 非主動-主動閘道相同。 

### <a name="before-you-begin"></a>開始之前
* 請確認您有 Azure 訂用帳戶。 如果您還沒有 Azure 訂用帳戶，則可以啟用 [MSDN 訂戶權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)或註冊[免費帳戶](https://azure.microsoft.com/pricing/free-trial/)。
* 您將需要 tooinstall hello Azure 資源管理員 PowerShell cmdlet。 請參閱[Azure PowerShell 概觀](/powershell/azure/overview)如需安裝 hello PowerShell cmdlet 的詳細資訊。

### <a name="step-1---create-and-configure-vnet1"></a>步驟 1 - 建立及設定 VNet1
#### <a name="1-declare-your-variables"></a>1.宣告變數
對於此練習，我們一開始先宣告我們的變數。 下列的 hello 範例宣告 hello 針對此練習使用 hello 值的變數。 設定用於生產環境時，請以您自己是確定 tooreplace hello 值。 如果您正在透過 hello 步驟 toobecome 熟悉這種設定，您可以使用這些變數。 修改 hello 變數然後複製並貼到您的 PowerShell 主控台。

```powershell
$Sub1 = "Ross"
$RG1 = "TestAARG1"
$Location1 = "West US"
$VNetName1 = "TestVNet1"
$FESubName1 = "FrontEnd"
$BESubName1 = "Backend"
$GWSubName1 = "GatewaySubnet"
$VNetPrefix11 = "10.11.0.0/16"
$VNetPrefix12 = "10.12.0.0/16"
$FESubPrefix1 = "10.11.0.0/24"
$BESubPrefix1 = "10.12.0.0/24"
$GWSubPrefix1 = "10.12.255.0/27"
$VNet1ASN = 65010
$DNS1 = "8.8.8.8"
$GWName1 = "VNet1GW"
$GW1IPName1 = "VNet1GWIP1"
$GW1IPName2 = "VNet1GWIP2"
$GW1IPconf1 = "gw1ipconf1"
$GW1IPconf2 = "gw1ipconf2"
$Connection12 = "VNet1toVNet2"
$Connection151 = "VNet1toSite5_1"
$Connection152 = "VNet1toSite5_2"
```

#### <a name="2-connect-tooyour-subscription-and-create-a-new-resource-group"></a>2.連接 tooyour 訂用帳戶，並建立新的資源群組
請確定切換 tooPowerShell 模式 toouse hello 資源管理員 cmdlet。 如需詳細資訊，請參閱 [搭配使用 Windows PowerShell 與 Resource Manager](../powershell-azure-resource-manager.md)。

開啟 PowerShell 主控台並連接 tooyour 帳戶。 使用下列範例 toohelp 您連接的 hello:

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="3-create-testvnet1"></a>3.建立 TestVNet1
hello 下面範例會建立名為 TestVNet1 三個子網路，一個稱為的 GatewaySubnet、 一個稱為的前端和一個被呼叫後端的虛擬網路。 替代值時，務必一律將您的閘道子網路特定命名為 GatewaySubnet。 如果您將其命名為其他名稱，閘道將會建立失敗。

```powershell
$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1
$besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
```

### <a name="step-2---create-hello-vpn-gateway-for-testvnet1-with-active-active-mode"></a>步驟 2-建立 TestVNet1 hello VPN 閘道，並主動 / 主動模式
#### <a name="1-create-hello-public-ip-addresses-and-gateway-ip-configurations"></a>1.建立 hello 公用 IP 位址和閘道 IP 組態
要求兩個公用 IP 位址 toobe 配置的 toohello 閘道您將建立您的 VNet。 您也會定義 hello 子網路和 IP 所需的設定。

```powershell
$gw1pip1 = New-AzureRmPublicIpAddress -Name $GW1IPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic
$gw1pip2 = New-AzureRmPublicIpAddress -Name $GW1IPName2 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic

$vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gw1ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW1IPconf1 -Subnet $subnet1 -PublicIpAddress $gw1pip1
$gw1ipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW1IPconf2 -Subnet $subnet1 -PublicIpAddress $gw1pip2
```

#### <a name="2-create-hello-vpn-gateway-with-active-active-configuration"></a>2.主動-主動組態建立 hello VPN 閘道
建立 TestVNet1 hello 虛擬網路閘道。 請注意，兩個 GatewayIpConfig 項目，而且 hello EnableActiveActiveFeature 旗標設定。 建立閘道可能需要一段 （45 分鐘或更多 toocomplete）。

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gw1ipconf1,$gw1ipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -Asn $VNet1ASN -EnableActiveActiveFeature -Debug
```

#### <a name="3-obtain-hello-gateway-public-ip-addresses-and-hello-bgp-peer-ip-address"></a>3.取得 hello 閘道的公用 IP 位址和 hello BGP 對等 IP 位址
一旦建立 hello 閘道之後，您必須上 hello Azure VPN 閘道的 tooobtain hello BGP 對等 IP 位址。 這個位址會是需要的 tooconfigure hello Azure VPN 閘道的 BGP 對等內部部署 VPN 裝置為。

```powershell
$gw1pip1 = Get-AzureRmPublicIpAddress -Name $GW1IPName1 -ResourceGroupName $RG1
$gw1pip2 = Get-AzureRmPublicIpAddress -Name $GW1IPName2 -ResourceGroupName $RG1
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
```

使用下列 cmdlet tooshow hello 兩個公用 IP 位址配置給您的 VPN 閘道，以及其對應的 BGP 對等 IP 位址，每個閘道執行個體的 hello:

```powershell

    PS D:\> $gw1pip1.IpAddress
    40.112.190.5

    PS D:\> $gw1pip2.IpAddress
    138.91.156.129

    PS D:\> $vnet1gw.BgpSettingsText
    {
      "Asn": 65010,
      "BgpPeeringAddress": "10.12.255.4,10.12.255.5",
      "PeerWeight": 0
    }
```

hello hello 公用 IP 位址和順序的 hello 閘道器執行個體對應的 BGP 對等互連位址的 hello hello 相同。 在此範例中，hello 閘道具有公用 IP 的 40.112.190.5 VM 將會使用 10.12.255.4 做為其 BGP 對等互連位址，而 138.91.156.129 hello 閘道會使用 10.12.255.5。 當您設定您的內部連線 toohello 主動-主動閘道的 VPN 裝置時需要此資訊。 具有所有位址的 hello 圖表下方顯示 hello 閘道：

![主動-主動閘道](./media/vpn-gateway-activeactive-rm-powershell/active-active-gw.png)

一旦建立 hello 閘道之後，您可以使用此閘道 tooestablish 主動-主動跨內部部署或 VNet 對 VNet 連線。 hello 下列各節將逐步引導 hello 步驟 toocomplete hello 練習。

## <a name ="aacrossprem"></a>第 2 部分 - 建立主動-主動跨單位連線
您需要 toocreate 本機網路閘道 toorepresent tooestablish 跨單位連線，在內部部署 VPN 裝置，並與 hello 本機網路閘道連線 tooconnect hello Azure VPN 閘道。 在此範例中，hello Azure VPN 閘道為主動 / 主動模式。 如此一來，即使有一個內部部署 VPN 裝置 （區域網路閘道） 和一個連接資源，這兩個 Azure VPN 閘道器執行個體將會建立 S2S VPN 通道與 hello 在內部部署裝置。

在繼續之前，請確定您已完成本練習的 [第 1 部分](#aagateway) 。

### <a name="step-1---create-and-configure-hello-local-network-gateway"></a>步驟 1-建立和設定 hello 區域網路閘道
#### <a name="1-declare-your-variables"></a>1.宣告變數
這個練習中，將會繼續 toobuild hello 組態 hello 圖所示。 為確定 tooreplace 以 hello 的 hello 值的 toouse 您的組態。

```powershell
$RG5 = "TestAARG5"
$Location5 = "West US"
$LNGName51 = "Site5_1"
$LNGPrefix51 = "10.52.255.253/32"
$LNGIP51 = "131.107.72.22"
$LNGASN5 = 65050
$BGPPeerIP51 = "10.52.255.253"
```

幾個事項 toonote 有關 hello 本機網路閘道參數：

* hello 區域網路閘道可以是 hello 相同或不同的位置和資源群組為 hello VPN 閘道。 這個範例會顯示它們在不同的資源群組，但在 hello 相同的 Azure 位置。
* 如果只有一個在內部部署 VPN 裝置如上所示，hello 主動-主動連線可使用或不 BGP 通訊協定。 這個範例會使用 BGP hello 跨單位連線。
* 如果已啟用 BGP，您需要 toodeclare hello 本機網路閘道的 hello 前置詞是 hello 您 BGP 對等 IP 位址的 VPN 裝置上的主機位址。 在此情況下是 "10.52.255.253/32" 的前置詞 /32。
* 提醒您，您必須在內部部署網路與 Azure VNet 之間使用不同的 BGP ASN。 如果它們是 hello 相同，則需要 toochange VNet ASN 在內部部署 VPN 裝置已使用 hello ASN toopeer 與其他 BGP 芳鄰。

#### <a name="2-create-hello-local-network-gateway-for-site5"></a>2.建立 Site5 hello 區域網路閘道
您繼續之前，請先確認您仍連線的 tooSubscription 1。 如果尚未建立，請建立 hello 資源群組。

```powershell
New-AzureRmResourceGroup -Name $RG5 -Location $Location5
New-AzureRmLocalNetworkGateway -Name $LNGName51 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP51 -AddressPrefix $LNGPrefix51 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP51
```

### <a name="step-2---connect-hello-vnet-gateway-and-local-network-gateway"></a>步驟 2-連接 hello VNet 閘道與區域網路閘道
#### <a name="1-get-hello-two-gateways"></a>1.取得 hello 這兩個閘道

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw1 = Get-AzureRmLocalNetworkGateway  -Name $LNGName51 -ResourceGroupName $RG5
```

#### <a name="2-create-hello-testvnet1-toosite5-connection"></a>2.建立 hello TestVNet1 tooSite5 連線
在此步驟中，您將建立 hello 連接從 TestVNet1 tooSite5_1 與設定得 「 EnableBGP"$True。

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection151 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw1 -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP True
```

#### <a name="3-vpn-and-bgp-parameters-for-your-on-premises-vpn-device"></a>3.內部部署 VPN 裝置的 VPN 和 BGP 參數
hello 以下範例列出您將針對此練習在內部部署 VPN 裝置 hello BGP 設定區段在輸入的 hello 參數：

    - Site5 ASN            : 65050
    - Site5 BGP IP         : 10.52.255.253
    - 前置詞 tooannounce: （例如） 10.51.0.0/16 和 10.52.0.0/16
    - Azure VNet ASN       : 65010
    - 通道 too40.112.190.5 的 azure VNet BGP IP 1: 10.12.255.4
    - 通道 too138.91.156.129 的 azure VNet BGP IP 2: 10.12.255.5
    - 靜態路由： 目的地 10.12.255.4/32 下, 一個躍點 hello VPN 通道介面 too40.112.190.5 目的地 10.12.255.5/32 下, 一個躍點 hello VPN 通道介面 too138.91.156.129
    - eBGP Multihop： 確定 hello"multihop 」 選項視您的裝置上啟用 eBGP

後幾分鐘的時間和 hello BGP 對等互連工作階段，將會開始建立 hello IPsec 連線之後，應該要建立 hello 連線。 這個範例到目前為止已設定只能有一個在內部部署 VPN 裝置，導致 hello 圖表，如下所示：

![active-active-crossprem](./media/vpn-gateway-activeactive-rm-powershell/active-active.png)

### <a name="step-3---connect-two-on-premises-vpn-devices-toohello-active-active-vpn-gateway"></a>步驟 3-連接兩個內部部署 VPN 裝置 toohello 主動-主動 VPN 閘道
如果您有兩個 VPN 裝置 hello 在相同的內部網路，您可以達到雙重備援連線 hello Azure VPN 閘道 toohello 第二個 VPN 裝置。

#### <a name="1-create-hello-second-local-network-gateway-for-site5"></a>1.建立 Site5 hello 第二個本機網路閘道
請注意，hello 閘道 IP 位址、 位址首碼和 hello 第二個本機網路閘道的 BGP 對等位址不可重疊 hello 先前區域網路閘道使用相同的內部網路。

```powershell
$LNGName52 = "Site5_2"
$LNGPrefix52 = "10.52.255.254/32"
$LNGIP52 = "131.107.72.23"
$BGPPeerIP52 = "10.52.255.254"

New-AzureRmLocalNetworkGateway -Name $LNGName52 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP52 -AddressPrefix $LNGPrefix52 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP52
```

#### <a name="2-connect-hello-vnet-gateway-and-hello-second-local-network-gateway"></a>2.Hello VNet 閘道和 hello 第二個本機網路閘道連接
從 TestVNet1 tooSite5_2 建立 hello 連接，與設定得 「 EnableBGP"$True

```powershell
$lng5gw2 = Get-AzureRmLocalNetworkGateway -Name $LNGName52 -ResourceGroupName $RG5

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection152 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw2 -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP True
```

#### <a name="3-vpn-and-bgp-parameters-for-your-second-on-premises-vpn-device"></a>3.第二個內部部署 VPN 裝置的 VPN 和 BGP 參數
同樣地，以下列出 hello 參數，您會輸入到第二個 VPN 裝置 hello:

```
- Site5 ASN            : 65050
- Site5 BGP IP         : 10.52.255.254
- Prefixes tooannounce : (for example) 10.51.0.0/16 and 10.52.0.0/16
- Azure VNet ASN       : 65010
- Azure VNet BGP IP 1  : 10.12.255.4 for tunnel too40.112.190.5
- Azure VNet BGP IP 2  : 10.12.255.5 for tunnel too138.91.156.129
- Static routes        : Destination 10.12.255.4/32, nexthop hello VPN tunnel interface too40.112.190.5
                         Destination 10.12.255.5/32, nexthop hello VPN tunnel interface too138.91.156.129
- eBGP Multihop        : Ensure hello "multihop" option for eBGP is enabled on your device if needed
```

一旦建立 hello 連線 （通道），您將有雙重備援的 VPN 裝置與連接您的內部部署網路與 Azure 的通道：

![dual-redundancy-crossprem](./media/vpn-gateway-activeactive-rm-powershell/dual-redundancy.png)

## <a name ="aav2v"></a>第 3 部分 - 建立主動-主動 VNet 對 VNet 連線
本節會使用 BGP 建立主動-主動 VNet 對 VNet 連線。 

下列的 hello 指示繼續 hello 上面所列的上一個步驟。 您必須先完成[第 1 部分](#aagateway)toocreate 並設定 TestVNet1 hello bgp 的 VPN 閘道。 

### <a name="step-1---create-testvnet2-and-hello-vpn-gateway"></a>步驟 1-建立 TestVNet2 和 hello VPN 閘道
它是重要 toomake 確定 hello 新的虛擬網路，TestVNet2，hello IP 位址空間不與任何 VNet 範圍重疊。

在此範例中，hello 虛擬網路屬於 toohello 相同訂用帳戶。 您可以設定不同的訂用帳戶; 之間的 VNet 對 VNet 連線請參閱太[設定 VNet 對 VNet 連線](vpn-gateway-vnet-vnet-rm-ps.md)toolearn 更多詳細資訊。 請確定您新增 hello"的 EnableBgp $True 」 時建立 hello 連線 tooenable BGP。

#### <a name="1-declare-your-variables"></a>1.宣告變數
為確定 tooreplace 以 hello 的 hello 值的 toouse 您的組態。

```powershell
$RG2 = "TestAARG2"
$Location2 = "East US"
$VNetName2 = "TestVNet2"
$FESubName2 = "FrontEnd"
$BESubName2 = "Backend"
$GWSubName2 = "GatewaySubnet"
$VNetPrefix21 = "10.21.0.0/16"
$VNetPrefix22 = "10.22.0.0/16"
$FESubPrefix2 = "10.21.0.0/24"
$BESubPrefix2 = "10.22.0.0/24"
$GWSubPrefix2 = "10.22.255.0/27"
$VNet2ASN = 65020
$DNS2 = "8.8.8.8"
$GWName2 = "VNet2GW"
$GW2IPName1 = "VNet2GWIP1"
$GW2IPconf1 = "gw2ipconf1"
$GW2IPName2 = "VNet2GWIP2"
$GW2IPconf2 = "gw2ipconf2"
$Connection21 = "VNet2toVNet1"
$Connection12 = "VNet1toVNet2"
```

#### <a name="2-create-testvnet2-in-hello-new-resource-group"></a>2.建立 TestVNet2 hello 新資源群組中

```powershell
New-AzureRmResourceGroup -Name $RG2 -Location $Location2

$fesub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName2 -AddressPrefix $FESubPrefix2
$besub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName2 -AddressPrefix $BESubPrefix2
$gwsub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName2 -AddressPrefix $GWSubPrefix2

New-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2 -Location $Location2 -AddressPrefix $VNetPrefix21,$VNetPrefix22 -Subnet $fesub2,$besub2,$gwsub2
```

#### <a name="3-create-hello-active-active-vpn-gateway-for-testvnet2"></a>3.建立 TestVNet2 hello 主動-主動 VPN 閘道
要求兩個公用 IP 位址 toobe 配置的 toohello 閘道您將建立您的 VNet。 您也會定義 hello 子網路和 IP 所需的設定。

```powershell
$gw2pip1 = New-AzureRmPublicIpAddress -Name $GW2IPName1 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic
$gw2pip2 = New-AzureRmPublicIpAddress -Name $GW2IPName2 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic

$vnet2 = Get-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2
$subnet2 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet2
$gw2ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW2IPconf1 -Subnet $subnet2 -PublicIpAddress $gw2pip1
$gw2ipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW2IPconf2 -Subnet $subnet2 -PublicIpAddress $gw2pip2
```

建立以 hello hello VPN 閘道，為號碼 」 和 「 hello 」 EnableActiveActiveFeature 」 旗標。 請注意，您必須覆寫 hello 預設 ASN 在您的 Azure VPN 閘道。 hello Asn hello 連線 Vnet 必須是不同 tooenable BGP 和傳輸路由。

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2 -Location $Location2 -IpConfigurations $gw2ipconf1,$gw2ipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -Asn $VNet2ASN -EnableActiveActiveFeature
```

### <a name="step-2---connect-hello-testvnet1-and-testvnet2-gateways"></a>步驟 2-連接 hello TestVNet1 和 TestVNet2 閘道
在此範例中，兩個閘道位於 hello 相同訂用帳戶。 您可以完成此步驟在 hello 同一個 PowerShell 工作階段。

#### <a name="1-get-both-gateways"></a>1.取得兩個閘道
請確定您登入，並連接 tooSubscription 1。

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
$vnet2gw = Get-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2
```

#### <a name="2-create-both-connections"></a>2.建立兩個連線
在此步驟中，您將從 TestVNet2 tooTestVNet1 建立從 TestVNet1 tooTestVNet2 hello 連線與 hello 連線。

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection12 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet2gw -Location $Location1 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection21 -ResourceGroupName $RG2 -VirtualNetworkGateway1 $vnet2gw -VirtualNetworkGateway2 $vnet1gw -Location $Location2 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True
```

> [!IMPORTANT]
> 這兩個連接是確定 tooenable BGP。
> 
> 

完成這些步驟之後，將會建立 hello 連接在幾分鐘的時間，而且 hello BGP 對等互連工作階段會向上一旦完成雙重備援 hello VNet 對 VNet 連線：

![active-active-v2v](./media/vpn-gateway-activeactive-rm-powershell/vnet-to-vnet.png)

## <a name ="aaupdate"></a>第 4 部分 - 更新主動-主動和作用中-待命之間的現有閘道
hello 最後一節將說明您可以設定現有的 Azure VPN 閘道的方式從作用中-待命 tooactive 主動模式，反之亦然。

> [!NOTE]
> 本節包含從標準 tooHighPerformance 已建立 VPN 閘道的 hello 步驟 tooresize 舊版的 SKU (舊 SKU)。 這些步驟，請勿升級 hello 舊舊版 SKU tooone 新 Sku。
> 
> 

### <a name="configure-an-active-standby-gateway-tooactive-active-gateway"></a>設定作用中-待命閘道 tooactive 主動閘道
#### <a name="1-gateway-parameters"></a>1.閘道參數
下列範例中的 hello 轉換主動-主動閘道的作用中-待命閘道。 您需要 toocreate 另一個公用 IP 位址，然後加入第二個閘道 IP 組態。 以下顯示 hello 用的參數：

```powershell
$GWName = "TestVNetAA1GW"
$VNetName = "TestVNetAA1"
$RG = "TestVPNActiveActive01"
$GWIPName2 = "gwpip2"
$GWIPconf2 = "gw1ipconf2"

$vnet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG
$subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet
$gw = Get-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
$location = $gw.Location
```

#### <a name="2-create-hello-public-ip-address-then-add-hello-second-gateway-ip-configuration"></a>2.建立 hello 公用 IP 位址，然後將第二個閘道 IP 設定 hello

```powershell
$gwpip2 = New-AzureRmPublicIpAddress -Name $GWIPName2 -ResourceGroupName $RG -Location $location -AllocationMethod Dynamic
Add-AzureRmVirtualNetworkGatewayIpConfig -VirtualNetworkGateway $gw -Name $GWIPconf2 -Subnet $subnet -PublicIpAddress $gwpip2
```

#### <a name="3-enable-active-active-mode-and-update-hello-gateway"></a>3.啟用主動 / 主動模式和更新 hello 閘道
PowerShell tootrigger hello 實際的更新中，您必須設定 hello 閘道物件。 hello 的 hello 虛擬網路閘道 SKU 必須也變更 （調整大小） tooHighPerformance 先前建立的標準。

```powershell
Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -EnableActiveActiveFeature -GatewaySku HighPerformance
```

這項更新可能需要 30 的 too45 分鐘。

### <a name="configure-an-active-active-gateway-tooactive-standby-gateway"></a>主動-主動閘道 tooactive 待命閘道設定
#### <a name="1-gateway-parameters"></a>1.閘道參數
使用 hello 相同參數做為上述項目，取得 hello IP 設定您想要的 hello 名稱 tooremove。

```powershell
$GWName = "TestVNetAA1GW"
$RG = "TestVPNActiveActive01"

$gw = Get-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
$ipconfname = $gw.IpConfigurations[1].Name
```

#### <a name="2-remove-hello-gateway-ip-configuration-and-disable-hello-active-active-mode"></a>2.請移除 hello 閘道 IP 組態，然後停用 hello 主動 / 主動模式
同樣地，您必須設定 PowerShell tootrigger hello 實際更新 hello 閘道物件。

```powershell
Remove-AzureRmVirtualNetworkGatewayIpConfig -Name $ipconfname -VirtualNetworkGateway $gw
Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -DisableActiveActiveFeature
```

這項更新最多可能需要 too30 太 45 分鐘的時間。

## <a name="next-steps"></a>後續步驟
一旦完成您的連線，您可以將虛擬機器 tooyour 虛擬網路。 請參閱 [建立網站的虛擬機器](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 以取得相關步驟。
