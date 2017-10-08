---
title: "從傳統 tooResource 管理員移動的 ExpressRoute 電路： PowerShell: Azure |Microsoft 文件"
description: "此頁面描述 toomove 傳統線路 toohello 資源管理員部署模型使用 PowerShell。"
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 08152836-23e7-42d1-9a56-8306b341cd91
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/03/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 8dcadafca5e4f40773902cec5786eba1dbe133eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="move-expressroute-circuits-from-hello-classic-toohello-resource-manager-deployment-model-using-powershell"></a>Hello 傳統 toohello Resource Manager 部署模型使用 PowerShell 從移動 ExpressRoute 電路

toouse ExpressRoute 電路傳統 hello 和資源管理員部署模型，您必須移動 hello 電路 toohello Resource Manager 部署模型。 hello 下列各節協助您使用 PowerShell 來移動您的電路。

## <a name="before-you-begin"></a>開始之前

* 確認您擁有 hello hello Azure PowerShell 模組最新版本 (至少 1.0 版)。 如需詳細資訊，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。
* 請確定您已經檢閱 hello[必要條件](expressroute-prerequisites.md)，[路由需求](expressroute-routing.md)，和[工作流程](expressroute-workflows.md)開始設定之前。
* 檢閱底下提供的 hello 資訊[從傳統 tooResource 管理員移動的 ExpressRoute 電路](expressroute-move.md)。 請確定您完全瞭解 hello 限制和限制。
* 請確認 hello 循環可完全運作 hello 傳統部署模型中。
* 確定您擁有 hello Resource Manager 部署模型中所建立的資源群組。

## <a name="move-an-expressroute-circuit"></a>移動 ExpressRoute 電路

### <a name="step-1-gather-circuit-details-from-hello-classic-deployment-model"></a>步驟 1: Hello 傳統部署模型從收集電路詳細資料

登入 toohello Azure 傳統的環境，並收集 hello 服務金鑰。

1. Azure 帳戶登入 tooyour。

  ```powershell
  Add-AzureAccount
  ```

2. 選取 hello 適當的 Azure 訂用帳戶。

  ```powershell
  Select-AzureSubscription "<Enter Subscription Name here>"
  ```

3. Azure 和 ExpressRoute 匯入 hello PowerShell 模組。

  ```powershell
  Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
  Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
  ```

4. ExpressRoute 電路的所有使用 tooget hello 服務機碼下的 hello cmdlet。 擷取後 hello 索引鍵，複製 hello**服務金鑰**hello 循環的 toomove toohello Resource Manager 部署模型。

  ```powershell
  Get-AzureDedicatedCircuit
  ```

### <a name="step-2-sign-in-and-create-a-resource-group"></a>步驟 2：登入並建立資源群組

登入 toohello 資源管理員環境，並建立新的資源群組。

1. 登入 tooyour Azure 資源管理員環境。

  ```powershell
  Login-AzureRmAccount
  ```

2. 選取 hello 適當的 Azure 訂用帳戶。

  ```powershell
  Get-AzureRmSubscription -SubscriptionName "<Enter Subscription Name here>" | Select-AzureRmSubscription
  ```

3. 如果您還沒有資源群組，請修改 hello toocreate 新的資源群組下的程式碼片段。

  ```powershell
  New-AzureRmResourceGroup -Name "DemoRG" -Location "West US"
  ```

### <a name="step-3-move-hello-expressroute-circuit-toohello-resource-manager-deployment-model"></a>步驟 3： 移動 hello ExpressRoute 電路 toohello Resource Manager 部署模型

您會立即準備 toomove 您從 hello 傳統部署模型 toohello Resource Manager 部署模型的 ExpressRoute 電路。 繼續之前，檢閱中所提供的 hello 資訊[移動從 hello 傳統 toohello Resource Manager 部署模型的 ExpressRoute 電路](expressroute-move.md)。

toomove 修改您的循環，並執行下列程式碼片段的 hello:

```powershell
Move-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "DemoRG" -Location "West US" -ServiceKey "<Service-key>"
```

> [!NOTE]
> Hello 移動完成之後，會列在 hello 前一個 cmdlet 的 hello 新名稱將會使用的 tooaddress hello 資源。 hello 循環本質上會被重新命名。
> 

## <a name="modify-circuit-access"></a>修改電路存取

### <a name="tooenable-expressroute-circuit-access-for-both-deployment-models"></a>tooenable ExpressRoute 電路存取兩種部署模型

移動後傳統 ExpressRoute 電路 toohello 資源管理員部署模型，您可以啟用存取 tooboth 部署模型。 執行下列 cmdlet tooenable 存取 tooboth 部署模型的 hello:

1. 取得 hello 電路詳細資料。

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "DemoCkt" -ResourceGroupName "DemoRG"
  ```

2. 設定 「 允許傳統作業 > tooTRUE。

  ```powershell
  $ckt.AllowClassicOperations = $true
  ```

3. 更新 hello 循環。 這項作業已順利完成之後，您將無法 tooview hello 傳統部署模型中的 hello 循環。

  ```powershell
  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

4. 執行下列 cmdlet tooget hello 詳細資料的 hello ExpressRoute 電路的 hello。 您必須是所列的可以 toosee hello 服務機碼。

  ```powershell
  get-azurededicatedcircuit
  ```

5. 您現在可以管理連結 toohello ExpressRoute 循環使用資源管理員 Vnet 傳統的 Vnet 和 hello 資源管理員命令的 hello 傳統部署模型命令。 hello 下列文章協助您管理連結 toohello ExpressRoute 循環：

    * [連結您的虛擬網路 tooyour hello Resource Manager 部署模型中的 ExpressRoute 電路](expressroute-howto-linkvnet-arm.md)
    * [連結您的虛擬網路 tooyour hello 傳統部署模型中的 ExpressRoute 電路](expressroute-howto-linkvnet-classic.md)

### <a name="toodisable-expressroute-circuit-access-toohello-classic-deployment-model"></a>toodisable ExpressRoute 電路存取 toohello 傳統部署模型

執行下列 cmdlet toodisable 存取 toohello 傳統部署模型的 hello。

1. 取得 hello ExpressRoute 電路的詳細資料。

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "DemoCkt" -ResourceGroupName "DemoRG"
  ```

2. 設定 「 允許傳統作業 > tooFALSE。

  ```powershell
  $ckt.AllowClassicOperations = $false
  ```

3. 更新 hello 循環。 這項作業已順利完成之後，您將無法在 hello 傳統部署模型中的可以 tooview hello 循環。

  ```powershell
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

## <a name="next-steps"></a>後續步驟

* [建立和修改 ExpressRoute 線路的路由](expressroute-howto-routing-arm.md)
* [連結您的虛擬網路 tooyour ExpressRoute 電路](expressroute-howto-linkvnet-arm.md)
