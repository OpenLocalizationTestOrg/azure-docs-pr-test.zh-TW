---
title: "建立和修改 ExpressRoute 線路︰PowerShell：Azure 傳統| Microsoft Docs"
description: "這篇文章會引導您完成建立及佈建 ExpressRoute 循環的 hello 步驟。 本文也會顯示 toocheck hello 狀態如何更新或刪除和取消佈建您的電路。"
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 0134d242-6459-4dec-a2f1-4657c3bc8b23
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/21/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 9897c88776a2153ba22aa9ff328becb9f12b660b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-an-expressroute-circuit-using-powershell-classic"></a>使用 PowerShell 建立和修改 ExpressRoute 線路 (傳統)
> [!div class="op_single_selector"]
> * [Azure 入口網站](expressroute-howto-circuit-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-circuit-arm.md)
> * [Azure CLI](howto-circuit-cli.md)
> * [影片 - Azure 入口網站](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [PowerShell (傳統)](expressroute-howto-circuit-classic.md)
>

這篇文章會引導您透過 hello 步驟 toocreate Azure ExpressRoute 循環使用 PowerShell cmdlet 和 hello 傳統部署模型。 本文也會顯示 toocheck hello 狀態如何更新或刪除和取消佈建 ExpressRoute 電路。

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]


**關於 Azure 部署模型**

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="before-you-begin"></a>開始之前
### <a name="step-1-review-hello-prerequisites-and-workflow-articles"></a>步驟 1. 檢閱 hello 必要條件和工作流程發行項
請確定您已經檢閱 hello[必要條件](expressroute-prerequisites.md)和[工作流程](expressroute-workflows.md)開始設定之前。  

### <a name="step-2-install-hello-latest-versions-of-hello-azure-service-management-sm-powershell-modules"></a>步驟 2. 安裝 hello hello Azure 服務管理 (SM) PowerShell 模組最新版本
請依照下列中的 hello 指示[開始使用 Azure PowerShell 指令程式](/powershell/azure/overview)的逐步指示如何 tooconfigure 電腦 toouse hello Azure PowerShell 模組。

### <a name="step-3-log-in-tooyour-azure-account-and-select-a-subscription"></a>步驟 3. 登入 tooyour Azure 帳戶，然後選取訂用帳戶
1. 使用提高的權限開啟 PowerShell 主控台和 tooyour 帳戶連接。 使用下列範例 toohelp 您連接的 hello:

        Login-AzureRmAccount

2. 請檢查 hello hello 帳戶的訂用帳戶。

        Get-AzureRmSubscription

3. 如果您有多個訂閱，選取您想 toouse hello 訂用帳戶。

        Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"

4. 接下來，使用下列 cmdlet tooadd hello Azure 訂用帳戶 tooPowerShell hello 傳統部署模型。

        Add-AzureAccount

## <a name="create-and-provision-an-expressroute-circuit"></a>建立和佈建 ExpressRoute 線路
### <a name="step-1-import-hello-powershell-modules-for-expressroute"></a>步驟 1. Hello PowerShell 模組匯入 expressroute
 如果您尚未這樣做，必須以 hello PowerShell 工作階段中使用 hello ExpressRoute cmdlet 的順序 toostart 匯 hello Azure 和 ExpressRoute 模組。 您匯入 hello 模組 hello 從它們的位置安裝 tooon 本機電腦。 您可以根據 hello 方法使用 tooinstall hello 模組，可能不同於下列範例所示的 hello hello 位置。 如有必要，請修改 hello 範例。  

    Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
    Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'

### <a name="step-2-get-hello-list-of-supported-providers-locations-and-bandwidths"></a>步驟 2. 取得支援的提供者、 位置及頻寬 hello 清單
建立 ExpressRoute 電路之前，您需要支援的連線提供者、 位置及頻寬選項的 hello 清單。

hello PowerShell cmdlet`Get-AzureDedicatedCircuitServiceProvider`傳回這項資訊在稍後步驟中，您將使用：

    Get-AzureDedicatedCircuitServiceProvider

請檢查 toosee，如果您連線服務提供者已列於此處。 請記下的下列資訊，因為您將需要它稍後建立電路的 hello:

* 名稱
* PeeringLocations
* BandwidthsOffered

