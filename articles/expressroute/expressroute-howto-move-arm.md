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
# <a name="move-expressroute-circuits-from-hello-classic-toohello-resource-manager-deployment-model-using-powershell"></a><span data-ttu-id="574d4-103">Hello 傳統 toohello Resource Manager 部署模型使用 PowerShell 從移動 ExpressRoute 電路</span><span class="sxs-lookup"><span data-stu-id="574d4-103">Move ExpressRoute circuits from hello classic toohello Resource Manager deployment model using PowerShell</span></span>

<span data-ttu-id="574d4-104">toouse ExpressRoute 電路傳統 hello 和資源管理員部署模型，您必須移動 hello 電路 toohello Resource Manager 部署模型。</span><span class="sxs-lookup"><span data-stu-id="574d4-104">toouse an ExpressRoute circuit for both hello classic and Resource Manager deployment models, you must move hello circuit toohello Resource Manager deployment model.</span></span> <span data-ttu-id="574d4-105">hello 下列各節協助您使用 PowerShell 來移動您的電路。</span><span class="sxs-lookup"><span data-stu-id="574d4-105">hello following sections help you move your circuit by using PowerShell.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="574d4-106">開始之前</span><span class="sxs-lookup"><span data-stu-id="574d4-106">Before you begin</span></span>

