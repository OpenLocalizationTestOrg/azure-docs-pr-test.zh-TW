---
title: "在 Azure VPN 閘道上設定 BGP：Resource Manager: PowerShell | Microsoft Docs"
description: "本文將逐步引導您使用 Azure Resource Manager 和 PowerShell 來設定 BGP 與 Azure VPN 閘道。"
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 905b11a7-1333-482c-820b-0fd0f44238e5
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: yushwang
ms.openlocfilehash: a9d13ae6b319e2efa8965dc2955c9b89ac3fd12b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-bgp-on-azure-vpn-gateways-using-powershell"></a>如何 tooconfigure 上使用 PowerShell 的 Azure VPN 閘道的 BGP
本文將告訴您 hello 步驟 tooenable BGP 跨內部部署站台對站 (S2S) VPN 連線和使用 hello Resource Manager 部署模型和 PowerShell 的 VNet 對 VNet 連線。

## <a name="about-bgp"></a>關於 BGP
BGP 是 hello 標準路由通訊協定常用 hello 網際網路 tooexchange 路由和連線資訊中兩個或多個網路之間。 BGP 啟用 hello Azure VPN 閘道和 BGP 對等體或鄰近項目呼叫您在內部部署 VPN 裝置、 tooexchange 「 路由 」，會通知這兩個閘道 hello 可用性，並且連線的前置詞 toogo 透過 hello 閘道或路由器相關。 BGP 也可以啟用傳輸多個網路之間路由傳播路由的 BGP 閘道會從一個 BGP 對等 tooall 學習其他 BGP 對等節點。

請參閱[概觀的 BGP 與 Azure VPN 閘道](vpn-gateway-bgp-overview.md)如需詳細資訊優點 BGP 和 toounderstand hello 技術需求，以及使用 BGP 的考量。

## <a name="getting-started-with-bgp-on-azure-vpn-gateways"></a>開始在 Azure VPN 閘道上使用 BGP

這篇文章會引導您 hello 步驟 toodo hello 下列工作：

