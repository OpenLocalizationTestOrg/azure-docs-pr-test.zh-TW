---
title: "建立和修改 ExpressRoute 線路：PowerShell：Azure Resource Manager | Microsoft Docs"
description: "本文說明如何 toocreate，佈建、 驗證、 更新、 刪除和取消佈建 ExpressRoute 電路。"
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f997182e-9b25-4a7a-b079-b004221dadcc
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 8d76c577a9cffdd393abac1b76cccc27d92e9e62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-an-expressroute-circuit-using-powershell"></a>使用 PowerShell 建立和修改 ExpressRoute 線路
> [!div class="op_single_selector"]
> * [Azure 入口網站](expressroute-howto-circuit-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-circuit-arm.md)
> * [Azure CLI](howto-circuit-cli.md)
> * [影片 - Azure 入口網站](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [PowerShell (傳統)](expressroute-howto-circuit-classic.md)
>

本文說明如何 toocreate Azure ExpressRoute 電路使用 PowerShell cmdlet 和 hello Azure Resource Manager 部署模型。 本文也會顯示 hello 電路 toocheck hello 狀態如何更新，或刪除，並取消佈建它。

## <a name="before-you-begin"></a>開始之前
* 安裝 hello hello Azure 資源管理員的 PowerShell 指令程式最新版本。 如需詳細資訊，請參閱 [Azure PowerShell 概觀](/powershell/azure/overview)。
* 檢閱 hello[必要條件](expressroute-prerequisites.md)和[工作流程](expressroute-workflows.md)開始設定之前。


## <a name="create-and-provision-an-expressroute-circuit"></a>建立和佈建 ExpressRoute 線路
### <a name="1-sign-in-tooyour-azure-account-and-select-your-subscription"></a>1.登入 tooyour Azure 帳戶並選取您的訂用帳戶
toobegin 您的設定，登入 tooyour Azure 帳戶。 使用下列範例 toohelp 您連接的 hello:

```powershell
Login-AzureRmAccount
```

核取 hello 訂閱 hello 帳戶：

```powershell
Get-AzureRmSubscription
```

選取您想的 toocreate ExpressRoute 電路的 hello 訂用帳戶：

```powershell
Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
```

### <a name="2-get-hello-list-of-supported-providers-locations-and-bandwidths"></a>2.取得支援的提供者、 位置及頻寬 hello 清單
建立 ExpressRoute 電路之前，您需要支援的連線提供者、 位置及頻寬選項的 hello 清單。

hello PowerShell cmdlet **Get AzureRmExpressRouteServiceProvider**傳回這項資訊在稍後步驟中，您將使用：

```powershell
Get-AzureRmExpressRouteServiceProvider
```

請檢查 toosee，如果您連線服務提供者已列於此處。 記下 hello 下列資訊。 稍後當您建立線路時，將會需要用到它。

* 名稱
* PeeringLocations
* BandwidthsOffered

您現在準備好 toocreate ExpressRoute 電路。   

### <a name="3-create-an-expressroute-circuit"></a>3.建立 ExpressRoute 線路
若您還沒有資源群組，您必須在建立 ExpressRoute 線路之前建立一個。 您可以藉由執行下列命令的 hello:

```powershell
New-AzureRmResourceGroup -Name "ExpressRouteResourceGroup" -Location "West US"
```


hello 下列範例示範透過在美國矽谷 Equinix toocreate 200 Mbps ExpressRoute 電路的方式。 如果您使用不同的提供者和不同的設定，請在您提出要求時替換成該資訊。 hello 下面是新的服務金鑰的要求範例：

```powershell
New-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup" -Location "West US" -SkuTier Standard -SkuFamily MeteredData -ServiceProviderName "Equinix" -PeeringLocation "Silicon Valley" -BandwidthInMbps 200
```

請確定您指定正確 SKU 層 hello 和 SKU 系列：

* SKU 層會判斷 ExpressRoute 標準或 ExpressRoute 高階附加元件是否啟用。 您可以指定*標準*tooget hello 標準 SKU 或*Premium* hello premium 附加元件。
* SKU 系列決定 hello 計費的型別。 您可以指定 [Metereddata] 以採用計量付費數據傳輸方案，選取 [Unlimiteddata] 以採用無限行動數據方案。 您可以變更從 hello 計費類型*Metereddata*太*Unlimiteddata*，但是您無法變更 hello 類型從*Unlimiteddata*太*Metereddata*.

> [!IMPORTANT]
> ExpressRoute 電路將計費 hello 發出服務金鑰的時間。 請確定您執行此作業，準備好 tooprovision hello 電路 hello 連線服務提供者時。
> 
> 

hello 回應包含 hello 服務金鑰。 您可以藉由執行下列命令的 hello 取得所有 hello 參數的詳細的說明：

```powershell
get-help New-AzureRmExpressRouteCircuit -detailed
```


### <a name="4-list-all-expressroute-circuits"></a>4.列出所有 ExpressRoute 循環
一份所有 hello 您建立 ExpressRoute 電路 tooget 執行 hello **Get AzureRmExpressRouteCircuit**命令：

```powershell
Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
```

hello 回應看起來類似下列範例的 toohello:

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
    CircuitProvisioningState          : Enabled
    ServiceProviderProvisioningState  : NotProvisioned
    ServiceProviderNotes              :
    ServiceProviderProperties         : {
                                          "ServiceProviderName": "Equinix",
                                          "PeeringLocation": "Silicon Valley",
                                          "BandwidthInMbps": 200
                                        }
    ServiceKey                        : **************************************
    Peerings                          : []

您可以擷取這項資訊在任何時候使用 hello `Get-AzureRmExpressRouteCircuit` cmdlet。 進行呼叫不含任何參數的 hello 列出 hello 的所有電路。 您的服務金鑰將會列在 hello *ServiceKey*欄位：

```powershell
Get-AzureRmExpressRouteCircuit
```


hello 回應看起來類似下列範例的 toohello:

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
    ServiceProviderProvisioningState : NotProvisioned
    ServiceProviderNotes             :
    ServiceProviderProperties        : {
                                         "ServiceProviderName": "Equinix",
                                         "PeeringLocation": "Silicon Valley",
                                         "BandwidthInMbps": 200
                                          }
    ServiceKey                       : **************************************
    Peerings                         : []


您可以藉由執行下列命令的 hello 取得所有 hello 參數的詳細的說明：

```powershell
get-help Get-AzureRmExpressRouteCircuit -detailed
```

### <a name="5-send-hello-service-key-tooyour-connectivity-provider-for-provisioning"></a>5.佈建傳送嗨服務金鑰 tooyour 連線服務提供者
*ServiceProviderProvisioningState*提供 hello 的佈建 hello 服務提供者端的目前狀態的相關資訊。 狀態提供 hello Microsoft 戶端 hello 狀態。 如需循環的佈建狀態的詳細資訊，請參閱 hello[工作流程](expressroute-workflows.md#expressroute-circuit-provisioning-states)發行項。

當您建立新的 ExpressRoute 電路時，hello 電路將處於下列狀態的 hello:

    ServiceProviderProvisioningState : NotProvisioned
    CircuitProvisioningState         : Enabled



hello 循環會變更 toohello hello 連線服務提供者會在您啟用的 hello 程序中時，下列狀態：

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled

您 toobe 無法 toouse ExpressRoute 電路，它必須處於下列狀態的 hello:

    ServiceProviderProvisioningState : Provisioned
    CircuitProvisioningState         : Enabled

### <a name="6-periodically-check-hello-status-and-hello-state-of-hello-circuit-key"></a>6.定期檢查 hello 狀態和 hello 循環索引鍵 hello 狀態
檢查 hello 狀態和 hello 循環索引鍵 hello 狀態，可讓您了解您的提供者已啟用您的循環時間。 在設定 hello 循環之後， *ServiceProviderProvisioningState*會顯示為*已佈建*hello 下列範例所示：

```powershell
Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
```


hello 回應看起來類似下列範例的 toohello:

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

### <a name="7-create-your-routing-configuration"></a>7.建立路由組態
如需逐步指示，請參閱 hello [ExpressRoute 電路的路由組態](expressroute-howto-routing-arm.md)文章 toocreate 和修改循環的對等互連。

> [!IMPORTANT]
> 這些說明僅適用於 toocircuits 與提供層級 2 連線服務的服務提供者所建立。 如果您使用的服務提供者是提供受管理的第 3 層服務 (通常是 IP VPN，如 MPLS)，您的連線提供者會為您設定和管理路由。
> 
> 

### <a name="8-link-a-virtual-network-tooan-expressroute-circuit"></a>8.連結虛擬網路 tooan ExpressRoute 電路
接下來，將虛擬網路 tooyour ExpressRoute 電路的連結。 使用 hello[連結虛擬網路 tooExpressRoute 電路](expressroute-howto-linkvnet-arm.md)處理 hello Resource Manager 部署模型時，發行項。

## <a name="getting-hello-status-of-an-expressroute-circuit"></a>取得 hello 狀態的 ExpressRoute 電路
您可以擷取這項資訊在任何時候使用 hello **Get AzureRmExpressRouteCircuit** cmdlet。 進行呼叫不含任何參數的 hello 列出 hello 的所有電路。

```powershell
Get-AzureRmExpressRouteCircuit
```


hello 回應將類似下列範例的 toohello:

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


您可以取得有關特定的 ExpressRoute 電路並 hello 資源群組名稱和循環名稱傳遞為參數 toohello 呼叫：

```powershell
Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
```


hello 回應看起來類似下列範例的 toohello:

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


您可以藉由執行下列命令的 hello 取得所有 hello 參數的詳細的說明：

```powershell
get-help get-azurededicatedcircuit -detailed
```

## <a name="modify"></a>修改 ExpressRoute 線路
您可以修改 ExpressRoute 線路的某些屬性，而不會影響連線。

您可以 hello 遵循不中斷的情況：

* 啟用或停用 ExpressRoute 線路的 ExpressRoute 進階附加元件。
* 增加 hello 頻寬的 ExpressRoute 電路提供 hello 連接埠的容量不足。 不支援降級 hello 電路頻寬。 
* 變更計量計劃的計量資料 tooUnlimited 資料 hello。 變更計量計劃的資料不支援無限制的資料 tooMetered hello。
* 您可以啟用和停用 [允許傳統作業]。

如需有關限制和限制的詳細資訊，請參閱 toohello [ExpressRoute 常見問題集](expressroute-faqs.md)。

### <a name="tooenable-hello-expressroute-premium-add-on"></a>tooenable hello ExpressRoute 高階的附加元件
您可以使用下列 PowerShell 程式碼片段的 hello，為您現有的電路啟用 hello ExpressRoute premium add-on:

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.Sku.Tier = "Premium"
$ckt.sku.Name = "Premium_MeteredData"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

hello 電路現在會有 hello ExpressRoute 高階附加元件功能已啟用。 我們將會開始計費您 hello premium 附加元件的功能，儘速 hello 命令已順利執行。

### <a name="toodisable-hello-expressroute-premium-add-on"></a>toodisable hello ExpressRoute 高階的附加元件
> [!IMPORTANT]
> 如果您使用大於 hello 標準循環所允許的資源，這項作業可能會失敗。
> 
> 

請注意 hello 下列：

* 您從 premium toostandard 降級之前，您必須確定虛擬網路連結的 hello 數目 toohello 循環為小於 10。 如果您不這樣做，更新要求就會失敗，且我們會以進階費率計費。
* 您必須取消連結其他地理政治區域中的所有虛擬網路。 如果您不這樣做，更新要求就會失敗，且我們會以進階費率計費。
* 就私用對等設定而言，路由表必須少於 4000 個路由。 如果您的路由表的大小大於 4000 路由，hello BGP 工作階段卸除，並不會重新啟用，直到 hello 公告的首碼數目，低於 4000。

您可以使用下列 PowerShell cmdlet 的 hello，停用 hello ExpressRoute premium add-on hello 現有循環：

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.Sku.Tier = "Standard"
$ckt.sku.Name = "Standard_MeteredData"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="tooupdate-hello-expressroute-circuit-bandwidth"></a>tooupdate hello ExpressRoute 電路頻寬
如需針對您的提供者支援的頻寬選項，請檢查 hello [ExpressRoute 常見問題集](expressroute-faqs.md)。 您可以挑選任何比您現有的循環 hello 大小更大的大小。

> [!IMPORTANT]
> 如果 hello 現有的連接埠上有足夠的容量，您可能必須 toorecreate hello ExpressRoute 電路。 如果沒有任何額外的容量可在該位置，您無法升級 hello 循環。
>
> 您無法減少 hello 頻寬的 ExpressRoute 電路不會中斷。 降級頻寬 toodeprovision hello ExpressRoute 循環會要求您，並再重新佈建新增的 ExpressRoute 電路。
> 

決定您需要的大小之後，請使用下列命令 tooresize hello 您的循環：

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.ServiceProviderProperties.BandwidthInMbps = 1000

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```


您的電路將調整大小 hello Microsoft 一邊。 然後您必須連絡其端 toomatch 您連接的提供者 tooupdate 設定這項變更。 此通知之後，我們將會開始計費您更新的 hello 頻寬選項。

### <a name="toomove-hello-sku-from-metered-toounlimited"></a>從付費 toounlimited toomove hello SKU
您可以使用下列 PowerShell 程式碼片段的 hello 變更 hello 的 ExpressRoute 電路 SKU:

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.Sku.Family = "UnlimitedData"
$ckt.sku.Name = "Premium_UnlimitedData"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="toocontrol-access-toohello-classic-and-resource-manager-environments"></a>toocontrol 存取 toohello 傳統和資源管理員環境
檢閱中的 hello 指示[從 hello 傳統 toohello Resource Manager 部署模型的移動 ExpressRoute 電路](expressroute-howto-move-arm.md)。  

## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a>取消佈建和刪除 ExpressRoute 線路
請注意 hello 下列：

* 您必須取消連結從 hello ExpressRoute 電路的所有虛擬網路。 如果此作業失敗，請檢查 toosee 如果任何虛擬網路連結 toohello 循環。
* 如果 hello ExpressRoute 電路服務提供者佈建狀態為**佈建**或**已佈建**您必須使用您的服務提供者 toodeprovision hello 電路邊。 我們將繼續 tooreserve 資源，並向您收取費用，直到完成取消佈建 hello 電路 hello 服務提供者，並通知我們。
* 如果 hello 服務提供者已解除佈建 hello 循環 (hello 佈建狀態的服務提供者設定得**未佈建**) 可接著刪除 hello 循環。 這會停止計費 hello 循環

若要刪除 ExpressRoute 電路，您可以執行下列命令的 hello:

```powershell
Remove-AzureRmExpressRouteCircuit -ResourceGroupName "ExpressRouteResourceGroup" -Name "ExpressRouteARMCircuit"
```

## <a name="next-steps"></a>後續步驟

建立您的循環之後，請確定您執行 hello 遵循：

* [建立和修改 ExpressRoute 線路的路由](expressroute-howto-routing-arm.md)
* [連結您的虛擬網路 tooyour ExpressRoute 電路](expressroute-howto-linkvnet-arm.md)
