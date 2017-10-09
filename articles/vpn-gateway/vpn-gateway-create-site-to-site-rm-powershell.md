---
title: "連接您在內部部署網路 tooan Azure 虛擬網路： 站對站 VPN: PowerShell |Microsoft 文件"
description: "IPsec 連線從您內部網路 tooan Azure 虛擬網路上的步驟 toocreate hello 公用網際網路。 這些步驟可協助您使用 PowerShell 建立跨單位的站對站 VPN 閘道連線。"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: fcc2fda5-4493-4c15-9436-84d35adbda8e
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/09/2017
ms.author: cherylmc
ms.openlocfilehash: cb8db1dab3a5488816a7f7e8e63908a4c02f55db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vnet-with-a-site-to-site-vpn-connection-using-powershell"></a>使用 PowerShell 建立具有站對站 VPN 連接的 VNet

本文章將示範如何 toouse PowerShell toocreate 網站-站台 VPN 閘道連線在內部網路 toohello VNet。 本文章中的 hello 步驟適用於 toohello Resource Manager 部署模型。 您也可以建立此組態使用不同的部署工具或部署模型，從下列清單中的 hello 選取不同的選項：

> [!div class="op_single_selector"]
> * [Azure 入口網站](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [CLI](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [Azure 入口網站 (傳統)](vpn-gateway-howto-site-to-site-classic-portal.md)
> * [傳統入口網站 (傳統)](vpn-gateway-site-to-site-create.md)
> 
>


站對站 VPN 閘道連線是使用的 tooconnect 您內部網路 tooan Azure 虛擬網路透過 VPN IPsec/IKE （IKEv1 或 IKEv2） 通道。 這種類型的連線需要 VPN 裝置位於內部部署具有對外開放的公用 IP 位址指派 tooit。 如需 VPN 閘道的詳細資訊，請參閱[關於 VPN 閘道](vpn-gateway-about-vpngateways.md)。

![站對站 VPN 閘道跨單位連線圖表](./media/vpn-gateway-create-site-to-site-rm-powershell/site-to-site-diagram.png)

## <a name="before"></a>開始之前

請確認您已符合下列準則，開始您的組態之前 hello:

* 請確定您擁有相容的 VPN 裝置和人能夠 tooconfigure 它。 如需相容 VPN 裝置和裝置組態的詳細資訊，請參閱[關於 VPN 裝置](vpn-gateway-about-vpn-devices.md)。
* 確認您的 VPN 裝置有對外開放的公用 IPv4 位址。 此 IP 位址不能位於 NAT 後方。
* 如果您不熟悉 hello IP 位址範圍位於內部網路組態，您需要 toocoordinate 的人可以為您提供這些詳細資料。 當您建立此設定時，您必須指定 hello IP 位址範圍前置詞，則 Azure 會路由傳送 tooyour 在內部部署位置。 無 hello 的內部部署網路的子網路可以透過圈具有您想要 tooconnect hello 虛擬網路子網路。
* 安裝 hello hello Azure 資源管理員的 PowerShell 指令程式最新版本。 PowerShell 指令程式會經常更新，您通常需要 tooupdate 您 PowerShell cmdlet tooget hello 最新功能的功能。 如果您沒有更新您的 PowerShell cmdlet，指定 hello 值可能會失敗。 請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)如需有關下載和安裝 PowerShell cmdlet。

### <a name="example"></a>範例值

本文章中的 hello 範例會使用下列值的 hello。 您可以使用這些值 toocreate 測試環境中，或參閱 toothem toobetter 了解這篇文章中的 hello 範例。

```
#Example values

VnetName                = TestVNet1
ResourceGroup           = TestRG1
Location                = East US 
AddressSpace            = 10.11.0.0/16 
SubnetName              = Subnet1 
Subnet                  = 10.11.1.0/28 
GatewaySubnet           = 10.11.0.0/27
LocalNetworkGatewayName = Site2
LNG Public IP           = <VPN device IP address> 
Local Address Prefixes  = 10.0.0.0/24, 20.0.0.0/24
Gateway Name            = VNet1GW
PublicIP                = VNet1GWIP
Gateway IP Config       = gwipconfig1 
VPNType                 = RouteBased 
GatewayType             = Vpn 
ConnectionName          = VNet1toSite2

```


## <a name="Login"></a>1.連接 tooyour 訂用帳戶

[!INCLUDE [PowerShell login](../../includes/vpn-gateway-ps-login-include.md)]

## <a name="VNet"></a>2.建立虛擬網路和閘道器子網路

如果您還沒有虛擬網路，請建立一個。 當建立虛擬網路，請確定 hello 您指定的位址空間不將任何您已在內部部署網路的 hello 位址空間重疊。

[!INCLUDE [About gateway subnets](../../includes/vpn-gateway-about-gwsubnet-include.md)]

[!INCLUDE [No NSG warning](../../includes/vpn-gateway-no-nsg-include.md)]

### <a name="vnet"></a>toocreate 虛擬網路和閘道子網路

此範例會建立虛擬網路和閘道子網路。 如果您已經有虛擬網路，您需要閘道子網路，請參閱 tooadd [tooadd 閘道子網路 tooa 虛擬網路已經建立](#gatewaysubnet)。

建立資源群組：

```powershell
New-AzureRmResourceGroup -Name TestRG1 -Location 'East US'
```

建立虛擬網路。

1. 設定 hello 變數。

  ```powershell
  $subnet1 = New-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.11.0.0/27
  $subnet2 = New-AzureRmVirtualNetworkSubnetConfig -Name 'Subnet1' -AddressPrefix 10.11.1.0/28
  ```
2. 建立 hello VNet。

  ```powershell
  New-AzureRmVirtualNetwork -Name TestVNet1 -ResourceGroupName TestRG1 `
  -Location 'East US' -AddressPrefix 10.11.0.0/16 -Subnet $subnet1, $subnet2
  ```

### <a name="gatewaysubnet"></a>tooadd 閘道子網路 tooa 虛擬網路已經建立

1. 設定 hello 變數。

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG1 -Name TestVet1
  ```
2. 建立 hello 閘道子網路。

  ```powershell
  Add-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.11.0.0/27 -VirtualNetwork $vnet
  ```
3. 將 hello 組態設定。

  ```powershell
  Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```

## 3.<a name="localnet"></a>建立 hello 區域網路閘道

hello 區域網路閘道通常是指 tooyour 在內部部署位置。 您提供 hello 站台的名稱之 Azure 可以參考 tooit，然後指定 hello IP 位址的 hello 在內部部署 VPN 裝置 toowhich 中，您將建立連接。 您也指定 hello 而必須路由傳送透過 hello VPN 閘道 toohello VPN 裝置 IP 位址首碼。 您指定的 hello 位址前置詞是在內部部署網路上的 hello 前置詞。 如果您在內部部署網路變更時，您可以輕鬆地更新 hello 前置詞。

使用下列值的 hello:

* hello *GatewayIPAddress*是 hello 在內部部署 VPN 裝置 IP 位址。 VPN 裝置不能位於 NAT 後方。
* hello *AddressPrefix*是內部位址空間。

tooadd 區域網路閘道與單一位址前置詞：

  ```powershell
  New-AzureRmLocalNetworkGateway -Name Site2 -ResourceGroupName TestRG1 `
  -Location 'East US' -GatewayIpAddress '23.99.221.164' -AddressPrefix '10.0.0.0/24'
  ```

tooadd 區域網路閘道與多個位址前置詞：

  ```powershell
  New-AzureRmLocalNetworkGateway -Name Site2 -ResourceGroupName TestRG1 `
  -Location 'East US' -GatewayIpAddress '23.99.221.164' -AddressPrefix @('10.0.0.0/24','20.0.0.0/24')
  ```

toomodify 區域網路閘道的 IP 位址前置詞：<br>
有時候您的區域網路閘道首碼會有所變更。 hello 您採取步驟 toomodify 您前置詞，取決於您是否建立 VPN 閘道連線的 IP 位址。 請參閱 hello[修改 IP 位址首碼的區域網路閘道](#modify)本文一節。

## <a name="PublicIP"></a>4.要求公用 IP 位址

VPN 閘道必須具有公用 IP 位址。 您第一次要求 hello IP 位址資源，並建立您的虛擬網路閘道時參考 tooit。 hello IP 位址建立 hello VPN 閘道時，會動態指定 toohello 資源。 VPN 閘道目前僅支援*動態*公用 IP 位址配置。 您無法要求靜態公用 IP 位址指派。 不過，這不表示 hello IP 位址變更之後已被指派 tooyour VPN 閘道。 hello 公用 IP 位址變更為當 hello 閘道 hello 才會刪除並重新建立。 它不會因為重新調整、重設或 VPN 閘道的其他內部維護/升級而變更。

要求將會指派 tooyour 虛擬網路 VPN 閘道的公用 IP 位址。

```powershell
$gwpip= New-AzureRmPublicIpAddress -Name gwpip -ResourceGroupName TestRG1 -Location 'East US' -AllocationMethod Dynamic
```

## <a name="GatewayIPConfig"></a>5.建立 hello 閘道 IP 位址組態

hello 閘道組態會定義 hello 子網路和公用 IP 位址 toouse hello。 使用下列範例 toocreate hello 閘道組態：

```powershell
$vnet = Get-AzureRmVirtualNetwork -Name TestVNet1 -ResourceGroupName TestRG1
$subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet
$gwipconfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name gwipconfig1 -SubnetId $subnet.Id -PublicIpAddressId $gwpip.Id
```

## <a name="CreateGateway"></a>6.建立 hello VPN 閘道

建立 hello 虛擬網路 VPN 閘道。 建立 VPN 閘道可能佔用 too45 分鐘或更多 toocomplete。

使用下列值的 hello:

* hello *-gatewaytype 的授權*網站-站台組態是*Vpn*。 hello 閘道類型一律為您實作的特定 toohello 組態。 例如，其他閘道器組態可能需要 -GatewayType ExpressRoute。
* hello *-VpnType*可以*RouteBased* （又稱為 tooas 某些文件中的動態閘道），或*PolicyBased* （又稱為 tooas 某些文件中的靜態閘道). 如需 VPN 閘道類型的詳細資訊，請參閱[關於 VPN 閘道](vpn-gateway-about-vpngateways.md)。
* 選取您想 toouse 的閘道 SKU hello。 某些 SKU 有組態限制。 如需詳細資訊，請參閱[閘道 SKU](vpn-gateway-about-vpn-gateway-settings.md#gwsku)。 如果您建立有關 hello hello VPN 閘道時收到錯誤-GatewaySku，請確認您已安裝 hello hello PowerShell 指令程式的最新版本。

```powershell
New-AzureRmVirtualNetworkGateway -Name VNet1GW -ResourceGroupName TestRG1 `
-Location 'East US' -IpConfigurations $gwipconfig -GatewayType Vpn `
-VpnType RouteBased -GatewaySku VpnGw1
```

## <a name="ConfigureVPNDevice"></a>7.設定 VPN 裝置

站台對站連線 tooan 在內部部署網路需要 VPN 裝置。 在此步驟中，設定 VPN 裝置。 當設定 VPN 裝置，您會需要 hello 下列：

- 共用金鑰。 這是共用相同 hello 建立您的站對站 VPN 連線時所指定的索引鍵。 在我們的範例中，我們會使用基本的共用金鑰。 我們建議您產生更複雜金鑰 toouse。
- hello 的虛擬網路閘道的公用 IP 位址。 您可以使用 hello Azure 入口網站、 PowerShell 或 CLI 檢視 hello 公用 IP 位址。 toofind hello 公用 IP 位址的虛擬網路閘道使用 PowerShell，下列範例使用 hello:

  ```powershell
  Get-AzureRmPublicIpAddress -Name GW1PublicIP -ResourceGroupName TestRG1
  ```

[!INCLUDE [Configure VPN device](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]


## <a name="CreateConnection"></a>8.建立 hello VPN 連線

接下來，建立您的虛擬網路閘道與 VPN 裝置之間的 hello 站對站 VPN 連線。 是以您自己的確定 tooreplace hello 值。 hello 共用的金鑰必須符合您要用於 VPN 裝置組態的 hello 值。 請注意該 hello '-ConnectionType' 站台對站台是*IPsec*。

1. 設定 hello 變數。
  ```powershell
  $gateway1 = Get-AzureRmVirtualNetworkGateway -Name VNet1GW -ResourceGroupName TestRG1
  $local = Get-AzureRmLocalNetworkGateway -Name Site2 -ResourceGroupName TestRG1
  ```

2. 建立 hello 連線。
  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name VNet1toSite2 -ResourceGroupName TestRG1 `
  -Location 'East US' -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
  -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
  ```

過一會兒，hello 會建立連線。

## <a name="toverify"></a>9.確認 hello VPN 連線

有幾個不同的方式 tooverify VPN 連線。

[!INCLUDE [Verify connection](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <a name="connectVM"></a>tooconnect tooa 虛擬機器

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-s2s-include.md)]


## <a name="modify"></a>修改區域網路閘道的 IP 位址首碼

如果您想要路由傳送 tooyour 在內部部署位置的 hello IP 位址首碼的變更，您可以修改 hello 區域網路閘道。 所提供的指示有兩組。 您選擇的 hello 指示取決於是否已建立您的閘道連線。

[!INCLUDE [Modify prefixes](../../includes/vpn-gateway-modify-ip-prefix-rm-include.md)]

## <a name="modifygwipaddress"></a>修改 hello 區域網路閘道的閘道 IP 位址

[!INCLUDE [Modify gateway IP address](../../includes/vpn-gateway-modify-lng-gateway-ip-rm-include.md)]

## <a name="next-steps"></a>後續步驟

*  一旦完成您的連線，您可以將虛擬機器 tooyour 虛擬網路。 如需詳細資訊，請參閱[虛擬機器](https://docs.microsoft.com/azure/#pivot=services&panel=Compute)。
* BGP 的相關資訊，請參閱 hello [BGP 概觀](vpn-gateway-bgp-overview.md)和[如何 tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md)。
