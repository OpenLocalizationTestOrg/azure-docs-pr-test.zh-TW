---
title: "如何 tooconfigure ExpressRoute 電路的路由 （對等互連）： Azure： 傳統 |Microsoft 文件"
description: "這篇文章會引導您完成建立及佈建 hello 私人、 公用及 Microsoft 對等互連的 ExpressRoute 電路的 hello 步驟。 本文也會顯示 toocheck hello 狀態、 更新或刪除您的電路的互連的方式。"
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: a4bd39d2-373a-467a-8b06-36cfcc1027d2
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/21/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: dc5bcc4b86c3bc965a88281b6c2a660f3bc58eb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-peering-for-an-expressroute-circuit-classic"></a>建立和修改 ExpressRoute 線路的對等互連 (傳統)
> [!div class="op_single_selector"]
> * [Azure 入口網站](expressroute-howto-routing-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-routing-arm.md)
> * [Azure CLI](howto-routing-cli.md)
> * [視訊 - 私用對等互連](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [視訊 - 公用對等互連](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [視訊 - Microsoft 對等互連](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> * [PowerShell (傳統)](expressroute-howto-routing-classic.md)
> 

本文將引導您完成 hello 步驟 toocreate 並管理使用 PowerShell 和 hello 傳統部署模型的 ExpressRoute 電路的路由組態。 下列的 hello 步驟也會顯示您 toocheck hello 狀態更新，或刪除和取消佈建的 ExpressRoute 電路的互連的方式。

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

**關於 Azure 部署模型**

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]


## <a name="configuration-prerequisites"></a>組態必要條件
* 您將需要 hello 的 hello Azure 服務管理 (SM) PowerShell cmdlet 的最新版本。 如需詳細資訊，請參閱[開始使用 Azure PowerShell Cmdlet](/powershell/azure/overview)。  
* 請確定您已經檢閱 hello[必要條件](expressroute-prerequisites.md)頁面 hello[路由需求](expressroute-routing.md)頁面和 hello[工作流程](expressroute-workflows.md)頁面開始設定之前。
* 您必須擁有作用中的 ExpressRoute 線路。 請依照下列指示 hello 太[建立 ExpressRoute 電路](expressroute-howto-circuit-classic.md)和有 hello 電路啟用您的連線提供者，才能繼續。 hello ExpressRoute 電路必須位於您 toobe 無法 toorun hello cmdlet 如下所述的佈建並啟用狀態。

> [!IMPORTANT]
> 這些說明僅適用於 toocircuits 建立與服務供應項目層級 2 連線服務的提供者。 如果您使用的服務提供者是提供受管理的第 3 層服務 (通常是 IPVPN，如 MPLS)，您的連線提供者會為您設定和管理路由。
> 
> 

您可以為 ExpressRoute 線路設定一個、兩個或全部三個對等 (Azure 私用、Azure 公用和 Microsoft)。 您可以依自己選擇的任何順序設定對等。 不過，您必須確定您完成每個對等互連一次一個的 hello 設定。


### <a name="log-in-tooyour-azure-account-and-select-a-subscription"></a>登入 tooyour Azure 帳戶，然後選取訂用帳戶
1. 使用提高的權限開啟 PowerShell 主控台和 tooyour 帳戶連接。 使用下列範例 toohelp 您連接的 hello:

        Login-AzureRmAccount

2. 請檢查 hello hello 帳戶的訂用帳戶。

        Get-AzureRmSubscription

3. 如果您有多個訂閱，選取您想 toouse hello 訂用帳戶。

        Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"

4. 接下來，使用下列 cmdlet tooadd hello Azure 訂用帳戶 tooPowerShell hello 傳統部署模型。

        Add-AzureAccount


## <a name="azure-private-peering"></a>Azure 私用對等
本節提供 toocreate，如何取得、 更新和刪除 hello Azure ExpressRoute 循環的私用對等設定的指示。 

### <a name="toocreate-azure-private-peering"></a>toocreate Azure 私人互連
1. **匯入 ExpressRoute hello PowerShell 模組。**
   
    您必須匯 hello PowerShell 工作階段中使用 hello ExpressRoute cmdlet 的順序 toostart hello Azure 和 ExpressRoute 模組。 Hello 執行的下列命令 tooimport hello Azure 和 ExpressRoute 模組到 hello PowerShell 工作階段。  
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. **建立 ExpressRoute 線路。**
   
    請遵循 hello 指示 toocreate [ExpressRoute 電路](expressroute-howto-circuit-classic.md)，並讓它佈建的 hello 連線服務提供者。 如果您連線服務提供者提供受管理的第 3 層服務，您可以要求您連線提供者 tooenable 私用對等互連，為您的 Azure。 在此情況下，您不需要 toofollow hello 下一節中所列的指示。 不過，如果您連線服務提供者不會管理之後建立您的電路的路由，請遵循下列的 hello 指示。 
3. **請檢查已佈建 hello ExpressRoute 電路 tooensure。**
   
    如果佈建及也啟用 hello ExpressRoute 循環，您必須先檢查 toosee。 請參閱以下的 hello 範例。
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    請確定 hello 循環顯示已佈建與已啟用。 如果不是，使用您的連線提供者 tooget，您的循環所需的 toohello 狀態和狀態。
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. **設定 Azure 私用對等互連 hello 循環。**
   
    請確定您具備下列項目，再繼續進行下一個步驟的 hello hello:
   
   * / 30 子網路 hello 主要連結。 這不能在保留給虛擬網路的任何位址空間中。
   * / 30 hello 次要連結的子網路。 這不能在保留給虛擬網路的任何位址空間中。
   * 有效的 VLAN ID tooestablish 此對等。 請確認沒有其他對等互連中 hello 循環使用 hello 相同 VLAN id。
   * 對等的 AS 編號。 您可以使用 2 位元組和 4 位元組 AS 編號。 您可以將私用 AS 編號用於此對等。 請確定您不是使用 65515。
   * MD5 雜湊，如果您選擇其中一個 toouse。 **這是選擇性的**。
     
    您可以執行下列 cmdlet tooconfigure 為您的電路 Azure 私人互連的 hello。
     
        New-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 100
     
    如果您選擇 toouse MD5 雜湊，您可以使用下列的 hello cmdlet。
     
        New-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 100 -SharedKey "A1B2C3D4"
     
     > [!IMPORTANT]
     > 請確定您將 AS 編號指定為對等 ASN，而不是客戶 ASN。
     > 
     > 

### <a name="tooview-azure-private-peering-details"></a>tooview Azure 私用對等互連的詳細資料
就可以使用下列 cmdlet 的 hello 設定詳細資料

    Get-AzureBGPPeering -AccessType Private -ServiceKey "*********************************"

    AdvertisedPublicPrefixes       : 
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 
    PeerAsn                        : 1234
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 10.0.0.0/30
    RoutingRegistryName            : 
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 10.0.0.4/30
    State                          : Enabled
    VlanId                         : 100


### <a name="tooupdate-azure-private-peering-configuration"></a>tooupdate Azure 私用對等組態
您可以更新使用下列 cmdlet 的 hello hello 設定的任何部分。 在 hello 下列範例中，從 100 too500 正在更新 hello hello 循環的 VLAN ID。

    Set-AzureBGPPeering -AccessType Private -ServiceKey "*********************************" -PrimaryPeerSubnet "10.0.0.0/30" -SecondaryPeerSubnet "10.0.0.4/30" -PeerAsn 1234 -VlanId 500 -SharedKey "A1B2C3D4"

### <a name="toodelete-azure-private-peering"></a>toodelete Azure 私人互連
您可以藉由執行下列 cmdlet 的 hello 移除您對等的設定。

> [!WARNING]
> 您必須確定執行這個指令程式之前，所有虛擬網路是從 hello ExpressRoute 電路取消連結。 
> 
> 

    Remove-AzureBGPPeering -AccessType Private -ServiceKey "*********************************"


## <a name="azure-public-peering"></a>Azure 公用對等
本節提供 toocreate，如何取得、 更新及刪除 hello Azure ExpressRoute 循環的公用對等設定的指示。

### <a name="toocreate-azure-public-peering"></a>toocreate Azure 公用對等互連
1. **匯入 ExpressRoute hello PowerShell 模組。**
   
    您必須匯 hello PowerShell 工作階段中使用 hello ExpressRoute cmdlet 的順序 toostart hello Azure 和 ExpressRoute 模組。 Hello 執行的下列命令 tooimport hello Azure 和 ExpressRoute 模組到 hello PowerShell 工作階段。 
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. **建立 ExpressRoute 線路**
   
    請遵循 hello 指示 toocreate [ExpressRoute 電路](expressroute-howto-circuit-classic.md)，並讓它佈建的 hello 連線服務提供者。 如果您連線服務提供者提供受管理的第 3 層服務，您可以要求您連線提供者 tooenable Azure 公用對等互連。 在此情況下，您不需要 toofollow hello 下一節中所列的指示。 不過，如果您連線服務提供者不會管理之後建立您的電路的路由，請遵循下列的 hello 指示。
3. **檢查已佈建 ExpressRoute 循環 tooensure**
   
    如果佈建及也啟用 hello ExpressRoute 循環，您必須先檢查 toosee。 請參閱以下的 hello 範例。
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    請確定 hello 循環顯示已佈建與已啟用。 如果不是，使用您的連線提供者 tooget，您的循環所需的 toohello 狀態和狀態。
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. **設定 Azure 公用對等互連 hello 循環**
   
    確定您擁有 hello 繼續接下來，下列資訊。
   
   * / 30 子網路 hello 主要連結。 這必須是有效的公用 IPv4 首碼。
   * / 30 hello 次要連結的子網路。 這必須是有效的公用 IPv4 首碼。
   * 有效的 VLAN ID tooestablish 此對等。 請確認沒有其他對等互連中 hello 循環使用 hello 相同 VLAN id。
   * 對等的 AS 編號。 您可以使用 2 位元組和 4 位元組 AS 編號。
   * MD5 雜湊，如果您選擇其中一個 toouse。 **這是選擇性的**。
     
    您可以執行下列 cmdlet tooconfigure 為您的電路 Azure 公用對等的 hello
     
        New-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 200
     
    如果您選擇 toouse MD5 雜湊，您可以使用下列的 hello cmdlet
     
        New-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 200 -SharedKey "A1B2C3D4"
     
     > [!IMPORTANT]
     > 請確定您將 AS 編號指定為對等 ASN，而不是客戶 ASN。
     > 
     > 

### <a name="tooview-azure-public-peering-details"></a>tooview Azure 公用對等互連的詳細資料
就可以使用下列 cmdlet 的 hello 設定詳細資料

    Get-AzureBGPPeering -AccessType Public -ServiceKey "*********************************"

    AdvertisedPublicPrefixes       : 
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 
    PeerAsn                        : 1234
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 131.107.0.0/30
    RoutingRegistryName            : 
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 131.107.0.4/30
    State                          : Enabled
    VlanId                         : 200


### <a name="tooupdate-azure-public-peering-configuration"></a>tooupdate Azure 公用對等組態
您可以使用下列 cmdlet 的 hello hello 設定的任何部分，更新

    Set-AzureBGPPeering -AccessType Public -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -PeerAsn 1234 -VlanId 600 -SharedKey "A1B2C3D4"

正在從在上面範例中的 hello 200 too600 更新 hello hello 循環的 VLAN ID。

### <a name="toodelete-azure-public-peering"></a>toodelete Azure 公用對等互連
您可以藉由執行下列 cmdlet 的 hello 移除您對等的設定

    Remove-AzureBGPPeering -AccessType Public -ServiceKey "*********************************"

## <a name="microsoft-peering"></a>Microsoft 對等互連
本節提供 toocreate，如何取得、 更新及刪除 ExpressRoute 循環的 hello Microsoft 對等組態指示。 

### <a name="toocreate-microsoft-peering"></a>toocreate Microsoft 對等互連
1. **匯入 ExpressRoute hello PowerShell 模組。**
   
    您必須匯 hello PowerShell 工作階段中使用 hello ExpressRoute cmdlet 的順序 toostart hello Azure 和 ExpressRoute 模組。 Hello 執行的下列命令 tooimport hello Azure 和 ExpressRoute 模組到 hello PowerShell 工作階段。  
   
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
        Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
2. **建立 ExpressRoute 線路**
   
    請遵循 hello 指示 toocreate [ExpressRoute 電路](expressroute-howto-circuit-classic.md)，並讓它佈建的 hello 連線服務提供者。 如果您連線服務提供者提供受管理的第 3 層服務，您可以要求您連線提供者 tooenable 私用對等互連，為您的 Azure。 在此情況下，您不需要 toofollow hello 下一節中所列的指示。 不過，如果您連線服務提供者不會管理之後建立您的電路的路由，請遵循下列的 hello 指示。
3. **檢查已佈建 ExpressRoute 循環 tooensure**
   
    您必須先簽 toosee hello ExpressRoute 循環是否處於 已佈建且已啟用的狀態。
   
        PS C:\> Get-AzureDedicatedCircuit -ServiceKey "*********************************"
   
        Bandwidth                        : 200
        CircuitName                      : MyTestCircuit
        Location                         : Silicon Valley
        ServiceKey                       : *********************************
        ServiceProviderName              : equinix
        ServiceProviderProvisioningState : Provisioned
        Sku                              : Standard
        Status                           : Enabled
   
    請確定 hello 循環顯示已佈建與已啟用。 如果不是，使用您的連線提供者 tooget，您的循環所需的 toohello 狀態和狀態。
   
        ServiceProviderProvisioningState : Provisioned
        Status                           : Enabled
4. **設定 Microsoft 對等互連 hello 循環**
   
    請確定您擁有 hello 下列資訊才能繼續。
   
   * / 30 子網路 hello 主要連結。 這必須是您所擁有且註冊在 RIR / IRR 中的有效公用 IPv4 首碼。
   * / 30 hello 次要連結的子網路。 這必須是您所擁有且註冊在 RIR / IRR 中的有效公用 IPv4 首碼。
   * 有效的 VLAN ID tooestablish 此對等。 請確認沒有其他對等互連中 hello 循環使用 hello 相同 VLAN id。
   * 對等的 AS 編號。 您可以使用 2 位元組和 4 位元組 AS 編號。
   * 通告前置詞： 您必須提供清單的所有前置詞您計劃 tooadvertise 透過 hello BGP 工作階段。 只接受公用 IP 位址首碼。 如果您計劃 toosend 一組前置詞，您可以傳送的逗號分隔清單。 這些前置詞必須是已註冊的 tooyou 在 RIR / IRR。
   * 客戶 ASN： 如果您通告不是數字的已註冊的 toohello 對等互連的前置詞，您可以指定 hello 為其所註冊的數字 toowhich。 **這是選擇性的**。
   * 路由登錄名稱： 您可以指定 hello RIR / IRR 哪些 hello 做為數字，但前置詞會註冊。
   * MD5 雜湊，如果您選擇其中一個 toouse。 **這是選擇性。**
     
    您可以執行下列 cmdlet tooconfigure Microsoft pering 為您的電路的 hello
     
        New-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -VlanId 300 -PeerAsn 1234 -CustomerAsn 2245 -AdvertisedPublicPrefixes "123.0.0.0/30" -RoutingRegistryName "ARIN" -SharedKey "A1B2C3D4"

### <a name="tooview-microsoft-peering-details"></a>tooview Microsoft 對等詳細資料
就可以使用下列 cmdlet 的 hello 設定詳細資料。

    Get-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************"

    AdvertisedPublicPrefixes       : 123.0.0.0/30
    AdvertisedPublicPrefixesState  : Configured
    AzureAsn                       : 12076
    CustomerAutonomousSystemNumber : 2245
    PeerAsn                        : 1234
    PrimaryAzurePort               : 
    PrimaryPeerSubnet              : 10.0.0.0/30
    RoutingRegistryName            : ARIN
    SecondaryAzurePort             : 
    SecondaryPeerSubnet            : 10.0.0.4/30
    State                          : Enabled
    VlanId                         : 300


### <a name="tooupdate-microsoft-peering-configuration"></a>tooupdate Microsoft 對等組態
您可以更新使用下列 cmdlet 的 hello hello 設定的任何部分。

    Set-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************" -PrimaryPeerSubnet "131.107.0.0/30" -SecondaryPeerSubnet "131.107.0.4/30" -VlanId 300 -PeerAsn 1234 -CustomerAsn 2245 -AdvertisedPublicPrefixes "123.0.0.0/30" -RoutingRegistryName "ARIN" -SharedKey "A1B2C3D4"

### <a name="toodelete-microsoft-peering"></a>toodelete Microsoft 對等互連
您可以藉由執行下列 cmdlet 的 hello 移除您對等的設定。

    Remove-AzureBGPPeering -AccessType Microsoft -ServiceKey "*********************************"

## <a name="next-steps"></a>後續步驟
下一步[連結 VNet tooan ExpressRoute 電路](expressroute-howto-linkvnet-classic.md)。

* 如需有關工作流程的詳細資訊，請參閱 [ExpressRoute 工作流程](expressroute-workflows.md)。
* 如需線路對等的詳細資訊，請參閱 [ExpressRoute 線路和路由網域](expressroute-circuit-peerings.md)。

