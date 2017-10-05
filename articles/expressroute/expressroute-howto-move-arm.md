---
title: "將 ExpressRoute 電路從傳統移至 Resource Manager：PowerShell：Azure | Microsoft Docs"
description: "本頁面會描述如何使用 PowerShell 將傳統的電路移至 Resource Manager 部署模型。"
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
ms.openlocfilehash: c407e01e6d881cb8adcfe55faa246468669be883
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="move-expressroute-circuits-from-the-classic-to-the-resource-manager-deployment-model-using-powershell"></a><span data-ttu-id="3fba1-103">使用 PowerShell 將 ExpressRoute 電路從傳統部署模型移至 Resource Manager 部署模型</span><span class="sxs-lookup"><span data-stu-id="3fba1-103">Move ExpressRoute circuits from the classic to the Resource Manager deployment model using PowerShell</span></span>

<span data-ttu-id="3fba1-104">若要在傳統和 Resource Manager 兩種部署模型中使用 ExpressRoute，您必須將電路移至 Resource Manager 部署模型。</span><span class="sxs-lookup"><span data-stu-id="3fba1-104">To use an ExpressRoute circuit for both the classic and Resource Manager deployment models, you must move the circuit to the Resource Manager deployment model.</span></span> <span data-ttu-id="3fba1-105">下列章節協助您使用 PowerShell 來移動線路。</span><span class="sxs-lookup"><span data-stu-id="3fba1-105">The following sections help you move your circuit by using PowerShell.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="3fba1-106">開始之前</span><span class="sxs-lookup"><span data-stu-id="3fba1-106">Before you begin</span></span>

