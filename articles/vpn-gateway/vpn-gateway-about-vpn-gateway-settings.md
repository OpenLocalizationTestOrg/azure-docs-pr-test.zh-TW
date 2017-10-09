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
# <a name="about-vpn-gateway-configuration-settings"></a>關於 VPN 閘道組態設定

VPN 閘道是一種虛擬網路閘道，可透過公用連線在您的虛擬網路和內部部署位置之間傳送加密流量。 您也可以使用 hello Azure 骨幹上的虛擬網路之間的 VPN 閘道 toosend 流量。

VPN 閘道連線依賴 hello 設定多個資源，其中每一個都包含可設定的設定。 本文章中的 hello 各節將討論 hello 資源和 tooa Resource Manager 部署模型中建立虛擬網路的 VPN 閘道與相關聯的設定。 您可以找到 hello 中每個連線解決方案說明和拓撲圖表[有關 VPN 閘道](vpn-gateway-about-vpngateways.md)發行項。

## <a name="gwtype"></a>閘道類型

每個虛擬網路只能有一個各類型的虛擬網路閘道。 當您建立虛擬網路閘道時，您必須確定 hello 閘道類型正確設定。

hello-gatewaytype 的授權提供值如下：

* Vpn
* ExpressRoute

VPN 閘道需要 hello `-GatewayType` *Vpn*。

範例：

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig -GatewayType Vpn `
-VpnType RouteBased
```

## <a name="gwsku"></a>閘道 SKU

[!INCLUDE [vpn-gateway-gwsku-include](../../includes/vpn-gateway-gwsku-include.md)]

### <a name="configure-hello-gateway-sku"></a>設定 hello 閘道 SKU

#### <a name="azure-portal"></a>Azure 入口網站

如果您使用 hello Azure 入口網站 toocreate 資源管理員虛擬網路閘道，您可以使用 hello 下拉式清單中選取 hello 閘道 SKU。 hello 選項，您會看到對應 toohello 閘道類型和您選取的 VPN 類型。

#### <a name="powershell"></a>PowerShell

hello 下列 PowerShell 範例會指定 hello `-GatewaySku` VpnGw1 為。

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig -GatewaySku VpnGw1 `
-GatewayType Vpn -VpnType RouteBased
```

#### <a name="resize"></a>變更閘道 SKU (調整閘道 SKU 大小)

如果您的閘道 SKU tooa 想 tooupgrade 功能更強大的 SKU，您可以使用 hello `Resize-AzureRmVirtualNetworkGateway` PowerShell cmdlet。 您也可以降級 hello 閘道 SKU 大小使用這個指令程式。