您現在準備好 toocreate ExpressRoute 電路。         

### <a name="step-3-create-an-expressroute-circuit"></a>步驟 3. 建立 ExpressRoute 線路
hello 下列範例示範透過在美國矽谷 Equinix toocreate 200 Mbps ExpressRoute 電路的方式。 如果您使用不同的提供者和不同的設定，請在您提出要求時替換成該資訊。

> [!IMPORTANT]
> ExpressRoute 電路將計費 hello 發出服務金鑰的時間。 請確定您執行此作業，準備好 tooprovision hello 電路 hello 連線服務提供者時。
> 
> 

hello 下面是新的服務金鑰的要求範例：

    $Bandwidth = 200
    $CircuitName = "MyTestCircuit"
    $ServiceProvider = "Equinix"
    $Location = "Silicon Valley"

    New-AzureDedicatedCircuit -CircuitName $CircuitName -ServiceProviderName $ServiceProvider -Bandwidth $Bandwidth -Location $Location -sku Standard -BillingType MeteredData

或者，如果您想 toocreate ExpressRoute 電路 hello 高階的附加元件，使用 hello 下列範例。 請參閱 toohello [ExpressRoute 常見問題集](expressroute-faqs.md)如需詳細資訊 hello premium 附加元件。

    New-AzureDedicatedCircuit -CircuitName $CircuitName -ServiceProviderName $ServiceProvider -Bandwidth $Bandwidth -Location $Location -sku Premium - BillingType MeteredData


hello 回應會包含 hello 服務金鑰。 您可以取得所有 hello 參數的詳細的描述執行 hello 下列：

    get-help new-azurededicatedcircuit -detailed

### <a name="step-4-list-all-hello-expressroute-circuits"></a>步驟 4. 列出所有的 hello ExpressRoute 電路
您可以執行 hello `Get-AzureDedicatedCircuit` tooget 所有清單 hello 您建立 ExpressRoute 電路的命令：

    Get-AzureDedicatedCircuit

hello 回應將類似下列範例的 toohello:

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : NotProvisioned
    Sku                              : Standard
    Status                           : Enabled

您可以擷取這項資訊在任何時候使用 hello `Get-AzureDedicatedCircuit` cmdlet。 進行呼叫不含任何參數的 hello 列出 hello 的所有電路。 您的服務金鑰將會列在 hello *ServiceKey*欄位。

    Get-AzureDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : NotProvisioned
    Sku                              : Standard
    Status                           : Enabled

您可以取得所有 hello 參數的詳細的描述執行 hello 下列：

    get-help get-azurededicatedcircuit -detailed

