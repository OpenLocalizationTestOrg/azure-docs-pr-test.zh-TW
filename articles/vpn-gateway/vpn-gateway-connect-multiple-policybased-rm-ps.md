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
# <a name="connect-azure-vpn-gateways-toomultiple-on-premises-policy-based-vpn-devices-using-powershell"></a>連接 Azure VPN 閘道 toomultiple 內部以原則為基礎的 VPN 裝置使用 PowerShell

這篇文章可協助您設定 Azure 路由式 VPN 閘道 tooconnect toomultiple 在內部部署原則式 VPN 裝置運用 S2S VPN 連線自訂 IPsec/IKE 原則。

## <a name="about-policy-based-and-route-based-vpn-gateways"></a>關於以原則為基礎的 VPN 閘道和以路由為基礎的 VPN 閘道

原則-*與*路由式 VPN 裝置的 hello IPsec 流量選取器的連接上設定的方式不同：

* **以原則為基礎**VPN 裝置使用的前置詞，從這兩種方式的流量會加密/解密透過 IPsec 通道的網路 toodefine hello 組合。 它通常內建在執行封包篩選的防火牆裝置上。 IPsec 通道加密和解密會新增 toohello 封包篩選處理引擎。
* **路由式**VPN 裝置使用任何-any （萬用字元） 流量的選取器，可讓路由轉送/資料表和資料流導向 toodifferent IPsec 通道。 它通常內建在路由器平台上，其中，每個 IPsec 通道都會建模為網路介面或 VTI (虛擬通道介面)。

hello 圖反白顯示 hello 兩個模型：

### <a name="policy-based-vpn-example"></a>以原則為基礎的 VPN 範例
![以原則為基礎](./media/vpn-gateway-connect-multiple-policybased-rm-ps/policybasedmultisite.png)

### <a name="route-based-vpn-example"></a>以路由為基礎的 VPN 範例
![以路由為基礎](./media/vpn-gateway-connect-multiple-policybased-rm-ps/routebasedmultisite.png)

### <a name="azure-support-for-policy-based-vpn"></a>以原則為基礎的 VPN 的 Azure 支援
Azure 目前支援兩種 VPN 閘道模式：以路由為基礎的 VPN 閘道和以原則為基礎的 VPN 閘道。 它們內建在不同內部平台上，因而導致不同的規格：

|                          | **PolicyBased VPN 閘道** | **RouteBased VPN 閘道**               |
| ---                      | ---                         | ---                                      |
| **Azure 閘道 SKU**    | 基本                       | Basic、Standard、HighPerformance         |
| **IKE 版本**          | IKEv1                       | IKEv2                                    |
| **最大S2S 連線** | **1**                       | 基本/標準：10<br> 高效能：30 |
|                          |                             |                                          |

Hello 自訂 IPsec/IKE 原則，您現在可以設定 Azure 路由式 VPN 閘道 toouse 前置詞為基礎的傳輸選取器選項"**PolicyBasedTrafficSelectors**"，tooconnect tooon 內部以原則為基礎的 VPN 裝置。 這項功能可讓您從一個 Azure 虛擬網路的 tooconnect 和 VPN 閘道 toomultiple 內部原則式 VPN/防火牆裝置，從 hello 目前 Azure 原則式 VPN 閘道移除 hello 單一連線限制。

> [!IMPORTANT]
> 1. tooenable 您在內部以原則為基礎的 VPN 裝置必須支援這種連線能力， **IKEv2** tooconnect toohello Azure 路由式 VPN 閘道。 確認您的 VPN 裝置規格。
> 2. 使用這項機制透過以原則為基礎的 VPN 裝置連接的 hello 在內部部署網路只能連接 toohello Azure 虛擬網路。**它們無法傳輸 tooother 在內部部署網路，或透過虛擬網路 hello 相同 Azure VPN 閘道**。
> 3. hello 組態選項是 hello 自訂 IPsec/IKE 連接原則的一部分。 如果您啟用 hello 以原則為基礎的傳輸選取器選項，您必須指定 hello 完整的原則 （IPsec/IKE 加密及完整性演算法、 金鑰長度和 SA 存留時間）。

