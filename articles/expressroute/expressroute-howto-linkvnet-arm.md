---
title: "虛擬網路 tooan ExpressRoute 電路的連結： PowerShell: Azure |Microsoft 文件"
description: "本文件概述 toolink 虛擬網路 (Vnet) tooExpressRoute 電路使用 hello Resource Manager 部署模型和 PowerShell 的方式。"
services: expressroute
documentationcenter: na
author: ganesr
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: daacb6e5-705a-456f-9a03-c4fc3f8c1f7e
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/05/2017
ms.author: ganesr
ms.openlocfilehash: e75a9f6b42fa8e1a579e4f19882ec99b277b545f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-virtual-network-tooan-expressroute-circuit"></a>連接虛擬網路 tooan ExpressRoute 電路
> [!div class="op_single_selector"]
> * [Azure 入口網站](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-linkvnet-arm.md)
> * [Azure CLI](howto-linkvnet-cli.md)
> * [影片 - Azure 入口網站](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [PowerShell (傳統)](expressroute-howto-linkvnet-classic.md)
>

這篇文章可協助您使用 hello Resource Manager 部署模型和 PowerShell 連結虛擬網路 (Vnet) tooAzure ExpressRoute 電路。 虛擬網路可以 hello 中相同的訂用帳戶或其他訂用帳戶的一部分。 本文也會顯示如何 tooupdate 虛擬網路連結。 

## <a name="before-you-begin"></a>開始之前
* 安裝 hello hello Azure PowerShell 模組最新版本。 如需詳細資訊，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。
* 檢閱 hello[必要條件](expressroute-prerequisites.md)，[路由需求](expressroute-routing.md)，和[工作流程](expressroute-workflows.md)開始設定之前。
* 您必須擁有作用中的 ExpressRoute 線路。 
  * 請依照下列指示 hello 太[建立 ExpressRoute 電路](expressroute-howto-circuit-arm.md)和已啟用連線提供者的 hello 循環。 
  * 確定您已針對循環設定了 Azure 私用對等。 請參閱 hello[設定路由](expressroute-howto-routing-arm.md)路由指示的發行項。 
  * 請確認 Azure 私用對等設定，且 hello BGP 對等互連網路與 Microsoft 之間，以便您可以啟用端對端連線已啟動。
  * 請確定您有已建立且完整佈建的虛擬網路和虛擬網路閘道。 請依照下列指示 hello 太[建立 expressroute 的虛擬網路閘道](expressroute-howto-add-gateway-resource-manager.md)。 Expressroute 的虛擬網路閘道使用 hello gatewaytype 的授權 'ExpressRoute'，不是 VPN。

* 您可以連結 too10 虛擬網路 tooa 標準 ExpressRoute 電路。 所有虛擬網路必須位於 hello 相同地理政治區域時使用標準的 ExpressRoute 電路。 

* 您可以連結以外的 hello ExpressRoute 電路的 hello 地緣政治區域虛擬網路或連線較大的虛擬網路 tooyour ExpressRoute 循環數目，如果啟用 hello ExpressRoute premium add-on。 檢查 hello[常見問題集](expressroute-faqs.md)如需有關 hello premium 附加元件。


## <a name="connect-a-virtual-network-in-hello-same-subscription-tooa-circuit"></a>連接 hello 中的虛擬網路相同的訂用帳戶 tooa 電路
您可以使用下列 cmdlet 的 hello 連接虛擬網路閘道 tooan ExpressRoute 電路。 請確定該 hello 虛擬網路閘道建立並且準備好進行連結，然後再執行 hello cmdlet:

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$gw = Get-AzureRmVirtualNetworkGateway -Name "ExpressRouteGw" -ResourceGroupName "MyRG"
$connection = New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName "MyRG" -Location "East US" -VirtualNetworkGateway1 $gw -PeerId $circuit.Id -ConnectionType ExpressRoute
```

## <a name="connect-a-virtual-network-in-a-different-subscription-tooa-circuit"></a>在不同的訂用帳戶 tooa 電路的虛擬網路連線
您可以讓多個訂用帳戶共用 ExpressRoute 線路。 hello 遵循圖顯示的簡單圖解如何共用 ExpressRoute 電路的運作方式跨多個訂用帳戶。

Hello hello 大型雲端內的小型雲端都屬於 toodifferent 部門組織內使用的 toorepresent 訂用帳戶。 每個 hello hello 組織內的部門可以使用自己的訂用帳戶部署其服務-但它們可以共用單一 ExpressRoute 電路 tooconnect 後 tooyour 在內部部署網路。 單一部門 (在此範例中： IT) 可以擁有 hello ExpressRoute 電路。 Hello 組織內其他訂用帳戶可以使用 hello ExpressRoute 電路。

> [!NOTE]
> Hello ExpressRoute 電路的連線和頻寬費用將會套用的 toohello 訂用帳戶擁有者。 所有虛擬網路共用 hello 相同的頻寬。
> 
> 

![跨訂用帳戶的連線能力](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)


### <a name="administration---circuit-owners-and-circuit-users"></a>系統管理 - 線路擁有者和線路使用者

hello '電路擁有者' 是授權的 Power hello ExpressRoute 電路資源的使用者。 hello 電路擁有者可以建立可以兌換的 「 循環的使用者 」 的授權。 循環使用者是擁有者的虛擬網路閘道，不在 hello 相同訂用帳戶，因為 hello ExpressRoute 電路。 電路使用者可以兌換授權 (每個虛擬網路一個授權)。

hello 電路擁有者隨時都有 hello 電源 toomodify 和撤銷授權。 撤銷授權會導致從已撤銷其存取權的 hello 訂用帳戶中刪除所有連結連線。

### <a name="circuit-owner-operations"></a>循環擁有者作業

**toocreate 授權**

hello 電路擁有者建立的授權。 這會導致 hello 建立的授權金鑰可以使用循環使用者 tooconnect 其虛擬網路閘道 toohello ExpressRoute 電路。 一個授權僅適用於一個連線。

下列指令程式的程式碼片段說明如何 hello toocreate 授權：

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
Add-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization1"
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit

$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$auth1 = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization1"
```


hello 授權金鑰和狀態，將會包含 hello 回應 toothis:

    Name                   : MyAuthorization1
    Id                     : /subscriptions/&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&/resourceGroups/ERCrossSubTestRG/providers/Microsoft.Network/expressRouteCircuits/CrossSubTest/authorizations/MyAuthorization1
    Etag                   : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&& 
    AuthorizationKey       : ####################################
    AuthorizationUseStatus : Available
    ProvisioningState      : Succeeded



**tooreview 授權**

hello 電路擁有者可以檢閱由執行下列 cmdlet 的 hello 特定電路發出的所有授權：

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$authorizations = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit
```

**tooadd 授權**

hello 電路擁有者可以使用下列 cmdlet 的 hello 來新增授權：

```powershell
$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
Add-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit -Name "MyAuthorization2"
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit

$circuit = Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
$authorizations = Get-AzureRmExpressRouteCircuitAuthorization -ExpressRouteCircuit $circuit
```

**toodelete 授權**

hello 電路擁有者可以撤銷/刪除授權 toohello 使用者藉由執行下列 cmdlet 的 hello:

```powershell
Remove-AzureRmExpressRouteCircuitAuthorization -Name "MyAuthorization2" -ExpressRouteCircuit $circuit
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $circuit
```    

### <a name="circuit-user-operations"></a>循環使用者作業

hello 電路使用者需要 hello 對等識別碼與 hello 電路擁有者從授權金鑰。 hello 授權金鑰是 GUID。

對等識別碼可以檢查從 hello 下列命令：

```powershell
Get-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "MyRG"
```

**tooredeem 連線授權**

hello 循環使用者可以執行下列 cmdlet tooredeem hello 連結授權：

```powershell
$id = "/subscriptions/********************************/resourceGroups/ERCrossSubTestRG/providers/Microsoft.Network/expressRouteCircuits/MyCircuit"    
$gw = Get-AzureRmVirtualNetworkGateway -Name "ExpressRouteGw" -ResourceGroupName "MyRG"
$connection = New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName "RemoteResourceGroup" -Location "East US" -VirtualNetworkGateway1 $gw -PeerId $id -ConnectionType ExpressRoute -AuthorizationKey "^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^"
```

**toorelease 連線授權**

您可以藉由刪除連結 hello ExpressRoute 電路 toohello 虛擬網路的 hello 連接釋放授權。

## <a name="modify-a-virtual-network-connection"></a>修改虛擬網路連線
您可以更新虛擬網路連線的特定屬性。 

**tooupdate hello 連接權數**

您的虛擬網路可以連接的 toomultiple ExpressRoute 電路。 您可能會收到相同的前置詞的 hello 從多個 ExpressRoute 電路。 您可以變更的 toochoose 哪些連線 toosend 流量目的地為此前置詞， *RoutingWeight*的連線。 流量將會傳送 hello 連線以最高的 hello *RoutingWeight*。

```powershell
$connection = Get-AzureRmVirtualNetworkGatewayConnection -Name "MyVirtualNetworkConnection" -ResourceGroupName "MyRG"
$connection.RoutingWeight = 100
Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection
```

hello 範圍*RoutingWeight*是 0 too32000。 hello 預設值為 0。

## <a name="next-steps"></a>後續步驟
如需 ExpressRoute 的詳細資訊，請參閱 hello [ExpressRoute 常見問題集](expressroute-faqs.md)。
