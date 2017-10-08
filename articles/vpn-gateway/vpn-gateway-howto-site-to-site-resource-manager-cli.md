---
title: "連接您在內部部署網路 tooan Azure 虛擬網路： 站對站 VPN: CLI |Microsoft 文件"
description: "IPsec 連線從您內部網路 tooan Azure 虛擬網路上的步驟 toocreate hello 公用網際網路。 這些步驟可協助您使用 CLI 建立跨單位的站對站 VPN 閘道連線。"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/09/2017
ms.author: cherylmc
ms.openlocfilehash: c652cf2caf3928cdeb19d7dc329f6db101e5ed90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-with-a-site-to-site-vpn-connection-using-cli"></a>使用 CLI 建立具有站對站 VPN 連線的虛擬網路

本文章將示範如何 toouse 會 hello Azure CLI toocreate 站對站 VPN 閘道連線從您的內部部署網路 toohello VNet。 本文章中的 hello 步驟適用於 toohello Resource Manager 部署模型。 您也可以建立此組態使用不同的部署工具或部署模型，從下列清單中的 hello 選取不同的選項：<br>

> [!div class="op_single_selector"]
> * [Azure 入口網站](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [CLI](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [Azure 入口網站 (傳統)](vpn-gateway-howto-site-to-site-classic-portal.md)
> 
>


![站對站 VPN 閘道跨單位連線圖表](./media/vpn-gateway-howto-site-to-site-resource-manager-cli/site-to-site-diagram.png)

站對站 VPN 閘道連線是使用的 tooconnect 您內部網路 tooan Azure 虛擬網路透過 VPN IPsec/IKE （IKEv1 或 IKEv2） 通道。 這種類型的連線需要 VPN 裝置位於內部部署具有對外開放的公用 IP 位址指派 tooit。 如需 VPN 閘道的詳細資訊，請參閱[關於 VPN 閘道](vpn-gateway-about-vpngateways.md)。

## <a name="before-you-begin"></a>開始之前

請確認您已符合下列準則，開始設定之前的 hello:

* 請確定您擁有相容的 VPN 裝置和人能夠 tooconfigure 它。 如需相容 VPN 裝置和裝置組態的詳細資訊，請參閱[關於 VPN 裝置](vpn-gateway-about-vpn-devices.md)。
* 確認您的 VPN 裝置有對外開放的公用 IPv4 位址。 此 IP 位址不能位於 NAT 後方。
* 如果您不熟悉 hello IP 位址範圍位於內部網路組態，您需要 toocoordinate 的人可以為您提供這些詳細資料。 當您建立此設定時，您必須指定 hello IP 位址範圍前置詞，則 Azure 會路由傳送 tooyour 在內部部署位置。 無 hello 的內部部署網路的子網路可以透過圈具有您想要 tooconnect hello 虛擬網路子網路。
* 請確認您已安裝最新版本 （2.0 或更新版本） 的 hello CLI 命令。 如需安裝 hello CLI 命令的資訊，請參閱[安裝 Azure CLI 2.0](/cli/azure/install-azure-cli)和[開始使用 Azure CLI 2.0](/cli/azure/get-started-with-azure-cli)。

### <a name="example"></a>範例值

您可以使用下列值 toocreate 測試環境的 hello 或 toothese 值，請參閱 toobetter 了解這篇文章中的 hello 範例：

```
#Example values

VnetName                = TestVNet1 
ResourceGroup           = TestRG1 
Location                = eastus 
AddressSpace            = 10.11.0.0/16 
SubnetName              = Subnet1 
Subnet                  = 10.11.0.0/24 
GatewaySubnet           = 10.11.255.0/27 
LocalNetworkGatewayName = Site2 
LNG Public IP           = <VPN device IP address>
LocalAddrPrefix1        = 10.0.0.0/24
LocalAddrPrefix2        = 20.0.0.0/24   
GatewayName             = VNet1GW 
PublicIP                = VNet1GWIP 
VPNType                 = RouteBased 
GatewayType             = Vpn 
ConnectionName          = VNet1toSite2
```

## <a name="Login"></a>1.連接 tooyour 訂用帳戶

[!INCLUDE [CLI login](../../includes/vpn-gateway-cli-login-include.md)]

## <a name="rg"></a>2.建立資源群組

hello 下列範例會建立名為 'TestRG1' hello 'eastus' 位置中的資源群組。 如果您已經有資源群組，您想 toocreate VNet hello 區中，您可以改為使用一個。

```azurecli
az group create --name TestRG1 --location eastus
```

## <a name="VNet"></a>3.建立虛擬網路

如果您還沒有虛擬網路，建立一個使用 hello [az 網路 vnet 建立](/cli/azure/network/vnet#create)命令。 當建立虛擬網路，請確定 hello 您指定的位址空間不將任何您已在內部部署網路的 hello 位址空間重疊。

hello 下列範例會建立名為 'TestVNet1' 和 'Subnet1' 子網路，虛擬網路。

```azurecli
az network vnet create --name TestVNet1 --resource-group TestRG1 --address-prefix 10.11.0.0/16 --location eastus --subnet-name Subnet1 --subnet-prefix 10.11.0.0/24
```

## 4.<a name="gwsub"></a>建立 hello 閘道子網路

[!INCLUDE [vpn-gateway-no-nsg](../../includes/vpn-gateway-no-nsg-include.md)]

對於此組態，您也需要有閘道子網路。 hello 虛擬網路閘道會使用包含 hello hello VPN 閘道服務所使用的 IP 位址的閘道子網路。 當您建立閘道子網路時，請將它命名為「GatewaySubnet」。 如果您將其命名為其他名字，您會建立子網路，但 Azure 不會將它視為閘道器子網路。

您指定的 hello 閘道子網路的 hello 大小取決於 hello VPN 閘道設定您想 toocreate。 雖然可能 toocreate 閘道子網路為/29，我們建議您建立較大的子網路，其中包含多個位址，藉由選取 /27 或/28。 使用較大的閘道子網路允許足夠的 IP 位址 tooaccommodate 可能未來設定。

使用 hello [az vnet 子網路建立](/cli/azure/network/vnet/subnet#create)命令 toocreate hello 閘道子網路。

```azurecli
az network vnet subnet create --address-prefix 10.11.255.0/27 --name GatewaySubnet --resource-group TestRG1 --vnet-name TestVNet1
```

## <a name="localnet"></a>5.建立 hello 區域網路閘道

hello 區域網路閘道通常是指 tooyour 在內部部署位置。 您提供 hello 站台的名稱之 Azure 可以參考 tooit，然後指定 hello IP 位址的 hello 在內部部署 VPN 裝置 toowhich 中，您將建立連接。 您也指定 hello 而必須路由傳送透過 hello VPN 閘道 toohello VPN 裝置 IP 位址首碼。 您指定的 hello 位址前置詞是在內部部署網路上的 hello 前置詞。 如果您在內部部署網路變更時，您可以輕鬆地更新 hello 前置詞。

使用下列值的 hello:

* hello *-閘道 ip 位址*是 hello 在內部部署 VPN 裝置 IP 位址。 VPN 裝置不能位於 NAT 後方。
* hello *-本機位址首碼*是內部位址空間。

使用 hello [az 網路本機閘道建立](/cli/azure/network/local-gateway#create)命令 tooadd 區域網路閘道與多個位址前置詞：

```azurecli
az network local-gateway create --gateway-ip-address 23.99.221.164 --name Site2 --resource-group TestRG1 --local-address-prefixes 10.0.0.0/24 20.0.0.0/24
```

## <a name="PublicIP"></a>6.要求公用 IP 位址

VPN 閘道必須具有公用 IP 位址。 您第一次要求 hello IP 位址資源，並建立您的虛擬網路閘道時參考 tooit。 hello IP 位址建立 hello VPN 閘道時，會動態指定 toohello 資源。 VPN 閘道目前僅支援*動態*公用 IP 位址配置。 您無法要求靜態公用 IP 位址指派。 不過，這不表示 hello IP 位址變更之後已被指派 tooyour VPN 閘道。 hello 公用 IP 位址變更為當 hello 閘道 hello 才會刪除並重新建立。 它不會因為重新調整、重設或 VPN 閘道的其他內部維護/升級而變更。

使用 hello [az 網路公用 ip 建立](/cli/azure/network/public-ip#create)命令 toorequest 的動態公用 IP 位址。

```azurecli
az network public-ip create --name VNet1GWIP --resource-group TestRG1 --allocation-method Dynamic
```

## <a name="CreateGateway"></a>7.建立 hello VPN 閘道

建立 hello 虛擬網路 VPN 閘道。 建立 VPN 閘道可能佔用 too45 分鐘或更多 toocomplete。

使用下列值的 hello:

* hello *-閘道類型*網站-站台組態是*Vpn*。 hello 閘道類型一律為您實作的特定 toohello 組態。 如需詳細資訊，請參閱[閘道類型](vpn-gateway-about-vpn-gateway-settings.md#gwtype)。
* hello *-vpn 類型*可以*RouteBased* （又稱為 tooas 某些文件中的動態閘道），或*PolicyBased* （又稱為 tooas 部分中是靜態閘道文件）。 您所連接的 hello 裝置的特定 toorequirements hello 設定。 如需 VPN 閘道類型的詳細資訊，請參閱[關於 VPN 閘道組態設定](vpn-gateway-about-vpn-gateway-settings.md#vpntype)。
* 選取您想 toouse 的閘道 SKU hello。 某些 SKU 有組態限制。 如需詳細資訊，請參閱[閘道 SKU](vpn-gateway-about-vpn-gateway-settings.md#gwsku)。

建立 hello VPN 閘道使用 hello [az 網路 vnet 閘道建立](/cli/azure/network/vnet-gateway#create)命令。 如果您執行此命令使用 hello '-沒有-wait' 參數，您沒有看到任何意見反應或輸出。 此參數允許 hello 閘道 toocreate hello 背景。 它會採用約 45 分鐘內 toocreate 閘道。

```azurecli
az network vnet-gateway create --name VNet1GW --public-ip-address VNet1GWIP --resource-group TestRG1 --vnet TestVNet1 --gateway-type Vpn --vpn-type RouteBased --sku VpnGw1 --no-wait 
```

## <a name="VPNDevice"></a>8.設定 VPN 裝置

站台對站連線 tooan 在內部部署網路需要 VPN 裝置。 在此步驟中，設定 VPN 裝置。 當設定 VPN 裝置，您會需要 hello 下列：

- 共用金鑰。 這是共用相同 hello 建立您的站對站 VPN 連線時所指定的索引鍵。 在我們的範例中，我們會使用基本的共用金鑰。 我們建議您產生更複雜金鑰 toouse。
- hello 的虛擬網路閘道的公用 IP 位址。 您可以使用 hello Azure 入口網站、 PowerShell 或 CLI 檢視 hello 公用 IP 位址。 toofind hello 公用 IP 位址的虛擬網路閘道，使用 hello [az 網路公用 ip 清單](/cli/azure/network/public-ip#list)命令。 以方便閱讀，hello 輸出會是格式化的 toodisplay hello 清單的資料表中的公用 Ip。

  ```azurecli
  az network public-ip list --resource-group TestRG1 --output table
  ```


[!INCLUDE [Configure VPN device](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]


## <a name="CreateConnection"></a>9.建立 hello VPN 連線

建立虛擬網路閘道與內部部署 VPN 裝置之間的 hello 站對站 VPN 連線。 請特別注意 toohello 共用金鑰值，它必須符合設定的 hello 共用您的 VPN 裝置的金鑰值。

建立 hello 連線使用 hello [az 網路 vpn 連線建立](/cli/azure/network/vpn-connection#create)命令。

```azurecli
az network vpn-connection create --name VNet1toSite2 -resource-group TestRG1 --vnet-gateway1 VNet1GW -l eastus --shared-key abc123 --local-gateway2 Site2
```

過一會兒，hello 會建立連線。

## <a name="toverify"></a>10.確認 hello VPN 連線

[!INCLUDE [verify connection](../../includes/vpn-gateway-verify-connection-cli-rm-include.md)]

如果您想 toouse 另一個方法 tooverify 您的連線，請參閱[驗證的 VPN 閘道連線](vpn-gateway-verify-connection-resource-manager.md)。

## <a name="connectVM"></a>tooconnect tooa 虛擬機器

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-s2s-include.md)]

## <a name="tasks"></a>常見工作

本節包含使用站對站組態時很實用的常見命令。 Hello 的 CLI 網路命令的完整清單，請參閱[Azure CLI-網路](/cli/azure/network)。

[!INCLUDE [local network gateway common tasks](../../includes/vpn-gateway-common-tasks-cli-include.md)]

## <a name="next-steps"></a>後續步驟

* 一旦完成您的連線，您可以將虛擬機器 tooyour 虛擬網路。 如需詳細資訊，請參閱[虛擬機器](https://docs.microsoft.com/azure/#pivot=services&panel=Compute)。
* BGP 的相關資訊，請參閱 hello [BGP 概觀](vpn-gateway-bgp-overview.md)和[如何 tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md)。
* 如需強制通道的相關資訊，請參閱[關於強制通道](vpn-gateway-forced-tunneling-rm.md)。
* 如需高可用性主動-主動連線的相關資訊，請參閱[高可用性跨單位和 VNet 對 VNet 連線能力](vpn-gateway-highlyavailable.md)。
* 如需 Azure CLI 網路命令的清單，請參閱 [Azure CLI](https://docs.microsoft.com/cli/azure/network)。