hello 下列圖表顯示為何透過 Azure VPN 閘道的傳輸路由不能使用 hello 以原則為基礎的選項：

![以原則為基礎的傳輸](./media/vpn-gateway-connect-multiple-policybased-rm-ps/policybasedtransit.png)

Hello 圖表所示，hello Azure VPN 閘道有流量從 hello 虛擬網路 tooeach hello 在內部部署網路首碼，但不 hello 跨連接前置詞的選取器。 例如，在內部部署站台 2，3，站台與站台 4 可以每個分別通訊 tooVNet1，但無法連接透過 hello Azure VPN 閘道 tooeach 其他。 hello 圖表會顯示 hello 跨連接都無法使用此設定下 hello Azure VPN 閘道的流量選取器。

## <a name="configure-policy-based-traffic-selectors-on-a-connection"></a>在連線上設定以原則為基礎的流量選取器

hello 中這篇文章依照指示 hello 相同範例中所述[設定 IPsec/IKE S2S 或 VNet 對 VNet 連線原則](vpn-gateway-ipsecikepolicy-rm-powershell.md)tooestablish S2S VPN 連線。 Hello 下列圖表所示：

![s2s-policy](./media/vpn-gateway-connect-multiple-policybased-rm-ps/s2spolicypb.png)

hello 工作流程 tooenable 這種連線能力：
1. 建立 hello 虛擬網路、 VPN 閘道和跨單位連線的區域網路閘道
2. 建立 IPsec/IKE 原則
3. 當您建立 S2S 或 VNet 對 VNet 連線，套用 hello 原則和**啟用 hello 以原則為基礎的傳輸選取器**hello 連接上
4. 如果已經建立 hello 連線，您可以套用或更新 hello 原則 tooan 現有連線

## <a name="enable-policy-based-traffic-selectors-on-a-connection"></a>在連線上啟用以原則為基礎的流量選取器

請確定您已完成[hello 設定 IPsec/IKE 原則文件的組件 3](vpn-gateway-ipsecikepolicy-rm-powershell.md)對此區段。 下列範例會使用 hello hello 相同的參數和步驟：

### <a name="step-1---create-hello-virtual-network-vpn-gateway-and-local-network-gateway"></a>步驟 1-建立 hello 虛擬網路、 VPN 閘道與區域網路閘道

#### <a name="1-declare-your-variables--connect-tooyour-subscription"></a>1.宣告變數和連接 tooyour 訂用帳戶
對於此練習，我們一開始先宣告我們的變數。 設定用於生產環境時，請以您自己是確定 tooreplace hello 值。

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
toouse hello 資源管理員 cmdlet，請確定切換 tooPowerShell 模式。 如需詳細資訊，請參閱 [搭配使用 Windows PowerShell 與 Resource Manager](../powershell-azure-resource-manager.md)。

開啟 PowerShell 主控台並連接 tooyour 帳戶。 使用下列範例 toohelp 您連接的 hello:

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="2-create-hello-virtual-network-vpn-gateway-and-local-network-gateway"></a>2.建立 hello 虛擬網路、 VPN 閘道與區域網路閘道
下列範例中的 hello 建立 hello 虛擬網路，TestVNet1 三個的子網路與 hello VPN 閘道。 替代值時，務必一律將您的閘道子網路特定命名為 GatewaySubnet。 如果您將其命名為其他名稱，閘道建立會失敗。

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

### <a name="step-2---create-a-s2s-vpn-connection-with-an-ipsecike-policy"></a>步驟 2 - 使用 IPsec/IKE 原則建立 S2S VPN 連線

#### <a name="1-create-an-ipsecike-policy"></a>1.建立 IPsec/IKE 原則