* [第 1 部份 - 在 Azure VPN 閘道上啟用 BGP](#enablebgp)
* [第 2 部份 – 建立與 BGP 的跨單位連線](#crossprembgp)
* [第 3 部份 – 建立與 BGP 的 VNet 對 VNet 連線](#v2vbgp)

Hello 指示的每個部分會形成網路連線啟用 BGP 的基本建置組塊。 如果您完成所有三個部分，在您建立 hello 拓樸，hello 下列圖表所示：

![BGP 拓樸](./media/vpn-gateway-bgp-resource-manager-ps/bgp-crosspremv2v.png)

您可以結合部分一起 toobuild 符合您需求的更複雜、 多重躍點，傳輸網路。

## <a name ="enablebgp"></a>第 1 部-設定上 hello Azure VPN 閘道的 BGP
hello 組態步驟將會設定 hello hello Azure VPN 閘道的 BGP 參數 hello 下列圖表所示：

![BGP 閘道](./media/vpn-gateway-bgp-resource-manager-ps/bgp-gateway.png)

### <a name="before-you-begin"></a>開始之前
* 請確認您有 Azure 訂用帳戶。 如果您還沒有 Azure 訂用帳戶，則可以啟用 [MSDN 訂戶權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)或註冊[免費帳戶](https://azure.microsoft.com/pricing/free-trial/)。
* 安裝 hello Azure 資源管理員 PowerShell cmdlet。 如需安裝 hello PowerShell cmdlet 的詳細資訊，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。 

### <a name="step-1---create-and-configure-vnet1"></a>步驟 1 - 建立及設定 VNet1
#### <a name="1-declare-your-variables"></a>1.宣告變數
對於此練習，我們一開始先宣告我們的變數。 hello 下列範例會宣告 hello 針對此練習使用 hello 值的變數。 設定用於生產環境時，請以您自己是確定 tooreplace hello 值。 如果您正在透過 hello 步驟 toobecome 熟悉這種設定，您可以使用這些變數。 修改 hello 變數然後複製並貼到您的 PowerShell 主控台。

```powershell
$Sub1 = "Replace_With_Your_Subcription_Name"
$RG1 = "TestBGPRG1"
$Location1 = "East US"
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
$GWIPName1 = "VNet1GWIP"
$GWIPconfName1 = "gwipconf1"
$Connection12 = "VNet1toVNet2"
$Connection15 = "VNet1toSite5"
```

#### <a name="2-connect-tooyour-subscription-and-create-a-new-resource-group"></a>2.連接 tooyour 訂用帳戶，並建立新的資源群組
toouse hello 資源管理員 cmdlet，請確定切換 tooPowerShell 模式。 如需詳細資訊，請參閱 [搭配使用 Windows PowerShell 與 Resource Manager](../powershell-azure-resource-manager.md)。

開啟 PowerShell 主控台並連接 tooyour 帳戶。 使用下列範例 toohelp 您連接的 hello:

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="3-create-testvnet1"></a>3.建立 TestVNet1
hello 下列範例會建立名為 TestVNet1 三個子網路，一個稱為的 GatewaySubnet、 一個稱為的前端和一個被呼叫後端的虛擬網路。 替代值時，務必一律將您的閘道子網路特定命名為 GatewaySubnet。 如果您將其命名為其他名稱，閘道建立會失敗。

```powershell
$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1 $besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
```

### <a name="step-2---create-hello-vpn-gateway-for-testvnet1-with-bgp-parameters"></a>步驟 2-建立 TestVNet1 hello VPN 閘道的 BGP 參數與
#### <a name="1-create-hello-ip-and-subnet-configurations"></a>1.建立 hello IP 和子網路組態
要求的公用 IP 位址 toobe 配置的 toohello 閘道您將建立您的 VNet。 您也會定義所需的 hello 子網路和 IP 組態。

```powershell
$gwpip1 = New-AzureRmPublicIpAddress -Name $GWIPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic

$vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gwipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName1 -Subnet $subnet1 -PublicIpAddress $gwpip1
```

#### <a name="2-create-hello-vpn-gateway-with-hello-as-number"></a>2.Hello VPN 閘道建立 hello 與數字
建立 TestVNet1 hello 虛擬網路閘道。 BGP TestVNet1 需要路由式 VPN 閘道，以及 hello 加入參數-Asn，tooset hello ASN （AS 號碼）。 如果您未設定 hello ASN 參數，會指派 ASN 65515。 建立閘道可能需要一段 （30 分鐘或更多 toocomplete）。

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gwipconf1 -GatewayType Vpn -VpnType RouteBased -GatewaySku HighPerformance -Asn $VNet1ASN
```

#### <a name="3-obtain-hello-azure-bgp-peer-ip-address"></a>3.取得 hello Azure BGP 對等 IP 位址
一旦建立 hello 閘道之後，您會需要 hello Azure VPN 閘道 tooobtain hello BGP 對等 IP 位址。 這個位址會是需要的 tooconfigure hello Azure VPN 閘道的 BGP 對等內部部署 VPN 裝置為。

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
$vnet1gw.BgpSettingsText
```

hello 最後一個命令會顯示 hello 對應 BGP 設定上 hello Azure VPN 閘道。例如：

```powershell
$vnet1gw.BgpSettingsText
{
    "Asn": 65010,
    "BgpPeeringAddress": "10.12.255.30",
    "PeerWeight": 0
}
```

一旦建立 hello 閘道之後，您可以使用此閘道 tooestablish 跨單位連線或 VNet 對 VNet 連線 bgp。 hello 下列各節逐步解說 hello 步驟 toocomplete hello 練習。

## <a name ="crossprembbgp"></a>第 2 部份 – 建立與 BGP 的跨單位連線

您需要 toocreate 本機網路閘道 toorepresent tooestablish 跨單位連線，在內部部署 VPN 裝置，以及與 hello 本機網路閘道連線 tooconnect hello VPN 閘道。 文章會引導您完成這些步驟時，本文章包含 hello 其他內容需要的 toospecify hello BGP 設定參數。

![跨單位的 BGP](./media/vpn-gateway-bgp-resource-manager-ps/bgp-crossprem.png)

在繼續之前，請確定您已完成本練習的[第 1 部分](#enablebgp)。

### <a name="step-1---create-and-configure-hello-local-network-gateway"></a>步驟 1-建立和設定 hello 區域網路閘道

#### <a name="1-declare-your-variables"></a>1.宣告變數

這個練習會繼續 toobuild hello 組態 hello 圖所示。 為確定 tooreplace 以 hello 的 hello 值的 toouse 您的組態。

```powershell
$RG5 = "TestBGPRG5"
$Location5 = "East US 2"
$LNGName5 = "Site5"
$LNGPrefix50 = "10.52.255.254/32"
$LNGIP5 = "Your_VPN_Device_IP"
$LNGASN5 = 65050
$BGPPeerIP5 = "10.52.255.254"
```

幾個事項 toonote 有關 hello 本機網路閘道參數：

* hello 區域網路閘道可以是 hello 相同或不同的位置和資源群組為 hello VPN 閘道。 此範例會顯示它們位於不同位置的不同資源群組中。
* hello 區域網路閘道所需 toodeclare hello 最小前置詞是 hello 您 BGP 對等 IP 位址的 VPN 裝置上的主機位址。 在此情況下是 "10.52.255.254/32" 的前置詞 /32。
* 提醒您，您必須在內部部署網路與 Azure VNet 之間使用不同的 BGP ASN。 如果它們是 hello 相同，則需要 toochange VNet ASN 在內部部署 VPN 裝置已使用 hello ASN toopeer 與其他 BGP 芳鄰。

在繼續之前，請確認您仍連線的 tooSubscription 1。

#### <a name="2-create-hello-local-network-gateway-for-site5"></a>2.建立 Site5 hello 區域網路閘道

如果它不建立，在建立 hello 區域網路閘道之前，是確定 toocreate hello 資源群組。 請注意 hello 本機網路閘道的 hello 兩個額外的參數： Asn 與 BgpPeerAddress。

```powershell
New-AzureRmResourceGroup -Name $RG5 -Location $Location5

New-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP5 -AddressPrefix $LNGPrefix50 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP5
```

### <a name="step-2---connect-hello-vnet-gateway-and-local-network-gateway"></a>步驟 2-連接 hello VNet 閘道與區域網路閘道

#### <a name="1-get-hello-two-gateways"></a>1.取得 hello 這兩個閘道

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw  = Get-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG5
```

#### <a name="2-create-hello-testvnet1-toosite5-connection"></a>2.建立 hello TestVNet1 tooSite5 連線

在此步驟中，您會從 TestVNet1 tooSite5 建立 hello 連線。 您必須指定"-EnableBGP $True"tooenable BGP 此連線。 如同先前討論，很可能 toohave BGP 和非 BGP 連接 hello 相同 Azure VPN 閘道。 除非 hello 連接屬性中啟用 BGP，Azure 將不會啟用 BGP 此連線的即使已設定兩個閘道的 BGP 參數。

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $True
```

hello 下列範例會列出您針對此練習在內部部署 VPN 裝置輸入 hello BGP 組態區段的 hello 參數：

```

- Site5 ASN            : 65050
- Site5 BGP IP         : 10.52.255.254
- Prefixes tooannounce : (for example) 10.51.0.0/16 and 10.52.0.0/16
- Azure VNet ASN       : 65010
- Azure VNet BGP IP    : 10.12.255.30
- Static route         : Add a route for 10.12.255.30/32, with nexthop being hello VPN tunnel interface on your device
- eBGP Multihop        : Ensure hello "multihop" option for eBGP is enabled on your device if needed
```

一旦建立之後 IPsec 連線 hello 幾分鐘的時間和 hello BGP 對等互連工作階段開始之後建立 hello 連接。

## <a name ="v2vbgp"></a>第 3 部份 – 建立與 BGP 的 VNet 對 VNet 連線

本節將 VNet 對 VNet 連線 bgp，新增 hello 下列圖表所示：

![VNet 對 VNet 的 BGP](./media/vpn-gateway-bgp-resource-manager-ps/bgp-vnet2vnet.png)

下列指示的 hello 繼續 hello 上一個步驟。 您必須先完成[第 I 部分](#enablebgp)toocreate 並設定 TestVNet1 hello bgp 的 VPN 閘道。 

### <a name="step-1---create-testvnet2-and-hello-vpn-gateway"></a>步驟 1-建立 TestVNet2 和 hello VPN 閘道

它是重要 toomake 確定 hello 新的虛擬網路，TestVNet2，hello IP 位址空間不與任何 VNet 範圍重疊。

在此範例中，hello 虛擬網路屬於 toohello 相同訂用帳戶。 您可以設定不同訂用帳戶之間的 VNet 對 VNet 連線。 如需詳細資訊，請參閱[設定 VNet 對 VNet 連線](vpn-gateway-vnet-vnet-rm-ps.md)。 請確定您新增 hello"的 EnableBgp $True 」 時建立 hello 連線 tooenable BGP。

#### <a name="1-declare-your-variables"></a>1.宣告變數

為確定 tooreplace 以 hello 的 hello 值的 toouse 您的組態。

```powershell
$RG2 = "TestBGPRG2"
$Location2 = "West US"
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
$GWIPName2 = "VNet2GWIP"
$GWIPconfName2 = "gwipconf2"
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

#### <a name="3-create-hello-vpn-gateway-for-testvnet2-with-bgp-parameters"></a>3.建立 TestVNet2 hello VPN 閘道的 BGP 參數與

要求的公用 IP 位址 toobe 配置的 toohello 閘道您將為您的 VNet 建立並定義所需的 hello 子網路和 IP 組態。

```powershell
$gwpip2    = New-AzureRmPublicIpAddress -Name $GWIPName2 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic

$vnet2     = Get-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2
$subnet2   = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet2
$gwipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName2 -Subnet $subnet2 -PublicIpAddress $gwpip2
```

Hello VPN 閘道建立 hello 與數字。 您必須在 Azure VPN 閘道上，以覆寫 hello 預設 ASN。 hello Asn hello 連線 Vnet 必須是不同 tooenable BGP 和傳輸路由。

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2 -Location $Location2 -IpConfigurations $gwipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku Standard -Asn $VNet2ASN
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

在此步驟中，您建立從 TestVNet1 tooTestVNet2 hello 連線與 hello 連線從 TestVNet2 tooTestVNet1。

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection12 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet2gw -Location $Location1 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection21 -ResourceGroupName $RG2 -VirtualNetworkGateway1 $vnet2gw -VirtualNetworkGateway2 $vnet1gw -Location $Location2 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True
```

> [!IMPORTANT]
> 這兩個連接是確定 tooenable BGP。
> 
> 

完成這些步驟之後，會在幾分鐘後建立 hello 連線。 hello BGP 對等互連工作階段已啟動，一旦完成 hello VNet 對 VNet 連線。

如果您已完成此練習中的所有三個部分，您已建立下列 網路拓樸 hello:

![VNet 對 VNet 的 BGP](./media/vpn-gateway-bgp-resource-manager-ps/bgp-crosspremv2v.png)

## <a name="next-steps"></a>後續步驟

一旦完成您的連線，您可以將虛擬機器 tooyour 虛擬網路。 請參閱 [建立網站的虛擬機器](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 以取得相關步驟。