* <span data-ttu-id="574d4-107">確認您擁有 hello hello Azure PowerShell 模組最新版本 (至少 1.0 版)。</span><span class="sxs-lookup"><span data-stu-id="574d4-107">Verify that you have hello latest version of hello Azure PowerShell modules (at least version 1.0).</span></span> <span data-ttu-id="574d4-108">如需詳細資訊，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="574d4-108">For more information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="574d4-109">請確定您已經檢閱 hello[必要條件](expressroute-prerequisites.md)，[路由需求](expressroute-routing.md)，和[工作流程](expressroute-workflows.md)開始設定之前。</span><span class="sxs-lookup"><span data-stu-id="574d4-109">Make sure that you have reviewed hello [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="574d4-110">檢閱底下提供的 hello 資訊[從傳統 tooResource 管理員移動的 ExpressRoute 電路](expressroute-move.md)。</span><span class="sxs-lookup"><span data-stu-id="574d4-110">Review hello information that is provided under [Moving an ExpressRoute circuit from classic tooResource Manager](expressroute-move.md).</span></span> <span data-ttu-id="574d4-111">請確定您完全瞭解 hello 限制和限制。</span><span class="sxs-lookup"><span data-stu-id="574d4-111">Make sure that you fully understand hello limits and limitations.</span></span>
* <span data-ttu-id="574d4-112">請確認 hello 循環可完全運作 hello 傳統部署模型中。</span><span class="sxs-lookup"><span data-stu-id="574d4-112">Verify that hello circuit is fully operational in hello classic deployment model.</span></span>
* <span data-ttu-id="574d4-113">確定您擁有 hello Resource Manager 部署模型中所建立的資源群組。</span><span class="sxs-lookup"><span data-stu-id="574d4-113">Ensure that you have a resource group that was created in hello Resource Manager deployment model.</span></span>

## <a name="move-an-expressroute-circuit"></a><span data-ttu-id="574d4-114">移動 ExpressRoute 電路</span><span class="sxs-lookup"><span data-stu-id="574d4-114">Move an ExpressRoute circuit</span></span>

### <a name="step-1-gather-circuit-details-from-hello-classic-deployment-model"></a><span data-ttu-id="574d4-115">步驟 1: Hello 傳統部署模型從收集電路詳細資料</span><span class="sxs-lookup"><span data-stu-id="574d4-115">Step 1: Gather circuit details from hello classic deployment model</span></span>

<span data-ttu-id="574d4-116">登入 toohello Azure 傳統的環境，並收集 hello 服務金鑰。</span><span class="sxs-lookup"><span data-stu-id="574d4-116">Sign in toohello Azure classic environment and gather hello service key.</span></span>

1. <span data-ttu-id="574d4-117">Azure 帳戶登入 tooyour。</span><span class="sxs-lookup"><span data-stu-id="574d4-117">Sign in tooyour Azure account.</span></span>

  ```powershell
  Add-AzureAccount
  ```

2. <span data-ttu-id="574d4-118">選取 hello 適當的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="574d4-118">Select hello appropriate Azure subscription.</span></span>

  ```powershell
  Select-AzureSubscription "<Enter Subscription Name here>"
  ```

3. <span data-ttu-id="574d4-119">Azure 和 ExpressRoute 匯入 hello PowerShell 模組。</span><span class="sxs-lookup"><span data-stu-id="574d4-119">Import hello PowerShell modules for Azure and ExpressRoute.</span></span>

  ```powershell
  Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
  Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
  ```

4. <span data-ttu-id="574d4-120">ExpressRoute 電路的所有使用 tooget hello 服務機碼下的 hello cmdlet。</span><span class="sxs-lookup"><span data-stu-id="574d4-120">Use hello cmdlet below tooget hello service keys for all of your ExpressRoute circuits.</span></span> <span data-ttu-id="574d4-121">擷取後 hello 索引鍵，複製 hello**服務金鑰**hello 循環的 toomove toohello Resource Manager 部署模型。</span><span class="sxs-lookup"><span data-stu-id="574d4-121">After retrieving hello keys, copy hello **service key** of hello circuit that you want toomove toohello Resource Manager deployment model.</span></span>

  ```powershell
  Get-AzureDedicatedCircuit
  ```

### <a name="step-2-sign-in-and-create-a-resource-group"></a><span data-ttu-id="574d4-122">步驟 2：登入並建立資源群組</span><span class="sxs-lookup"><span data-stu-id="574d4-122">Step 2: Sign in and create a resource group</span></span>

<span data-ttu-id="574d4-123">登入 toohello 資源管理員環境，並建立新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="574d4-123">Sign in toohello Resource Manager environment and create a new resource group.</span></span>

1. <span data-ttu-id="574d4-124">登入 tooyour Azure 資源管理員環境。</span><span class="sxs-lookup"><span data-stu-id="574d4-124">Sign in tooyour Azure Resource Manager environment.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

2. <span data-ttu-id="574d4-125">選取 hello 適當的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="574d4-125">Select hello appropriate Azure subscription.</span></span>

  ```powershell
  Get-AzureRmSubscription -SubscriptionName "<Enter Subscription Name here>" | Select-AzureRmSubscription
  ```

3. <span data-ttu-id="574d4-126">如果您還沒有資源群組，請修改 hello toocreate 新的資源群組下的程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="574d4-126">Modify hello snippet below toocreate a new resource group if you don't already have a resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name "DemoRG" -Location "West US"
  ```

### <a name="step-3-move-hello-expressroute-circuit-toohello-resource-manager-deployment-model"></a><span data-ttu-id="574d4-127">步驟 3： 移動 hello ExpressRoute 電路 toohello Resource Manager 部署模型</span><span class="sxs-lookup"><span data-stu-id="574d4-127">Step 3: Move hello ExpressRoute circuit toohello Resource Manager deployment model</span></span>

<span data-ttu-id="574d4-128">您會立即準備 toomove 您從 hello 傳統部署模型 toohello Resource Manager 部署模型的 ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="574d4-128">You are now ready toomove your ExpressRoute circuit from hello classic deployment model toohello Resource Manager deployment model.</span></span> <span data-ttu-id="574d4-129">繼續之前，檢閱中所提供的 hello 資訊[移動從 hello 傳統 toohello Resource Manager 部署模型的 ExpressRoute 電路](expressroute-move.md)。</span><span class="sxs-lookup"><span data-stu-id="574d4-129">Before proceeding, review hello information provided in [Moving an ExpressRoute circuit from hello classic toohello Resource Manager deployment model](expressroute-move.md).</span></span>

<span data-ttu-id="574d4-130">toomove 修改您的循環，並執行下列程式碼片段的 hello:</span><span class="sxs-lookup"><span data-stu-id="574d4-130">toomove your circuit, modify and run hello following snippet:</span></span>

```powershell
Move-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "DemoRG" -Location "West US" -ServiceKey "<Service-key>"
```

> [!NOTE]
> <span data-ttu-id="574d4-131">Hello 移動完成之後，會列在 hello 前一個 cmdlet 的 hello 新名稱將會使用的 tooaddress hello 資源。</span><span class="sxs-lookup"><span data-stu-id="574d4-131">After hello move has finished, hello new name that is listed in hello previous cmdlet will be used tooaddress hello resource.</span></span> <span data-ttu-id="574d4-132">hello 循環本質上會被重新命名。</span><span class="sxs-lookup"><span data-stu-id="574d4-132">hello circuit will essentially be renamed.</span></span>
> 

## <a name="modify-circuit-access"></a><span data-ttu-id="574d4-133">修改電路存取</span><span class="sxs-lookup"><span data-stu-id="574d4-133">Modify circuit access</span></span>

### <a name="tooenable-expressroute-circuit-access-for-both-deployment-models"></a><span data-ttu-id="574d4-134">tooenable ExpressRoute 電路存取兩種部署模型</span><span class="sxs-lookup"><span data-stu-id="574d4-134">tooenable ExpressRoute circuit access for both deployment models</span></span>

<span data-ttu-id="574d4-135">移動後傳統 ExpressRoute 電路 toohello 資源管理員部署模型，您可以啟用存取 tooboth 部署模型。</span><span class="sxs-lookup"><span data-stu-id="574d4-135">After moving your classic ExpressRoute circuit toohello Resource Manager deployment model, you can enable access tooboth deployment models.</span></span> <span data-ttu-id="574d4-136">執行下列 cmdlet tooenable 存取 tooboth 部署模型的 hello:</span><span class="sxs-lookup"><span data-stu-id="574d4-136">Run hello following cmdlets tooenable access tooboth deployment models:</span></span>

1. <span data-ttu-id="574d4-137">取得 hello 電路詳細資料。</span><span class="sxs-lookup"><span data-stu-id="574d4-137">Get hello circuit details.</span></span>

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "DemoCkt" -ResourceGroupName "DemoRG"
  ```

2. <span data-ttu-id="574d4-138">設定 「 允許傳統作業 > tooTRUE。</span><span class="sxs-lookup"><span data-stu-id="574d4-138">Set "Allow Classic Operations" tooTRUE.</span></span>

  ```powershell
  $ckt.AllowClassicOperations = $true
  ```

3. <span data-ttu-id="574d4-139">更新 hello 循環。</span><span class="sxs-lookup"><span data-stu-id="574d4-139">Update hello circuit.</span></span> <span data-ttu-id="574d4-140">這項作業已順利完成之後，您將無法 tooview hello 傳統部署模型中的 hello 循環。</span><span class="sxs-lookup"><span data-stu-id="574d4-140">After this operation has finished successfully, you will be able tooview hello circuit in hello classic deployment model.</span></span>

  ```powershell
  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

4. <span data-ttu-id="574d4-141">執行下列 cmdlet tooget hello 詳細資料的 hello ExpressRoute 電路的 hello。</span><span class="sxs-lookup"><span data-stu-id="574d4-141">Run hello following cmdlet tooget hello details of hello ExpressRoute circuit.</span></span> <span data-ttu-id="574d4-142">您必須是所列的可以 toosee hello 服務機碼。</span><span class="sxs-lookup"><span data-stu-id="574d4-142">You must be able toosee hello service key listed.</span></span>

  ```powershell
  get-azurededicatedcircuit
  ```

5. <span data-ttu-id="574d4-143">您現在可以管理連結 toohello ExpressRoute 循環使用資源管理員 Vnet 傳統的 Vnet 和 hello 資源管理員命令的 hello 傳統部署模型命令。</span><span class="sxs-lookup"><span data-stu-id="574d4-143">You can now manage links toohello ExpressRoute circuit using hello classic deployment model commands for classic VNets, and hello Resource Manager commands for Resource Manager VNets.</span></span> <span data-ttu-id="574d4-144">hello 下列文章協助您管理連結 toohello ExpressRoute 循環：</span><span class="sxs-lookup"><span data-stu-id="574d4-144">hello following articles help you manage links toohello ExpressRoute circuit:</span></span>

    * [<span data-ttu-id="574d4-145">連結您的虛擬網路 tooyour hello Resource Manager 部署模型中的 ExpressRoute 電路</span><span class="sxs-lookup"><span data-stu-id="574d4-145">Link your virtual network tooyour ExpressRoute circuit in hello Resource Manager deployment model</span></span>](expressroute-howto-linkvnet-arm.md)
    * [<span data-ttu-id="574d4-146">連結您的虛擬網路 tooyour hello 傳統部署模型中的 ExpressRoute 電路</span><span class="sxs-lookup"><span data-stu-id="574d4-146">Link your virtual network tooyour ExpressRoute circuit in hello classic deployment model</span></span>](expressroute-howto-linkvnet-classic.md)

### <a name="toodisable-expressroute-circuit-access-toohello-classic-deployment-model"></a><span data-ttu-id="574d4-147">toodisable ExpressRoute 電路存取 toohello 傳統部署模型</span><span class="sxs-lookup"><span data-stu-id="574d4-147">toodisable ExpressRoute circuit access toohello classic deployment model</span></span>

<span data-ttu-id="574d4-148">執行下列 cmdlet toodisable 存取 toohello 傳統部署模型的 hello。</span><span class="sxs-lookup"><span data-stu-id="574d4-148">Run hello following cmdlets toodisable access toohello classic deployment model.</span></span>

1. <span data-ttu-id="574d4-149">取得 hello ExpressRoute 電路的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="574d4-149">Get details of hello ExpressRoute circuit.</span></span>

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "DemoCkt" -ResourceGroupName "DemoRG"
  ```

2. <span data-ttu-id="574d4-150">設定 「 允許傳統作業 > tooFALSE。</span><span class="sxs-lookup"><span data-stu-id="574d4-150">Set "Allow Classic Operations" tooFALSE.</span></span>

  ```powershell
  $ckt.AllowClassicOperations = $false
  ```

3. <span data-ttu-id="574d4-151">更新 hello 循環。</span><span class="sxs-lookup"><span data-stu-id="574d4-151">Update hello circuit.</span></span> <span data-ttu-id="574d4-152">這項作業已順利完成之後，您將無法在 hello 傳統部署模型中的可以 tooview hello 循環。</span><span class="sxs-lookup"><span data-stu-id="574d4-152">After this operation has finished successfully, you will not be able tooview hello circuit in hello classic deployment model.</span></span>

  ```powershell
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

## <a name="next-steps"></a><span data-ttu-id="574d4-153">後續步驟</span><span class="sxs-lookup"><span data-stu-id="574d4-153">Next steps</span></span>

* [<span data-ttu-id="574d4-154">建立和修改 ExpressRoute 線路的路由</span><span class="sxs-lookup"><span data-stu-id="574d4-154">Create and modify routing for your ExpressRoute circuit</span></span>](expressroute-howto-routing-arm.md)
* [<span data-ttu-id="574d4-155">連結您的虛擬網路 tooyour ExpressRoute 電路</span><span class="sxs-lookup"><span data-stu-id="574d4-155">Link your virtual network tooyour ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-arm.md)