> [!IMPORTANT]
> 您需要 toocreate 順序 tooenable"UsePolicyBasedTrafficSelectors"hello 連線選項中的 IPsec/IKE 原則。

hello 下列範例會建立一個 IPsec/IKE 原則使用這些演算法和參數：
* IKEv2：AES256、SHA384、DHGroup24
* IPsec：AES256、SHA256、PFS24、SA 存留期 3600 秒和 2048KB

```powershell
$ipsecpolicy6 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption AES256 -IpsecIntegrity SHA256 -PfsGroup PFS24 -SALifeTimeSeconds 3600 -SADataSizeKilobytes 2048
```

#### <a name="2-create-hello-s2s-vpn-connection-with-policy-based-traffic-selectors-and-ipsecike-policy"></a>2.使用以原則為基礎的傳輸選取器與 IPsec/IKE 原則建立 hello S2S VPN 連線
建立 S2S VPN 連線並套用 hello hello 先前步驟中建立的 IPsec/IKE 原則。 請留意 hello 額外的參數"-UsePolicyBasedTrafficSelectors $True 」 可讓以原則為基礎的流量 hello 連接上的選取器。

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng6 = Get-AzureRmLocalNetworkGateway  -Name $LNGName6 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng6 -Location $Location1 -ConnectionType IPsec -UsePolicyBasedTrafficSelectors $True -IpsecPolicies $ipsecpolicy6 -SharedKey 'AzureA1b2C3'
```

完成 hello 步驟之後，將會使用 hello IPsec/IKE 原則定義，hello S2S VPN 連線，並將其啟用以原則為基礎的流量 hello 連接上的選取器中。 您可以重複相同步驟 tooadd 多個連線 tooadditional 內部以原則為基礎的 VPN 裝置從 hello hello 相同 Azure VPN 閘道。

## <a name="update-policy-based-traffic-selectors-for-a-connection"></a>更新連線的以原則為基礎的流量選取器
hello 最後一節顯示如何 tooupdate hello 以原則為基礎的傳輸選取器選項現有 S2S VPN 連線。

### <a name="1-get-hello-connection"></a>1.取得 hello 連線
收到 hello 連接資源。

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1
```

### <a name="2-check-hello-policy-based-traffic-selectors-option"></a>2.核取 hello 以原則為基礎的傳輸選取器選項
hello 下列一行顯示 hello 以原則為基礎的傳輸選取器是否會用於 hello 連接：

```powershell
$connection6.UsePolicyBasedTrafficSelectors
```

如果 hello 一行傳回的"**True**"，然後以原則為基礎的傳輸選取器會在 hello 連線上設定; 否則會傳回"**False**。 」

### <a name="3-update-hello-policy-based-traffic-selectors-on-a-connection"></a>3.更新的連接上的 hello 以原則為基礎的傳輸選取器
一旦您取得 hello 連接資源，您可以啟用或停用 hello 選項。

#### <a name="disable-usepolicybasedtrafficselectors"></a>停用 UsePolicyBasedTrafficSelectors
hello 下列範例會停用 hello 以原則為基礎的傳輸選取器選項，但保留 hello IPsec/IKE 原則保持不變：

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -UsePolicyBasedTrafficSelectors $False
```

#### <a name="enable-usepolicybasedtrafficselectors"></a>啟用 UsePolicyBasedTrafficSelectors
hello 下列範例會啟用 hello 以原則為基礎的傳輸選取器選項，但保留 hello IPsec/IKE 原則保持不變：

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -UsePolicyBasedTrafficSelectors $True
```

## <a name="next-steps"></a>後續步驟
一旦完成您的連線，您可以將虛擬機器 tooyour 虛擬網路。 請參閱 [建立網站的虛擬機器](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 以取得相關步驟。

如需自訂 IPsec/IKE 原則的詳細資訊，也請檢閱[設定 S2S VPN 或 VNet 對 VNet 連線的 IPsec/IKE 原則](vpn-gateway-ipsecikepolicy-rm-powershell.md)。
