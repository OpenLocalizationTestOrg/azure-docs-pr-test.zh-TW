---
title: "從傳統 tooResource Manager 移轉相關聯的 ExpressRoute 的虛擬網路： Azure: PowerShell |Microsoft 文件"
description: "此頁面描述 toomigrate 移動您的循環後所關聯的虛擬網路 tooResource 管理員。"
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/06/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: e64506c6909296f98c5dd23b1437bc0b81f31c75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-expressroute-associated-virtual-networks-from-classic-tooresource-manager"></a>從傳統 tooResource Manager 移轉相關聯的 ExpressRoute 的虛擬網路

本文說明 toomigrate Azure ExpressRoute 移動 ExpressRoute 電路之後所關聯的虛擬網路與 hello 傳統部署模型 toohello Azure Resource Manager 部署模型。 


## <a name="before-you-begin"></a>開始之前
* 確認您擁有 hello hello Azure PowerShell 模組最新版本。 如需詳細資訊，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。
* 請確定您已經檢閱 hello[必要條件](expressroute-prerequisites.md)，[路由需求](expressroute-routing.md)，和[工作流程](expressroute-workflows.md)開始設定之前。
* 檢閱底下提供的 hello 資訊[從傳統 tooResource 管理員移動的 ExpressRoute 電路](expressroute-move.md)。 請確定您完全瞭解 hello 限制和限制。
* 請確認 hello 循環可完全運作 hello 傳統部署模型中。
* 確定您擁有 hello Resource Manager 部署模型中所建立的資源群組。
* 檢閱下列資源移轉文件的 hello:

    * [平台支援移轉從傳統 tooAzure 資源管理員的 IaaS 資源](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager.md)
    * [技術的深入剖析平台支援移轉從傳統 tooAzure 資源管理員](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager-deep-dive.md)
    * [常見問題集： 平台支援移轉 IaaS 資源從傳統 tooAzure 資源管理員](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager.md)
    * [檢閱最常見的移轉錯誤和避免方式](../virtual-machines/windows/migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="supported-and-unsupported-scenarios"></a>支援和不支援的案例

* 可以從 hello 傳統 toohello 資源管理員的環境沒有任何停機時間移動的 ExpressRoute 電路。 您可以將任何 ExpressRoute 電路移 hello 傳統 toohello 資源管理員環境沒有停機。 請依照下列中的 hello 指示[hello 傳統 toohello Resource Manager 部署模型使用 PowerShell 從移動 ExpressRoute 電路](expressroute-howto-move-arm.md)。 這是必要條件 toomove 資源連線的 toohello 虛擬網路。
* 虛擬網路、 閘道和相關聯的部署 hello 虛擬網路內附加的 tooan hello 可以是相同的訂用帳戶中的 ExpressRoute 電路移轉 toohello 資源管理員環境完全不需要停機。 您可以依照 hello 步驟所述更新 toomigrate 資源，例如虛擬網路、 閘道和 hello 虛擬網路內部署的虛擬機器。 您必須確定在移轉之前 hello 虛擬網路已正確設定。 
* 虛擬網路、 閘道和相關聯的部署中的 hello 虛擬網路內 hello 相同訂用帳戶，因為 hello ExpressRoute 電路需要一些停機時間 toocomplete hello 移轉。 hello hello 文件的最後一節描述 hello 步驟後面的 toobe toomigrate 資源。
* 無法移轉同時具有「ExpressRoute 閘道」和「VPN 閘道」的虛擬網路。

## <a name="move-an-expressroute-circuit-from-classic-tooresource-manager"></a>從傳統 tooResource 管理員移動的 ExpressRoute 電路
您必須移動 hello 傳統 toohello 資源管理員環境再 toomigrate 資源從 ExpressRoute 電路附加 toohello ExpressRoute 電路。 tooaccomplish 這項工作，請參閱下列文章 hello:

* 檢閱底下提供的 hello 資訊[從傳統 tooResource 管理員移動的 ExpressRoute 電路](expressroute-move.md)。
* [從傳統 tooResource 管理員使用 Azure PowerShell 移動電路](expressroute-howto-move-arm.md)。
* 使用 hello Azure 服務管理入口網站。 您可以依照 hello 工作流程太[建立新的 ExpressRoute 電路](expressroute-howto-circuit-portal-resource-manager.md)並選取 hello 匯入選項。 

這項作業不需要停機。 Hello 移轉正在進行時，您可以繼續 tootransfer 您內部部署和 Microsoft 之間的資料。

## <a name="migrate-virtual-networks-gateways-and-associated-deployments"></a>移轉虛擬網路、閘道與關聯的部署

hello 遵循 toomigrate 步驟取決於您的資源是否 hello 相同訂用帳戶、 不同的訂用帳戶，或兩者。

### <a name="migrate-virtual-networks-gateways-and-associated-deployments-in-hello-same-subscription-as-hello-expressroute-circuit"></a>移轉虛擬網路閘道，以及相關聯的部署中 hello 相同訂用帳戶，因為 hello ExpressRoute 電路
本章節描述 hello 步驟後面的 toobe toomigrate 虛擬網路、 閘道和相關聯的部署中 hello 相同訂用帳戶為 hello ExpressRoute 電路。 這項移轉不需要停機。 您可以繼續 toouse 透過 hello 移轉程序的所有資源。 hello 移轉正在進行時，會鎖定 hello 管理平面。 

1. 請從 hello 傳統 toohello 資源管理員環境的 hello ExpressRoute 循環到已移。
2. 請確定該 hello 虛擬網路已經準備適當 hello 移轉。
3. 註冊您的訂用帳戶以便移轉資源。 tooregister 資源移轉，使用下列 PowerShell 程式碼片段的 hello 的訂用帳戶：

  ```powershell 
  Select-AzureRmSubscription -SubscriptionName <Your Subscription Name>
  Register-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
  Get-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
  ```
4. 驗證、準備和移轉。 toomove hello 虛擬網路，使用下列 PowerShell 程式碼片段的 hello:

  ```powershell
  Move-AzureVirtualNetwork -Prepare $vnetName  
  Move-AzureVirtualNetwork -Commit $vnetName
  ```

  您也可以藉由執行下列 PowerShell cmdlet 的 hello 中止移轉：

  ```powershell
  Move-AzureVirtualNetwork -Abort $vnetName
  ```

## <a name="next-steps"></a>後續步驟
* [平台支援移轉從傳統 tooAzure 資源管理員的 IaaS 資源](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager.md)
* [技術的深入剖析平台支援移轉從傳統 tooAzure 資源管理員](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager-deep-dive.md)
* [常見問題集： 平台支援移轉 IaaS 資源從傳統 tooAzure 資源管理員](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager.md)
* [檢閱最常見的移轉錯誤和避免方式](../virtual-machines/windows/migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
