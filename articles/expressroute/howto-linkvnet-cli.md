---
title: "虛擬網路 tooan ExpressRoute 電路的連結： CLI: Azure |Microsoft 文件"
description: "本文件概述 toolink 虛擬網路 (Vnet) tooExpressRoute 電路 hello Resource Manager 部署模型和 CLI 所使用的方式。"
services: expressroute
documentationcenter: na
author: cherylmc
manager: timlit
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/25/2017
ms.author: anzaman,cherylmc
ms.openlocfilehash: 1251f016d9b94d3fee81de1df164cb085cbe9d78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-virtual-network-tooan-expressroute-circuit-using-cli"></a>連接使用 CLI 的虛擬網路 tooan ExpressRoute 電路

這篇文章可協助您使用 CLI 的虛擬網路 (Vnet) tooAzure ExpressRoute 電路的連結。 使用 Azure CLI toolink hello 虛擬網路必須使用 hello Resource Manager 部署模型來建立。 它們可以在 hello 是相同的訂用帳戶或其他訂用帳戶的一部分。 如果您想 toouse 不同方法 tooconnect 您 VNet tooan ExpressRoute 循環，您可以從下列清單中的 hello 選取一個發行項：

> [!div class="op_single_selector"]
> * [Azure 入口網站](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-linkvnet-arm.md)
> * [Azure CLI](howto-linkvnet-cli.md)
> * [影片 - Azure 入口網站](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [PowerShell (傳統)](expressroute-howto-linkvnet-classic.md)
> 

## <a name="configuration-prerequisites"></a>組態必要條件

* 您需要 hello hello 命令列介面 (CLI) 的最新版本。 如需詳細資訊，請參閱[安裝 Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)。
* 您需要 tooreview hello[必要條件](expressroute-prerequisites.md)，[路由需求](expressroute-routing.md)，和[工作流程](expressroute-workflows.md)開始設定之前。
* 您必須擁有作用中的 ExpressRoute 線路。 
  * 請依照下列指示 hello 太[建立 ExpressRoute 電路](howto-circuit-cli.md)和已啟用連線提供者的 hello 循環。 
  * 確定您已針對循環設定了 Azure 私用對等。 請參閱 hello[設定路由](howto-routing-cli.md)路由指示的發行項。 
  * 確定已設定 Azure 私用對等互連。 hello BGP 對等互連網路與 Microsoft 之間必須啟動，讓您可以啟用端對端連線。
  * 請確定您有已建立且完整佈建的虛擬網路和虛擬網路閘道。 請依照下列指示 hello 太[設定 expressroute 的虛擬網路閘道](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-cli)。 要確定 toouse `--gateway-type ExpressRoute`。

* 您可以連結 too10 虛擬網路 tooa 標準 ExpressRoute 電路。 所有虛擬網路必須位於 hello 相同地理政治區域時使用標準的 ExpressRoute 電路。 

* 如果您啟用 hello ExpressRoute premium 附加元件，您可以連結以外的 hello ExpressRoute 電路的 hello 地緣政治區域虛擬網路或連線較大的虛擬網路 tooyour ExpressRoute 循環數目。 如需 hello premium 附加元件的詳細資訊，請參閱 hello[常見問題集](expressroute-faqs.md)。

## <a name="connect-a-virtual-network-in-hello-same-subscription-tooa-circuit"></a>連接 hello 中的虛擬網路相同的訂用帳戶 tooa 電路

您可以藉由使用 hello 範例連接虛擬網路閘道 tooan ExpressRoute 電路。 請確定該 hello 虛擬網路閘道建立並且準備好進行連結，然後再執行 hello 命令。

```azurecli
az network vpn-connection create --name ERConnection --resource-group ExpressRouteResourceGroup --vnet-gateway1 VNet1GW --express-route-circuit2 MyCircuit
```

## <a name="connect-a-virtual-network-in-a-different-subscription-tooa-circuit"></a>在不同的訂用帳戶 tooa 電路的虛擬網路連線

您可以讓多個訂用帳戶共用 ExpressRoute 線路。 hello 下圖顯示簡單圖解如何共用 ExpressRoute 電路的運作方式跨多個訂用帳戶。

Hello hello 大型雲端內的小型雲端都屬於 toodifferent 部門組織內使用的 toorepresent 訂用帳戶。 每個 hello hello 組織內的部門可以使用自己的訂用帳戶部署其服務-但它們可以共用單一 ExpressRoute 電路 tooconnect 後 tooyour 在內部部署網路。 單一部門 (在此範例中： IT) 可以擁有 hello ExpressRoute 電路。 Hello 組織內其他訂用帳戶可以使用 hello ExpressRoute 電路。

> [!NOTE]
> Hello 專用循環的連線和頻寬費用將會套用的 toohello ExpressRoute 電路擁有者。 所有虛擬網路共用 hello 相同的頻寬。
> 
> 

![跨訂用帳戶的連線能力](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)

### <a name="administration---circuit-owners-and-circuit-users"></a>系統管理 - 線路擁有者和線路使用者

hello '電路擁有者' 是授權的 Power hello ExpressRoute 電路資源的使用者。 hello 電路擁有者可以建立可以兌換的 「 循環的使用者 」 的授權。 循環使用者是擁有者的虛擬網路閘道，不在 hello 相同訂用帳戶，因為 hello ExpressRoute 電路。 線路使用者可以兌換授權 (每個虛擬網路一個授權)。

hello 電路擁有者隨時都有 hello 電源 toomodify 和撤銷授權。 授權撤銷時，所有連結連線將會都刪除從 hello 訂用帳戶已撤銷其存取權。

### <a name="circuit-owner-operations"></a>線路擁有者作業

**toocreate 授權**

hello 電路擁有者建立授權，可建立的授權金鑰，可以使用循環使用者 tooconnect 其虛擬網路閘道 toohello ExpressRoute 電路。 一個授權僅適用於一個連線。

下列範例會示範如何 hello toocreate 授權：

```azurecli
az network express-route auth create --circuit-name MyCircuit -g ExpressRouteResourceGroup -n MyAuthorization
```

hello 回應包含 hello 授權金鑰和狀態：

```azurecli
"authorizationKey": "0a7f3020-541f-4b4b-844a-5fb43472e3d7",
"authorizationUseStatus": "Available",
"etag": "W/\"010353d4-8955-4984-807a-585c21a22ae0\"",
"id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/authorizations/MyAuthorization1",
"name": "MyAuthorization1",
"provisioningState": "Succeeded",
"resourceGroup": "ExpressRouteResourceGroup"
```

**tooreview 授權**

hello 電路擁有者可以檢閱執行 hello 下列範例針對特定電路來發出的所有授權：

```azurecli
az network express-route auth list --circuit-name MyCircuit -g ExpressRouteResourceGroup
```

**tooadd 授權**

hello 電路擁有者可以使用下列範例中的 hello 來新增授權：

```azurecli
az network express-route auth create --circuit-name MyCircuit -g ExpressRouteResourceGroup -n MyAuthorization1
```

**toodelete 授權**

hello 電路擁有者可以撤銷/刪除授權 toohello 使用者藉由執行下列範例中的 hello:

```azurecli
az network express-route auth delete --circuit-name MyCircuit -g ExpressRouteResourceGroup -n MyAuthorization1
```

### <a name="circuit-user-operations"></a>線路使用者作業

hello 循環使用者需要 hello 對等識別碼與 hello 電路擁有者從授權金鑰。 hello 授權金鑰是 GUID。

```azurecli
Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
```

**tooredeem 連線授權**

hello 循環使用者可以執行下列範例 tooredeem hello 連結授權：

```azurecli
az network vpn-connection create --name ERConnection --resource-group ExpressRouteResourceGroup --vnet-gateway1 VNet1GW --express-route-circuit2 MyCircuit --authorization-key "^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^"
```

**toorelease 連線授權**

您可以藉由刪除連結 hello ExpressRoute 電路 toohello 虛擬網路的 hello 連接釋放授權。

## <a name="next-steps"></a>後續步驟

如需 ExpressRoute 的詳細資訊，請參閱 hello [ExpressRoute 常見問題集](expressroute-faqs.md)。
