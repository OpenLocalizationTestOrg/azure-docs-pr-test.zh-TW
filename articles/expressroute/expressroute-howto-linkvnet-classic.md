---
title: "虛擬網路 tooan ExpressRoute 電路的連結： PowerShell： 傳統： Azure |Microsoft 文件"
description: "本文件概述 toolink 虛擬網路 (Vnet) tooExpressRoute 電路使用 hello 傳統部署模型和 PowerShell 的方式。"
services: expressroute
documentationcenter: na
author: ganesr
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: 9b53fd72-9b6b-4844-80b9-4e1d54fd0c17
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/28/2017
ms.author: ganesr
ms.openlocfilehash: 6b8a01dcd4bbb9618ec3dd438cf0107538fb2a7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-virtual-network-tooan-expressroute-circuit-using-powershell-classic"></a>連接虛擬網路 tooan ExpressRoute 電路使用 PowerShell （傳統）
> [!div class="op_single_selector"]
> * [Azure 入口網站](expressroute-howto-linkvnet-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-linkvnet-arm.md)
> * [Azure CLI](howto-linkvnet-cli.md)
> * [影片 - Azure 入口網站](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-connection-between-your-vpn-gateway-and-expressroute-circuit)
> * [PowerShell (傳統)](expressroute-howto-linkvnet-classic.md)
>

本文將協助您使用 hello 傳統部署模型和 PowerShell 連結虛擬網路 (Vnet) tooAzure ExpressRoute 電路。 虛擬網路可以是在 hello 相同訂用帳戶，或可以是另一個訂用帳戶的一部分。

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

