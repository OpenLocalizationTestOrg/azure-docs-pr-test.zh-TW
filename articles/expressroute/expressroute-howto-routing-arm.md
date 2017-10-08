---
title: "如何 tooconfigure ExpressRoute 電路的路由 （對等互連）： 資源管理員： PowerShell: Azure |Microsoft 文件"
description: "這篇文章會引導您完成建立及佈建 hello 私人、 公用及 Microsoft 對等互連的 ExpressRoute 電路的 hello 步驟。 本文也會顯示 toocheck hello 狀態、 更新或刪除您的電路的互連的方式。"
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 0a036d51-77ae-4fee-9ddb-35f040fbdcdf
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: eb3ddf5c05a086ac3e22c64417e51381ef465921
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit-using-powershell"></a>使用 PowerShell 建立和修改 ExpressRoute 線路的對等互連

這篇文章可協助您建立及管理在 hello 資源管理員部署模型中使用 PowerShell 的 ExpressRoute 電路的路由組態。 您也可以檢查 hello 狀態、 更新或刪除，並取消佈建 ExpressRoute 循環的對等互連。 如果您想 toouse 不同方法 toowork 與您的循環，請從下列清單中的 hello 選取一個發行項：

> [!div class="op_single_selector"]
> * [Azure 入口網站](expressroute-howto-routing-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-routing-arm.md)
> * [Azure CLI](howto-routing-cli.md)
> * [視訊 - 私用對等互連](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [視訊 - 公用對等互連](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [視訊 - Microsoft 對等互連](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> * [PowerShell (傳統)](expressroute-howto-routing-classic.md)
> 

## <a name="configuration-prerequisites"></a>組態必要條件

* 您將需要 hello 的 hello Azure 資源管理員 PowerShell cmdlet 的最新版本。 如需詳細資訊，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。 
* 請確定您已經檢閱 hello[必要條件](expressroute-prerequisites.md)頁面 hello[路由需求](expressroute-routing.md)頁面和 hello[工作流程](expressroute-workflows.md)頁面開始設定之前。
* 您必須擁有作用中的 ExpressRoute 線路。 請依照下列指示 hello 太[建立 ExpressRoute 電路](expressroute-howto-circuit-arm.md)和有 hello 電路啟用您的連線提供者，才能繼續。 hello ExpressRoute 電路必須位於您 toobe 無法 toorun hello cmdlet，在本文中的佈建並啟用狀態。

這些說明僅適用於 toocircuits 建立與服務供應項目層級 2 連線服務的提供者。 如果您使用的服務提供者提供受管理的第 3 層服務 (通常是 IPVPN，如 MPLS)，連線提供者會為您設定和管理路由。

> [!IMPORTANT]
> 我們目前不會進行通告透過 hello 服務管理入口網站的服務提供者所設定的對等互連。 我們正努力在近期推出這項功能。 設定 BGP 對等互連之前，請洽詢您的服務提供者。
> 
> 

您可以為 ExpressRoute 線路設定一個、兩個或全部三個對等 (Azure 私用、Azure 公用和 Microsoft)。 您可以依自己選擇的任何順序設定對等。 不過，您必須確定您完成每個對等互連一次一個的 hello 設定。 

## <a name="azure-private-peering"></a>Azure 私用對等

本節可協助您建立、 取得、 更新和刪除 hello Azure ExpressRoute 循環的私用對等設定。

### <a name="toocreate-azure-private-peering"></a>toocreate Azure 私人互連

1. 匯入 ExpressRoute hello PowerShell 模組。

  您必須安裝 hello 最新 PowerShell 安裝程式從[PowerShell 資源庫](http://www.powershellgallery.com/)hello Azure Resource Manager 模組匯入 hello 順序 toostart 使用 hello ExpressRoute cmdlet 中的 PowerShell 工作階段。 您必須以系統管理員身分 toorun PowerShell。

  ```powershell
  Install-Module AzureRM
  Install-AzureRM
  ```

  匯入所有 hello AzureRM.* 模組 hello 已知的語意版本範圍內。

  ```powershell
  Import-AzureRM
  ```

  您也可以匯入選取的模組 hello 已知的語意版本範圍內。

  ```powershell
  Import-Module AzureRM.Network 
  ```

  登入 tooyour 帳戶。

  ```powershell
  Login-AzureRmAccount
  ```

  選取您想 toocreate ExpressRoute 電路的 hello 訂用帳戶。

  ```powershell
  Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. 建立 ExpressRoute 線路。

  請遵循 hello 指示 toocreate [ExpressRoute 電路](expressroute-howto-circuit-arm.md)，並讓它佈建的 hello 連線服務提供者。

  如果您連線服務提供者提供受管理的第 3 層服務，您可以要求您連線提供者 tooenable 私用對等互連，為您的 Azure。 在此情況下，您不需要 toofollow hello 下一節中所列的指示。 不過，如果您連線服務提供者不會管理路由，在建立您的循環之後繼續您 hello 後續步驟的組態。
3. 請檢查 hello ExpressRoute 電路 toomake 確定佈建，而且也已啟用。 下列範例使用 hello:

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  hello 回應是類似 toohello 下列範例：

  ```
  Name                             : ExpressRouteARMCircuit
  ResourceGroupName                : ExpressRouteResourceGroup
  Location                         : westus
  Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
  Etag                             : W/"################################"
  ProvisioningState                : Succeeded
  Sku                              : {
                                       "Name": "Standard_MeteredData",
                                       "Tier": "Standard",
                                       "Family": "MeteredData"
                                     }
  CircuitProvisioningState         : Enabled
  ServiceProviderProvisioningState : Provisioned
  ServiceProviderNotes             : 
  ServiceProviderProperties        : {
                                       "ServiceProviderName": "Equinix",
                                       "PeeringLocation": "Silicon Valley",
                                       "BandwidthInMbps": 200
                                     }
  ServiceKey                       : **************************************
  Peerings                         : []
  ```
4. 設定 Azure 私用對等互連 hello 循環。 請確定您具備下列項目，再繼續進行下一個步驟的 hello hello:

  * / 30 子網路 hello 主要連結。 hello 子網路不能保留的虛擬網路的任何位址空間的一部分。
  * / 30 hello 次要連結的子網路。 hello 子網路不能保留的虛擬網路的任何位址空間的一部分。
  * 有效的 VLAN ID tooestablish 此對等。 請確認沒有其他對等互連中 hello 循環使用 hello 相同 VLAN id。
  * 對等的 AS 編號。 您可以使用 2 位元組和 4 位元組 AS 編號。 您可以將私用 AS 編號用於此對等。 請確定您不是使用 65515。
  * **選用-**如果您選擇其中一個 toouse 的 MD5 雜湊。

  使用下列範例 tooconfigure Azure 私用對等互連，為您的電路的 hello:

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  如果您選擇 toouse MD5 雜湊時，使用下列範例中的 hello:

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200  -SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > 請確定您將 AS 編號指定為對等 ASN，而不是客戶 ASN。
  > 
  >

### <a name="tooview-azure-private-peering-details"></a>tooview Azure 私用對等互連的詳細資料

您可以使用下列範例中的 hello，以取得設定的詳細資訊：

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -Circuit $ckt
```

### <a name="tooupdate-azure-private-peering-configuration"></a>tooupdate Azure 私用對等組態

您可以更新使用下列範例中的 hello hello 設定的任何部分。 在此範例中，從 100 too500 正在更新 hello hello 循環的 VLAN ID。

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt -PeeringType AzurePrivatePeering -PeerASN 100 -PrimaryPeerAddressPrefix "10.0.0.0/30" -SecondaryPeerAddressPrefix "10.0.0.4/30" -VlanId 200

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="toodelete-azure-private-peering"></a>toodelete Azure 私人互連

您可以執行下列範例中的 hello 來移除您對等的設定：

> [!WARNING]
> 您必須確定所有虛擬網路，然後再執行此範例會從 hello ExpressRoute 電路取消連結。 
> 
> 

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePrivatePeering" -ExpressRouteCircuit $ckt

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="azure-public-peering"></a>Azure 公用對等

本節可協助您建立、 取得、 更新和刪除 hello Azure ExpressRoute 循環的公用對等設定。

### <a name="toocreate-azure-public-peering"></a>toocreate Azure 公用對等互連

1. 匯入 ExpressRoute hello PowerShell 模組。

  您必須安裝 hello 最新 PowerShell 安裝程式從[PowerShell 資源庫](http://www.powershellgallery.com/)hello Azure Resource Manager 模組匯入 hello 順序 toostart 使用 hello ExpressRoute cmdlet 中的 PowerShell 工作階段。 您必須以系統管理員身分 toorun PowerShell。

  ```powershell
  Install-Module AzureRM

  Install-AzureRM
```

  匯入所有 hello AzureRM.* 模組 hello 已知的語意版本範圍內。

  ```powershell
  Import-AzureRM
  ```

  您也可以匯入選取的模組 hello 已知的語意版本範圍內。

  ```powershell
  Import-Module AzureRM.Network
```

  登入 tooyour 帳戶。

  ```powershell
  Login-AzureRmAccount
  ```

  選取您想 toocreate ExpressRoute 電路的 hello 訂用帳戶。

  ```powershell
  Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. 建立 ExpressRoute 線路。

  請遵循 hello 指示 toocreate [ExpressRoute 電路](expressroute-howto-circuit-arm.md)，並讓它佈建的 hello 連線服務提供者。

  如果您連線服務提供者提供受管理的第 3 層服務，您可以要求您連線提供者 tooenable 私用對等互連，為您的 Azure。 在此情況下，您不需要 toofollow hello 下一節中所列的指示。 不過，如果您連線服務提供者不會管理路由，在建立您的循環之後繼續您 hello 後續步驟的組態。
3. 請檢查已佈建並也啟用 hello ExpressRoute 電路 tooensure。 下列範例使用 hello:

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  hello 回應是類似 toohello 下列範例：

  ```
  Name                             : ExpressRouteARMCircuit
  ResourceGroupName                : ExpressRouteResourceGroup
  Location                         : westus
  Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
  Etag                             : W/"################################"
  ProvisioningState                : Succeeded
  Sku                              : {
                                      "Name": "Standard_MeteredData",
                                       "Tier": "Standard",
                                       "Family": "MeteredData"
                                     }
  CircuitProvisioningState         : Enabled
  ServiceProviderProvisioningState : Provisioned
  ServiceProviderNotes             : 
  ServiceProviderProperties        : {
                                       "ServiceProviderName": "Equinix",
                                       "PeeringLocation": "Silicon Valley",
                                       "BandwidthInMbps": 200
                                     }
  ServiceKey                       : **************************************
  Peerings                         : []
  ```
4. 設定 Azure 公用對等互連 hello 循環。 請確定您擁有 hello 繼續接下來，下列資訊。

  * / 30 子網路 hello 主要連結。 這必須是有效的公用 IPv4 首碼。
  * / 30 hello 次要連結的子網路。 這必須是有效的公用 IPv4 首碼。
  * 有效的 VLAN ID tooestablish 此對等。 請確認沒有其他對等互連中 hello 循環使用 hello 相同 VLAN id。
  * 對等的 AS 編號。 您可以使用 2 位元組和 4 位元組 AS 編號。
  * **選用-**如果您選擇其中一個 toouse 的 MD5 雜湊。

  執行下列範例 tooconfigure Azure 公用對等互連，為您的電路的 hello

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "12.0.0.0/30" -SecondaryPeerAddressPrefix "12.0.0.4/30" -VlanId 100

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  如果您選擇 toouse MD5 雜湊時，使用下列範例中的 hello:

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "12.0.0.0/30" -SecondaryPeerAddressPrefix "12.0.0.4/30" -VlanId 100  -SharedKey "A1B2C3D4"

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

  > [!IMPORTANT]
  > 請確定您將 AS 編號指定為對等 ASN，而不是客戶 ASN。
  > 
  >

### <a name="tooview-azure-public-peering-details"></a>tooview Azure 公用對等互連的詳細資料

就可以使用下列 cmdlet 的 hello 設定詳細資料：

```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

  Get-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -Circuit $ckt
  ```

### <a name="tooupdate-azure-public-peering-configuration"></a>tooupdate Azure 公用對等組態

您可以更新使用下列範例中的 hello hello 設定的任何部分。 在此範例中，從 200 too600 正在更新 hello hello 循環的 VLAN ID。

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig  -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt -PeeringType AzurePublicPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 600

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="toodelete-azure-public-peering"></a>toodelete Azure 公用對等互連

您可以執行下列範例中的 hello 來移除您對等的設定：

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "AzurePublicPeering" -ExpressRouteCircuit $ckt
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="microsoft-peering"></a>Microsoft 對等互連

本節可協助您建立、 取得、 更新和刪除 ExpressRoute 循環的 hello Microsoft 對等設定。

> [!IMPORTANT]
> Microsoft 對等互連的 ExpressRoute 電路已設定先前 tooAugust 1，2017年必須透過 hello Microsoft 對等互連，公告的所有服務首碼，即使未定義路由篩選器。 Microsoft 對等互連的當天或之後 2017 年 8 月 1，已設定的 ExpressRoute 電路並不會有任何前置詞通告的路由篩選器連接直到 toohello 循環。 如需詳細資訊，請參閱[設定 Microsoft 對等互連的路由篩選](how-to-routefilter-powershell.md)。
> 
> 

### <a name="toocreate-microsoft-peering"></a>toocreate Microsoft 對等互連

1. 匯入 ExpressRoute hello PowerShell 模組。

  您必須安裝 hello 最新 PowerShell 安裝程式從[PowerShell 資源庫](http://www.powershellgallery.com/)hello Azure Resource Manager 模組匯入 hello 順序 toostart 使用 hello ExpressRoute cmdlet 中的 PowerShell 工作階段。 您必須以系統管理員身分 toorun PowerShell。

  ```powershell
  Install-Module AzureRM

  Install-AzureRM
  ```

  匯入所有 hello AzureRM.* 模組 hello 已知的語意版本範圍內。

  ```powershell
  Import-AzureRM
  ```

  您也可以匯入選取的模組 hello 已知的語意版本範圍內。

  ```powershell
  Import-Module AzureRM.Network
  ```

  登入 tooyour 帳戶。

  ```powershell
  Login-AzureRmAccount
  ```

  選取您想 toocreate ExpressRoute 電路的 hello 訂用帳戶。

  ```powershell
Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
  ```
2. 建立 ExpressRoute 線路。

  請遵循 hello 指示 toocreate [ExpressRoute 電路](expressroute-howto-circuit-arm.md)，並讓它佈建的 hello 連線服務提供者。

  如果您連線服務提供者提供受管理的第 3 層服務，您可以要求您連線提供者 tooenable 私用對等互連，為您的 Azure。 在此情況下，您不需要 toofollow hello 下一節中所列的指示。 不過，如果您連線服務提供者不會管理路由，在建立您的循環之後繼續您 hello 後續步驟的組態。
3. 請檢查 hello ExpressRoute 電路 toomake 確定佈建，而且也已啟用。 下列範例使用 hello:

  ```powershell
  Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
  ```

  hello 回應是類似 toohello 下列範例：

  ```
  Name                             : ExpressRouteARMCircuit
  ResourceGroupName                : ExpressRouteResourceGroup
  Location                         : westus
  Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
  Etag                             : W/"################################"
  ProvisioningState                : Succeeded
  Sku                              : {
                                       "Name": "Standard_MeteredData",
                                       "Tier": "Standard",
                                       "Family": "MeteredData"
                                     }
  CircuitProvisioningState         : Enabled
  ServiceProviderProvisioningState : Provisioned
  ServiceProviderNotes             : 
  ServiceProviderProperties        : {
                                       "ServiceProviderName": "Equinix",
                                       "PeeringLocation": "Silicon Valley",
                                       "BandwidthInMbps": 200
                                     }
  ServiceKey                       : **************************************
  Peerings                         : []
  ```
4. 設定 Microsoft 對等互連 hello 循環。 請確定您擁有 hello 下列資訊才能繼續。

  * / 30 子網路 hello 主要連結。 這必須是您所擁有且註冊在 RIR / IRR 中的有效公用 IPv4 首碼。
  * / 30 hello 次要連結的子網路。 這必須是您所擁有且註冊在 RIR / IRR 中的有效公用 IPv4 首碼。
  * 有效的 VLAN ID tooestablish 此對等。 請確認沒有其他對等互連中 hello 循環使用 hello 相同 VLAN id。
  * 對等的 AS 編號。 您可以使用 2 位元組和 4 位元組 AS 編號。
  * 通告前置詞： 您必須提供清單的所有前置詞您計劃 tooadvertise 透過 hello BGP 工作階段。 只接受公用 IP 位址首碼。 如果您計劃 toosend 一組前置詞，您可以傳送的逗號分隔清單。 這些前置詞必須是已註冊的 tooyou 在 RIR / IRR。
  * **選用-**客戶 ASN： 如果您不是數字的已註冊的 toohello 對等互連的廣告前置詞，您可以指定 hello 為其所註冊的數字 toowhich。
  * 路由登錄名稱： 您可以指定 hello RIR / IRR 哪些 hello 做為數字，但前置詞會註冊。
  * **選用-**如果您選擇其中一個 toouse 的 MD5 雜湊。

   使用下列範例 tooconfigure Microsoft 對等互連為您的電路的 hello:

  ```powershell
  Add-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt -PeeringType MicrosoftPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 300 -MicrosoftConfigAdvertisedPublicPrefixes "123.1.0.0/24" -MicrosoftConfigCustomerAsn 23 -MicrosoftConfigRoutingRegistryName "ARIN"

  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

### <a name="tooget-microsoft-peering-details"></a>tooget Microsoft 對等詳細資料

就可以使用下列範例中的 hello 設定詳細資料：

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

Get-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt
```

### <a name="tooupdate-microsoft-peering-configuration"></a>tooupdate Microsoft 對等組態

您可以更新使用下列範例中的 hello hello 設定的任何部分：

```powershell
Set-AzureRmExpressRouteCircuitPeeringConfig  -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt -PeeringType MicrosoftPeering -PeerASN 100 -PrimaryPeerAddressPrefix "123.0.0.0/30" -SecondaryPeerAddressPrefix "123.0.0.4/30" -VlanId 300 -MicrosoftConfigAdvertisedPublicPrefixes "124.1.0.0/24" -MicrosoftConfigCustomerAsn 23 -MicrosoftConfigRoutingRegistryName "ARIN"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="toodelete-microsoft-peering"></a>toodelete Microsoft 對等互連

您可以藉由執行下列 cmdlet 的 hello 移除您對等的設定：

```powershell
Remove-AzureRmExpressRouteCircuitPeeringConfig -Name "MicrosoftPeering" -ExpressRouteCircuit $ckt

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

## <a name="next-steps"></a>後續步驟

下一步，[連結 VNet tooan ExpressRoute 電路](expressroute-howto-linkvnet-arm.md)。

* 如需 ExpressRoute 工作流程的詳細資訊，請參閱 [ExpressRoute 工作流程](expressroute-workflows.md)。
* 如需線路對等的詳細資訊，請參閱 [ExpressRoute 線路和路由網域](expressroute-circuit-peerings.md)。
* 如需使用虛擬網路的詳細資訊，請參閱 [虛擬網路概觀](../virtual-network/virtual-networks-overview.md)。