下列 PowerShell 範例 hello 顯示閘道 SKU 正在調整大小 tooVpnGw2。

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku VpnGw2
```

## <a name="connectiontype"></a>連線類型

在 hello Resource Manager 部署模型，每個組態會需要特定虛擬網路閘道的連線類型。 hello 可用的資源管理員 PowerShell 值`-ConnectionType`是：

* IPsec
* Vnet2Vnet
* ExpressRoute
* VPNClient

在 hello 下列 PowerShell 範例，我們會建立需要 hello 連接類型的 S2S 連線*IPsec*。

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name localtovon -ResourceGroupName testrg `
-Location 'West US' -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
-ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
```

## <a name="vpntype"></a>VPN 類型

當您建立 VPN 閘道設定的 hello 虛擬網路閘道時，您必須指定的 VPN 類型。 hello 您選擇的 VPN 類型取決於 hello 連線拓撲的 toocreate。 例如，P2S 連線需要 RouteBased VPN 類型。 VPN 類型而且可以根據您使用的 hello 硬體。 S2S 組態需要 VPN 裝置。 有些 VPN 裝置僅支援特定 VPN 類型。

hello 您所選取的 VPN 類型必須符合您想要 toocreate hello 解決方案的所有 hello 連線需求。 例如，如果您想 toocreate S2S VPN 閘道連線和 P2S VPN 閘道連線的 hello 相同虛擬網路，您會使用 VPN 類型*RouteBased*因為 P2S 需要 RouteBased VPN 類型。 您也需要 tooverify VPN 裝置支援 RouteBased VPN 連線。 

一旦建立虛擬網路閘道之後，您無法變更 hello VPN 類型。 您有 toodelete hello 虛擬網路閘道，並建立新的連線。 有兩種 VPN 類型：

[!INCLUDE [vpn-gateway-vpntype](../../includes/vpn-gateway-vpntype-include.md)]

hello 下列 PowerShell 範例會指定 hello`-VpnType`為*RouteBased*。 當您建立閘道時，您必須確定該 hello-VpnType 是正確的組態。

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig `
-GatewayType Vpn -VpnType RouteBased
```

## <a name="requirements"></a>閘道需求

[!INCLUDE [vpn-gateway-table-requirements](../../includes/vpn-gateway-table-requirements-include.md)]

## <a name="gwsub"></a>閘道子網路

建立 VPN 閘道之前，您必須先建立閘道子網路。 hello 閘道子網路包含 hello 的 IP 位址的 hello 虛擬網路閘道的 Vm 和服務使用。 當您建立虛擬網路閘道時，閘道 Vm 已部署的 toohello 閘道子網路並且使用設定所需的 hello VPN 閘道設定。 您必須永遠不會部署任何項目 （例如，其他 Vm） else toohello 閘道子網路。 hello 閘道子網路必須命名為 'GatewaySubnet' toowork 正確。 命名 hello 閘道子網路 'GatewaySubnet' 可讓 Azure 知道這是 hello 子網路 toodeploy hello 虛擬網路閘道的 Vm 和服務。

當您建立 hello 閘道子網路時，您可以指定包含 hello hello 子網路的 IP 位址數目。 hello 閘道子網路中的 hello IP 位址是配置的 toohello 閘道 Vm，閘道服務。 有些組態需要的 IP 位址比其他組態多。 查看 hello 設定您想 toocreate，並確認您想要 toocreate hello 閘道子網路會符合這些需求的 hello 指示。 此外，您可能想 toomake 確定您的閘道子網路包含足夠的 IP 位址 tooaccommodate 可能未來其他設定。 雖然您可以建立像 /29 這麼小的閘道子網路，但建議您建立 /28 或更大 (/28、/27、/26 等) 的閘道子網路。 這樣一來，如果您將功能加入在 hello 未來，您將不會有 tootear 閘道，然後刪除並重新建立 hello 閘道子網路 tooallow 更多 IP 位址。

hello 下列資源管理員 PowerShell 範例會示範名為 GatewaySubnet 閘道子網路。 您可以看到 hello CIDR 標記法指定 /27，即允許足夠的 IP 位址，對於多數組態目前存在的。

```powershell
Add-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.0.3.0/27
```

[!INCLUDE [vpn-gateway-no-nsg](../../includes/vpn-gateway-no-nsg-include.md)]

## <a name="lng"></a>區域網路閘道

在建立 VPN 閘道設定時，hello 區域網路閘道通常代表您在內部部署位置。 在 hello 傳統部署模型中，hello 區域網路閘道已參考的 tooas 本機站台。 

您指定 hello 區域網路閘道的名稱、 hello hello 在內部部署 VPN 裝置，公用 IP 位址，並指定 hello 都位於 hello 在內部部署位置的位址首碼。 Azure 會查看網路流量的 hello 目的地位址前置詞、 參照 hello 設定您所指定區域網路閘道，並據以路由傳送封包。 您也可以針對使用 VPN 閘道連線的 VNet 對 VNet 組態指定區域網路閘道。

hello 下列 PowerShell 範例會建立新的區域網路閘道：

```powershell
New-AzureRmLocalNetworkGateway -Name LocalSite -ResourceGroupName testrg `
-Location 'West US' -GatewayIpAddress '23.99.221.164' -AddressPrefix '10.5.51.0/24'
```

有時候您需要 toomodify hello 區域網路閘道設定。 例如，當您加入或修改 hello 位址範圍，或如果 hello hello VPN 裝置 IP 位址變更。 傳統的 vnet，您可以變更這些設定 hello hello 區域網路 頁面上的傳統入口網站中。 針對 Resource Manager，請參閱 [使用 PowerShell 修改區域網路閘道設定](vpn-gateway-modify-local-network-gateway.md)。

## <a name="resources"></a>REST API 和 PowerShell Cmdlet

如需其他技術資源與特定語法需求時使用 REST Api、 PowerShell cmdlet 或 Azure CLI VPN 閘道的設定，請參閱 hello 下列頁面：

| **傳統** | **資源管理員** |
| --- | --- |
| [PowerShell](/powershell/module/azure#networking) |[PowerShell](/powershell/module/azurerm.network#vpn) |
| [REST API](https://msdn.microsoft.com/library/jj154113) |[REST API](/rest/api/network/virtualnetworkgateways) |
| 不支援 | [Azure CLI](/cli/azure/network/vnet-gateway)|

## <a name="next-steps"></a>後續步驟

如需有關可用連線組態的詳細資訊，請參閱[關於 VPN 閘道](vpn-gateway-about-vpngateways.md)。