**關於 Azure 部署模型**

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="configuration-prerequisites"></a>組態必要條件
1. 您需要 hello hello Azure PowerShell 模組最新版本。 您可以從 hello hello PowerShell 區段下載最新 PowerShell 模組 hello [Azure 下載頁面](https://azure.microsoft.com/downloads/)。 請依照下列中的 hello 指示[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)的逐步指示如何 tooconfigure 電腦 toouse hello Azure PowerShell 模組。
2. 您需要 tooreview hello[必要條件](expressroute-prerequisites.md)，[路由需求](expressroute-routing.md)，和[工作流程](expressroute-workflows.md)開始設定之前。
3. 您必須擁有作用中的 ExpressRoute 線路。
   * 請依照下列指示 hello 太[建立 ExpressRoute 電路](expressroute-howto-circuit-classic.md)且有連線提供者啟用 hello 循環。
   * 確定您已針對循環設定了 Azure 私用對等。 請參閱 hello[設定路由](expressroute-howto-routing-classic.md)路由指示的發行項。
   * 請確認 Azure 私用對等設定，且 hello BGP 對等互連網路與 Microsoft 之間，以便您可以啟用端對端連線已啟動。
   * 您必須有已建立且完整佈建的虛擬網路和虛擬網路閘道。 請依照下列指示 hello 太[設定 expressroute 的虛擬網路](expressroute-howto-vnet-portal-classic.md)。

您可以連結 too10 虛擬網路 tooan ExpressRoute 電路。 所有虛擬網路必須位於 hello 相同地理政治區域。 您可以更大量的虛擬網路 tooyour ExpressRoute 電路的連結，或位於其他地緣政治區域，如果您啟用 hello ExpressRoute premium add-on 的虛擬網路連結。 檢查 hello[常見問題集](expressroute-faqs.md)如需有關 hello premium 附加元件。

## <a name="connect-a-virtual-network-in-hello-same-subscription-tooa-circuit"></a>連接 hello 中的虛擬網路相同的訂用帳戶 tooa 電路
您可以使用下列 cmdlet 的 hello 連結虛擬網路 tooan ExpressRoute 電路。 請確定該 hello 虛擬網路閘道建立並且準備好進行連結，然後再執行 hello cmdlet。

    New-AzureDedicatedCircuitLink -ServiceKey "*****************************" -VNetName "MyVNet"
    Provisioned

## <a name="connect-a-virtual-network-in-a-different-subscription-tooa-circuit"></a>在不同的訂用帳戶 tooa 電路的虛擬網路連線
您可以讓多個訂用帳戶共用 ExpressRoute 線路。 hello 遵循圖顯示的簡單圖解如何共用 ExpressRoute 電路的運作方式跨多個訂用帳戶。

Hello hello 大型雲端內的小型雲端都屬於 toodifferent 部門組織內使用的 toorepresent 訂用帳戶。 針對部署其服務： 但 hello 部門可以共用單一 ExpressRoute 電路 tooconnect 後 tooyour 在內部部署網路，hello 部門 hello 組織內的每個可以使用自己的訂用帳戶。 單一部門 (在此範例中： IT) 可以擁有 hello ExpressRoute 電路。 Hello 組織內其他訂用帳戶可以使用 hello ExpressRoute 電路。

> [!NOTE]
> Hello 專用循環的連線和頻寬費用將會套用的 toohello ExpressRoute 電路擁有者。 所有虛擬網路共用 hello 相同的頻寬。
> 
> 

![跨訂用帳戶的連線能力](./media/expressroute-howto-linkvnet-classic/cross-subscription.png)

### <a name="administration"></a>系統管理
hello*電路擁有者*是 hello 管理員/coadministrator hello 訂用帳戶中的 hello ExpressRoute 電路建立。 hello 電路擁有者可以授權其他訂用帳戶，參照 tooas 的系統管理員/coadministrators*電路使用者*，toouse hello 專用他們所擁有的電路。 循環的使用者授權的 toouse hello 組織的 ExpressRoute 電路可以連結 hello 中其訂用帳戶 toohello ExpressRoute 電路的虛擬網路之後他們獲授權。

hello 電路擁有者隨時都有 hello 電源 toomodify 和撤銷授權。 撤銷授權會導致從已撤銷其存取權的 hello 訂用帳戶中刪除所有連結。

### <a name="circuit-owner-operations"></a>循環擁有者作業

**建立授權**

hello 電路擁有者授與其他訂閱的 hello 管理員 toouse hello 指定循環。 在下列範例的 hello，hello hello 電路 (Contoso IT) 系統管理員可讓向上 tootwo 虛擬網路 toohello 循環的另一個訂用帳戶 （開發測試） toolink hello 系統管理員。 hello Contoso IT 系統管理員可讓這指定 hello 開發測試 Microsoft id。 hello cmdlet 不會傳送電子郵件 toohello 指定的 Microsoft id。 hello 電路擁有者必須 tooexplicitly 通知 hello hello 授權其他訂用帳戶擁有者已完成。

    New-AzureDedicatedCircuitLinkAuthorization -ServiceKey "**************************" -Description "Dev-Test Links" -Limit 2 -MicrosoftIds 'devtest@contoso.com'

    Description         : Dev-Test Links
    Limit               : 2
    LinkAuthorizationId : **********************************
    MicrosoftIds        : devtest@contoso.com
    Used                : 0

**檢閱授權**

hello 電路擁有者可以檢閱由執行下列 cmdlet 的 hello 特定電路發出的所有授權：

    Get-AzureDedicatedCircuitLinkAuthorization -ServiceKey: "**************************"

    Description         : EngineeringTeam
    Limit               : 3
    LinkAuthorizationId : ####################################
    MicrosoftIds        : engadmin@contoso.com
    Used                : 1

    Description         : MarketingTeam
    Limit               : 1
    LinkAuthorizationId : @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
    MicrosoftIds        : marketingadmin@contoso.com
    Used                : 0

    Description         : Dev-Test Links
    Limit               : 2
    LinkAuthorizationId : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
    MicrosoftIds        : salesadmin@contoso.com
    Used                : 2


**更新授權**

hello 電路擁有者可以使用下列 cmdlet 的 hello 修改授權：

    Set-AzureDedicatedCircuitLinkAuthorization -ServiceKey "**************************" -AuthorizationId "&&&&&&&&&&&&&&&&&&&&&&&&&&&&"-Limit 5

    Description         : Dev-Test Links
    Limit               : 5
    LinkAuthorizationId : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
    MicrosoftIds        : devtest@contoso.com
    Used                : 0


**刪除授權**

hello 電路擁有者可以撤銷/刪除授權 toohello 使用者藉由執行下列 cmdlet 的 hello:

    Remove-AzureDedicatedCircuitLinkAuthorization -ServiceKey "*****************************" -AuthorizationId "###############################"


### <a name="circuit-user-operations"></a>循環使用者作業

**檢閱授權**

hello 循環使用者可以使用下列 cmdlet 的 hello 來檢閱授權：

    Get-AzureAuthorizedDedicatedCircuit

    Bandwidth                        : 200
    CircuitName                      : ContosoIT
    Location                         : Washington DC
    MaximumAllowedLinks              : 2
    ServiceKey                       : &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
    ServiceProviderName              : equinix
    ServiceProviderProvisioningState : Provisioned
    Status                           : Enabled
    UsedLinks                        : 0

**兌換連結授權**

hello 循環使用者可以執行下列 cmdlet tooredeem hello 連結授權：

    New-AzureDedicatedCircuitLink –servicekey "&&&&&&&&&&&&&&&&&&&&&&&&&&" –VnetName 'SalesVNET1'

    State VnetName
    ----- --------
    Provisioned SalesVNET1

Hello 虛擬網路的新連結的 hello 訂用帳戶中執行下列命令：

    New-AzureDedicatedCircuitLink -ServiceKey "*****************************" -VNetName "MyVNet"

## <a name="next-steps"></a>後續步驟
如需 ExpressRoute 的詳細資訊，請參閱 hello [ExpressRoute 常見問題集](expressroute-faqs.md)。