### <a name="step-5-send-hello-service-key-tooyour-connectivity-provider-for-provisioning"></a>步驟 5。 佈建傳送嗨服務金鑰 tooyour 連線服務提供者
*ServiceProviderProvisioningState*提供 hello 的佈建 hello 服務提供者端的目前狀態的相關資訊。 *狀態*hello Microsoft 側邊提供 hello 狀態。 如需循環的佈建狀態的詳細資訊，請參閱 hello[工作流程](expressroute-workflows.md#expressroute-circuit-provisioning-states)發行項。

當您建立新的 ExpressRoute 電路時，hello 電路將處於下列狀態的 hello:

    ServiceProviderProvisioningState : NotProvisioned
    Status                           : Enabled


hello 電路將會移 toohello hello 連線服務提供者會在您啟用的 hello 程序中時，下列狀態：

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled

ExpressRoute 電路必須遵循您 toobe 無法 toouse 狀態 hello 它：

    ServiceProviderProvisioningState : Provisioned
    Status                           : Enabled


### <a name="step-6-periodically-check-hello-status-and-hello-state-of-hello-circuit-key"></a>步驟 6. 定期檢查 hello 狀態和 hello 循環索引鍵 hello 狀態
這樣可讓您知道提供者何時已啟用您的線路。 在設定 hello 循環之後， *ServiceProviderProvisioningState*將會顯示為*已佈建*hello 下列範例所示：

    Get-AzureDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

### <a name="step-7-create-your-routing-configuration"></a>步驟 7. 建立路由組態
請參閱 toohello [ExpressRoute 電路的路由組態 （建立和修改電路的互連）](expressroute-howto-routing-classic.md)文件以取得逐步指示。

> [!IMPORTANT]
> 這些說明僅適用於 toocircuits 與提供層級 2 連線服務的服務提供者所建立。 如果您使用的服務提供者是提供受管理的第 3 層服務 (通常是 IP VPN，如 MPLS)，您的連線提供者會為您設定和管理路由。
> 
> 

### <a name="step-8-link-a-virtual-network-tooan-expressroute-circuit"></a>步驟 8。 連結虛擬網路 tooan ExpressRoute 電路
接下來，將虛擬網路 tooyour ExpressRoute 電路的連結。 請參閱太[連結 ExpressRoute 電路 toovirtual 網路](expressroute-howto-linkvnet-classic.md)如需逐步指示。 如果您需要 toocreate hello 傳統部署模型使用 expressroute 的虛擬網路，請參閱[建立 expressroute 的虛擬網路](expressroute-howto-vnet-portal-classic.md)。

## <a name="getting-hello-status-of-an-expressroute-circuit"></a>取得 hello 狀態的 ExpressRoute 電路
您可以擷取這項資訊在任何時候使用 hello `Get-AzureCircuit` cmdlet。 進行呼叫不含任何參數的 hello 列出 hello 的所有電路。

    Get-AzureDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

    Bandwidth                        : 1000
    CircuitName                      : MyAsiaCircuit
    Location                         : Singapore
    ServiceKey                       : #################################
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

您可以傳遞做為參數 toohello 呼叫 hello 服務金鑰，以取得特定的 ExpressRoute 電路的詳細資訊。

    Get-AzureDedicatedCircuit -ServiceKey "*********************************"

    Bandwidth                        : 200
    CircuitName                      : MyTestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled


您可以藉由執行下列範例中的 hello 取得所有 hello 參數的詳細的說明：

    get-help get-azurededicatedcircuit -detailed

## <a name="modifying-an-expressroute-circuit"></a>修改 ExpressRoute 線路
您可以修改 ExpressRoute 線路的某些屬性，而不會影響連線。

您可以 hello 遵循不中斷的情況：

* 啟用或停用 ExpressRoute 線路的 ExpressRoute 進階附加元件。
* 增加 hello 頻寬的 ExpressRoute 電路提供 hello 連接埠的容量不足。 請注意，不支援降級 hello 電路頻寬。 
* 變更計量計劃的計量資料 tooUnlimited 資料 hello。 請注意該變更 hello 計量計劃從無限制的資料 tooMetered 不支援資料。
* 您可以啟用和停用 [允許傳統作業]。

請參閱 toohello [ExpressRoute 常見問題集](expressroute-faqs.md)如需有關限制和限制。

### <a name="tooenable-hello-expressroute-premium-add-on"></a>tooenable hello ExpressRoute 高階的附加元件
您可以使用下列 PowerShell cmdlet 的 hello，為您現有的電路啟用 hello ExpressRoute premium add-on:

    Set-AzureDedicatedCircuitProperties -ServiceKey "*********************************" -Sku Premium

    Bandwidth                        : 1000
    CircuitName                      : TestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Premium
    Status                           : Enabled

您的電路現在會有 hello ExpressRoute 高階附加元件功能已啟用。 請注意，我們就會啟動 hello 命令已順利執行完成後，只要您計費 hello premium 附加元件的功能。

### <a name="toodisable-hello-expressroute-premium-add-on"></a>toodisable hello ExpressRoute 高階的附加元件
> [!IMPORTANT]
> 如果您使用大於 hello 標準循環所允許的資源，這項作業可能會失敗。
> 
> 

#### <a name="considerations"></a>考量

* 您必須確定虛擬網路連結的 toohello 循環的 hello 數目小於 10 之前您從 premium toostandard 降級。 如果不這麼做，您的更新要求會失敗，，您可以使用票據的 hello 高階費率。
* 您必須取消連結其他地理政治區域中的所有虛擬網路。 如果不這麼做，您的更新要求會失敗，，您可以使用票據的 hello 高階費率。
* 就私用對等設定而言，路由表必須少於 4000 個路由。 如果您的路由表的大小大於 4000 路由，hello BGP 工作階段會卸除，並不會重新啟用，直到 hello 公告的首碼數目，低於 4000。

#### <a name="disable-hello-premium-add-on"></a>停用 hello premium 附加元件
您可以使用下列 PowerShell cmdlet 的 hello 停用 hello ExpressRoute premium add-on 您現有的循環：

    Set-AzureDedicatedCircuitProperties -ServiceKey "*********************************" -Sku Standard

    Bandwidth                        : 1000
    CircuitName                      : TestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled



### <a name="tooupdate-hello-expressroute-circuit-bandwidth"></a>tooupdate hello ExpressRoute 電路頻寬
檢查 hello [ExpressRoute 常見問題集](expressroute-faqs.md)支援您的提供者的頻寬選項。 您可以選擇大於您現有的循環 hello 大小，只要 hello （您的電路建立所在） 的實體連接埠可讓任何規模。

> [!IMPORTANT]
> 如果 hello 現有的連接埠上有足夠的容量，您可能必須 toorecreate hello ExpressRoute 電路。 如果沒有任何額外的容量可在該位置，您無法升級 hello 循環。
>
> 您無法減少 hello 頻寬的 ExpressRoute 電路不會中斷。 降級頻寬 toodeprovision hello ExpressRoute 循環會要求您，並再重新佈建新增的 ExpressRoute 電路。
> 
> 

#### <a name="resize-a-circuit"></a>調整電路大小

決定您需要的大小之後，您可以使用下列命令 tooresize hello 您的循環：

    Set-AzureDedicatedCircuitProperties -ServiceKey ********************************* -Bandwidth 1000

    Bandwidth                        : 1000
    CircuitName                      : TestCircuit
    Location                         : Silicon Valley
    ServiceKey                       : *********************************
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Sku                              : Standard
    Status                           : Enabled

您的電路將具有已調整大小 hello Microsoft 一邊。 您必須連絡其端 toomatch 您連接的提供者 tooupdate 設定這項變更。 請注意，我們將會開始計費您 hello 更新從這個點的頻寬選項上。

如果您看到下列錯誤，當增加 hello 電路頻寬的 hello，這表示那里 hello 您現有的電路建立所在的實體連接埠上保留足夠的頻寬。 您有 toodelete 這個循環，並建立新的循環，您需要的 hello 大小。 

    Set-AzureDedicatedCircuitProperties : InvalidOperation : Insufficient bandwidth available tooperform this circuit
    update operation
    At line:1 char:1
    + Set-AzureDedicatedCircuitProperties -ServiceKey ********************* ...
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : CloseError: (:) [Set-AzureDedicatedCircuitProperties], CloudException
        + FullyQualifiedErrorId : Microsoft.WindowsAzure.Commands.ExpressRoute.SetAzureDedicatedCircuitPropertiesCommand


## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a>取消佈建和刪除 ExpressRoute 線路

### <a name="considerations"></a>考量

* 您必須取消連結從 hello 這個作業 toosucceed 的 ExpressRoute 電路的所有虛擬網路。 請檢查 toosee，如果您有任何虛擬網路連結 toohello 循環，如果此作業會失敗。
* 如果 hello ExpressRoute 電路服務提供者佈建狀態為**佈建**或**已佈建**您必須使用您的服務提供者 toodeprovision hello 電路邊。 我們將繼續 tooreserve 資源，並向您收取費用，直到完成取消佈建 hello 電路 hello 服務提供者，並通知我們。
* 如果 hello 服務提供者已解除佈建 hello 循環 (hello 佈建狀態的服務提供者設定得**未佈建**) 可接著刪除 hello 循環。 這樣會停止計費 hello 循環。

#### <a name="delete-a-circuit"></a>刪除電路

若要刪除 ExpressRoute 電路，您可以執行下列命令的 hello:

    Remove-AzureDedicatedCircuit -ServiceKey "*********************************"



## <a name="next-steps"></a>後續步驟
建立您的循環之後，請確定您執行 hello 遵循：

* [建立和修改 ExpressRoute 線路的路由](expressroute-howto-routing-classic.md)
* [連結您的虛擬網路 tooyour ExpressRoute 電路](expressroute-howto-linkvnet-classic.md)