* <span data-ttu-id="3fba1-107">請確認您有最新版的 Azure PowerShell 模組 (至少 1.0 版)。</span><span class="sxs-lookup"><span data-stu-id="3fba1-107">Verify that you have the latest version of the Azure PowerShell modules (at least version 1.0).</span></span> <span data-ttu-id="3fba1-108">如需詳細資訊，請參閱 [如何安裝和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="3fba1-108">For more information, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="3fba1-109">開始設定之前，請確定您已經檢閱過[必要條件](expressroute-prerequisites.md)、[路由需求](expressroute-routing.md)和[工作流程](expressroute-workflows.md)。</span><span class="sxs-lookup"><span data-stu-id="3fba1-109">Make sure that you have reviewed the [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="3fba1-110">請檢閱[將 ExpressRoute 電路從傳統移至 Resource Manager](expressroute-move.md) 下提供的資訊。</span><span class="sxs-lookup"><span data-stu-id="3fba1-110">Review the information that is provided under [Moving an ExpressRoute circuit from classic to Resource Manager](expressroute-move.md).</span></span> <span data-ttu-id="3fba1-111">請確定您已完整了解各項限制。</span><span class="sxs-lookup"><span data-stu-id="3fba1-111">Make sure that you fully understand the limits and limitations.</span></span>
* <span data-ttu-id="3fba1-112">請確認電路在傳統部署模型中的運作完全正常。</span><span class="sxs-lookup"><span data-stu-id="3fba1-112">Verify that the circuit is fully operational in the classic deployment model.</span></span>
* <span data-ttu-id="3fba1-113">請確定您擁有建立在 Resource Manager 部署模型中建立的資源群組。</span><span class="sxs-lookup"><span data-stu-id="3fba1-113">Ensure that you have a resource group that was created in the Resource Manager deployment model.</span></span>

## <a name="move-an-expressroute-circuit"></a><span data-ttu-id="3fba1-114">移動 ExpressRoute 電路</span><span class="sxs-lookup"><span data-stu-id="3fba1-114">Move an ExpressRoute circuit</span></span>

### <a name="step-1-gather-circuit-details-from-the-classic-deployment-model"></a><span data-ttu-id="3fba1-115">步驟 1︰從傳統部署模型收集電路詳細資訊</span><span class="sxs-lookup"><span data-stu-id="3fba1-115">Step 1: Gather circuit details from the classic deployment model</span></span>

<span data-ttu-id="3fba1-116">登入 Azure 傳統環境並收集服務金鑰。</span><span class="sxs-lookup"><span data-stu-id="3fba1-116">Sign in to the Azure classic environment and gather the service key.</span></span>

1. <span data-ttu-id="3fba1-117">登入您的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="3fba1-117">Sign in to your Azure account.</span></span>

  ```powershell
  Add-AzureAccount
  ```

2. <span data-ttu-id="3fba1-118">選取適當的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="3fba1-118">Select the appropriate Azure subscription.</span></span>

  ```powershell
  Select-AzureSubscription "<Enter Subscription Name here>"
  ```

3. <span data-ttu-id="3fba1-119">匯入 Azure 和 ExpressRoute 的 PowerShell 模組。</span><span class="sxs-lookup"><span data-stu-id="3fba1-119">Import the PowerShell modules for Azure and ExpressRoute.</span></span>

  ```powershell
  Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
  Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
  ```

4. <span data-ttu-id="3fba1-120">使用下列 Cmdlet 來取得所有 ExpressRoute 電路的服務金鑰。</span><span class="sxs-lookup"><span data-stu-id="3fba1-120">Use the cmdlet below to get the service keys for all of your ExpressRoute circuits.</span></span> <span data-ttu-id="3fba1-121">在取得金鑰之後，請複製電路的「服務金鑰」，這個電路就是您想要移至 Resource Manager 部署模型的電路。</span><span class="sxs-lookup"><span data-stu-id="3fba1-121">After retrieving the keys, copy the **service key** of the circuit that you want to move to the Resource Manager deployment model.</span></span>

  ```powershell
  Get-AzureDedicatedCircuit
  ```

### <a name="step-2-sign-in-and-create-a-resource-group"></a><span data-ttu-id="3fba1-122">步驟 2：登入並建立資源群組</span><span class="sxs-lookup"><span data-stu-id="3fba1-122">Step 2: Sign in and create a resource group</span></span>

<span data-ttu-id="3fba1-123">登入 Resource Manager 環境並建立新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="3fba1-123">Sign in to the Resource Manager environment and create a new resource group.</span></span>

1. <span data-ttu-id="3fba1-124">登入您的 Azure Resource Manager 環境。</span><span class="sxs-lookup"><span data-stu-id="3fba1-124">Sign in to your Azure Resource Manager environment.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

2. <span data-ttu-id="3fba1-125">選取適當的 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="3fba1-125">Select the appropriate Azure subscription.</span></span>

  ```powershell
  Get-AzureRmSubscription -SubscriptionName "<Enter Subscription Name here>" | Select-AzureRmSubscription
  ```

3. <span data-ttu-id="3fba1-126">修改下列程式碼片段以建立新的資源群組 (如果您尚未擁有資源群組)。</span><span class="sxs-lookup"><span data-stu-id="3fba1-126">Modify the snippet below to create a new resource group if you don't already have a resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name "DemoRG" -Location "West US"
  ```

### <a name="step-3-move-the-expressroute-circuit-to-the-resource-manager-deployment-model"></a><span data-ttu-id="3fba1-127">步驟 3：將 ExpressRoute 電路移至 Resource Manager 部署模型</span><span class="sxs-lookup"><span data-stu-id="3fba1-127">Step 3: Move the ExpressRoute circuit to the Resource Manager deployment model</span></span>

<span data-ttu-id="3fba1-128">您已準備就緒，可將 ExpressRoute 電路從傳統部署模型移至 Resource Manager 部署模型。</span><span class="sxs-lookup"><span data-stu-id="3fba1-128">You are now ready to move your ExpressRoute circuit from the classic deployment model to the Resource Manager deployment model.</span></span> <span data-ttu-id="3fba1-129">更進一步之前，請先檢閱[將 ExpressRoute 電路從傳統移至 Resource Manager 部署模型](expressroute-move.md)下提供的資訊。</span><span class="sxs-lookup"><span data-stu-id="3fba1-129">Before proceeding, review the information provided in [Moving an ExpressRoute circuit from the classic to the Resource Manager deployment model](expressroute-move.md).</span></span>

<span data-ttu-id="3fba1-130">若要移動電路，請修改並執行下列程式碼片段：</span><span class="sxs-lookup"><span data-stu-id="3fba1-130">To move your circuit, modify and run the following snippet:</span></span>

```powershell
Move-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "DemoRG" -Location "West US" -ServiceKey "<Service-key>"
```

> [!NOTE]
> <span data-ttu-id="3fba1-131">移動完成之後，列在前一個 Cmdlet 中的新名稱會用來處理資源。</span><span class="sxs-lookup"><span data-stu-id="3fba1-131">After the move has finished, the new name that is listed in the previous cmdlet will be used to address the resource.</span></span> <span data-ttu-id="3fba1-132">電路基本上會重新命名。</span><span class="sxs-lookup"><span data-stu-id="3fba1-132">The circuit will essentially be renamed.</span></span>
> 

## <a name="modify-circuit-access"></a><span data-ttu-id="3fba1-133">修改電路存取</span><span class="sxs-lookup"><span data-stu-id="3fba1-133">Modify circuit access</span></span>

### <a name="to-enable-expressroute-circuit-access-for-both-deployment-models"></a><span data-ttu-id="3fba1-134">為兩種部署模型啟用 ExpressRoute 電路存取</span><span class="sxs-lookup"><span data-stu-id="3fba1-134">To enable ExpressRoute circuit access for both deployment models</span></span>

<span data-ttu-id="3fba1-135">在將傳統 ExpressRoute 電路移至 Resource Manager 部署模型之後，您可以為這兩種部署模型啟用存取。</span><span class="sxs-lookup"><span data-stu-id="3fba1-135">After moving your classic ExpressRoute circuit to the Resource Manager deployment model, you can enable access to both deployment models.</span></span> <span data-ttu-id="3fba1-136">執行下列的 Cmdlet 以存取這兩種部署模型︰</span><span class="sxs-lookup"><span data-stu-id="3fba1-136">Run the following cmdlets to enable access to both deployment models:</span></span>

1. <span data-ttu-id="3fba1-137">取得電路詳細資料。</span><span class="sxs-lookup"><span data-stu-id="3fba1-137">Get the circuit details.</span></span>

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "DemoCkt" -ResourceGroupName "DemoRG"
  ```

2. <span data-ttu-id="3fba1-138">將 [允許傳統作業] 設定為 TRUE。</span><span class="sxs-lookup"><span data-stu-id="3fba1-138">Set "Allow Classic Operations" to TRUE.</span></span>

  ```powershell
  $ckt.AllowClassicOperations = $true
  ```

3. <span data-ttu-id="3fba1-139">更新電路。</span><span class="sxs-lookup"><span data-stu-id="3fba1-139">Update the circuit.</span></span> <span data-ttu-id="3fba1-140">成功完成這項作業後，您就可以在傳統部署模型中檢視電路。</span><span class="sxs-lookup"><span data-stu-id="3fba1-140">After this operation has finished successfully, you will be able to view the circuit in the classic deployment model.</span></span>

  ```powershell
  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

4. <span data-ttu-id="3fba1-141">執行下列 Cmdlet 以取得 ExpressRoute 電路的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="3fba1-141">Run the following cmdlet to get the details of the ExpressRoute circuit.</span></span> <span data-ttu-id="3fba1-142">您必須能夠看到列出的服務金鑰。</span><span class="sxs-lookup"><span data-stu-id="3fba1-142">You must be able to see the service key listed.</span></span>

  ```powershell
  get-azurededicatedcircuit
  ```

5. <span data-ttu-id="3fba1-143">您現在可以使用適用於傳統 VNet 的傳統部署模型命令，以及適用於 Resource Manager VNet 的 Resource Manager 命令，來管理 ExpressRoute 電路的連結。</span><span class="sxs-lookup"><span data-stu-id="3fba1-143">You can now manage links to the ExpressRoute circuit using the classic deployment model commands for classic VNets, and the Resource Manager commands for Resource Manager VNets.</span></span> <span data-ttu-id="3fba1-144">下列文件會協助您管理 ExpressRoute 線路的連結︰</span><span class="sxs-lookup"><span data-stu-id="3fba1-144">The following articles help you manage links to the ExpressRoute circuit:</span></span>

    * [<span data-ttu-id="3fba1-145">在 Resource Manager 部署模型中將虛擬網路連結到 ExpressRoute 電路</span><span class="sxs-lookup"><span data-stu-id="3fba1-145">Link your virtual network to your ExpressRoute circuit in the Resource Manager deployment model</span></span>](expressroute-howto-linkvnet-arm.md)
    * [<span data-ttu-id="3fba1-146">在傳統部署模型中將虛擬網路連結到 ExpressRoute 電路</span><span class="sxs-lookup"><span data-stu-id="3fba1-146">Link your virtual network to your ExpressRoute circuit in the classic deployment model</span></span>](expressroute-howto-linkvnet-classic.md)

### <a name="to-disable-expressroute-circuit-access-to-the-classic-deployment-model"></a><span data-ttu-id="3fba1-147">停用傳統部署模型的 ExpressRoute 電路存取</span><span class="sxs-lookup"><span data-stu-id="3fba1-147">To disable ExpressRoute circuit access to the classic deployment model</span></span>

<span data-ttu-id="3fba1-148">執行下列的 Cmdlet 以停止傳統部署模型的存取。</span><span class="sxs-lookup"><span data-stu-id="3fba1-148">Run the following cmdlets to disable access to the classic deployment model.</span></span>

1. <span data-ttu-id="3fba1-149">取得 ExpressRoute 電路的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="3fba1-149">Get details of the ExpressRoute circuit.</span></span>

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "DemoCkt" -ResourceGroupName "DemoRG"
  ```

2. <span data-ttu-id="3fba1-150">將 [允許傳統作業] 設定為 FALSE。</span><span class="sxs-lookup"><span data-stu-id="3fba1-150">Set "Allow Classic Operations" to FALSE.</span></span>

  ```powershell
  $ckt.AllowClassicOperations = $false
  ```

3. <span data-ttu-id="3fba1-151">更新電路。</span><span class="sxs-lookup"><span data-stu-id="3fba1-151">Update the circuit.</span></span> <span data-ttu-id="3fba1-152">成功完成這項作業後，您就不能在傳統部署模型中檢視電路。</span><span class="sxs-lookup"><span data-stu-id="3fba1-152">After this operation has finished successfully, you will not be able to view the circuit in the classic deployment model.</span></span>

  ```powershell
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

## <a name="next-steps"></a><span data-ttu-id="3fba1-153">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3fba1-153">Next steps</span></span>

* [<span data-ttu-id="3fba1-154">建立和修改 ExpressRoute 線路的路由</span><span class="sxs-lookup"><span data-stu-id="3fba1-154">Create and modify routing for your ExpressRoute circuit</span></span>](expressroute-howto-routing-arm.md)
* [<span data-ttu-id="3fba1-155">將虛擬網路連結至 ExpressRoute 線路</span><span class="sxs-lookup"><span data-stu-id="3fba1-155">Link your virtual network to your ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-arm.md)