---
title: "將 ExpressRoute 關聯的虛擬網路從傳統移轉至 Resource Manager：Azure：PowerShell | Microsoft Docs"
description: "此頁面描述如何在移動線路之後將關聯的虛擬網路移轉至 Resource Manager。"
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
ms.openlocfilehash: 964ea38569062a7127f60dd6309b328db263bf6f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="migrate-expressroute-associated-virtual-networks-from-classic-to-resource-manager"></a><span data-ttu-id="db59a-103">將 ExpressRoute 關聯的虛擬網路從傳統移至 Resource Manager</span><span class="sxs-lookup"><span data-stu-id="db59a-103">Migrate ExpressRoute associated virtual networks from classic to Resource Manager</span></span>

<span data-ttu-id="db59a-104">此文章說明如何在移動您的 ExpressRoute 線路之後將 Azure ExpressRoute 關聯的虛擬網路從傳統部署模型移轉至 Azure Resource Manager 部署模型。</span><span class="sxs-lookup"><span data-stu-id="db59a-104">This article explains how to migrate Azure ExpressRoute associated virtual networks from the classic deployment model to the Azure Resource Manager deployment model after moving your ExpressRoute circuit.</span></span> 


## <a name="before-you-begin"></a><span data-ttu-id="db59a-105">開始之前</span><span class="sxs-lookup"><span data-stu-id="db59a-105">Before you begin</span></span>
* <span data-ttu-id="db59a-106">請確認您有最新版的 Azure PowerShell 模組。</span><span class="sxs-lookup"><span data-stu-id="db59a-106">Verify that you have the latest version of the Azure PowerShell modules.</span></span> <span data-ttu-id="db59a-107">如需詳細資訊，請參閱 [如何安裝和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="db59a-107">For more information, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="db59a-108">開始設定之前，請確定您已經檢閱過[必要條件](expressroute-prerequisites.md)、[路由需求](expressroute-routing.md)和[工作流程](expressroute-workflows.md)。</span><span class="sxs-lookup"><span data-stu-id="db59a-108">Make sure that you have reviewed the [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="db59a-109">請檢閱[將 ExpressRoute 電路從傳統移至 Resource Manager](expressroute-move.md) 下提供的資訊。</span><span class="sxs-lookup"><span data-stu-id="db59a-109">Review the information that is provided under [Moving an ExpressRoute circuit from classic to Resource Manager](expressroute-move.md).</span></span> <span data-ttu-id="db59a-110">請確定您已完整了解各項限制。</span><span class="sxs-lookup"><span data-stu-id="db59a-110">Make sure that you fully understand the limits and limitations.</span></span>
* <span data-ttu-id="db59a-111">請確認電路在傳統部署模型中的運作完全正常。</span><span class="sxs-lookup"><span data-stu-id="db59a-111">Verify that the circuit is fully operational in the classic deployment model.</span></span>
* <span data-ttu-id="db59a-112">請確定您擁有建立在 Resource Manager 部署模型中建立的資源群組。</span><span class="sxs-lookup"><span data-stu-id="db59a-112">Ensure that you have a resource group that was created in the Resource Manager deployment model.</span></span>
* <span data-ttu-id="db59a-113">檢閱下列資源移轉文件︰</span><span class="sxs-lookup"><span data-stu-id="db59a-113">Review the following resource-migration documentation:</span></span>

    * [<span data-ttu-id="db59a-114">平台支援的 IaaS 資源移轉 (從傳統移轉至 Azure Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="db59a-114">Platform-supported migration of IaaS resources from classic to Azure Resource Manager</span></span>](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager.md)
    * [<span data-ttu-id="db59a-115">平台支援的從傳統移轉至 Azure Resource Manager 的技術深入探討</span><span class="sxs-lookup"><span data-stu-id="db59a-115">Technical deep dive on platform-supported migration from classic to Azure Resource Manager</span></span>](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager-deep-dive.md)
    * [<span data-ttu-id="db59a-116">常見問題集：平台支援的 IaaS 資源移轉 (從傳統移轉至 Azure Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="db59a-116">FAQs: Platform-supported migration of IaaS resources from classic to Azure Resource Manager</span></span>](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager.md)
    * [<span data-ttu-id="db59a-117">檢閱最常見的移轉錯誤和避免方式</span><span class="sxs-lookup"><span data-stu-id="db59a-117">Review most common migration errors and mitigations</span></span>](../virtual-machines/windows/migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="supported-and-unsupported-scenarios"></a><span data-ttu-id="db59a-118">支援和不支援的案例</span><span class="sxs-lookup"><span data-stu-id="db59a-118">Supported and unsupported scenarios</span></span>

* <span data-ttu-id="db59a-119">ExpressRoute 線路可以從傳統移轉至 Resource Manager 環境，而不需要停機。</span><span class="sxs-lookup"><span data-stu-id="db59a-119">An ExpressRoute circuit can be moved from the classic to the Resource Manager environment without any downtime.</span></span> <span data-ttu-id="db59a-120">您可以將任何 ExpressRoute 線路從傳統移轉至 Resource Manager 環境，而不需要停機。</span><span class="sxs-lookup"><span data-stu-id="db59a-120">You can move any ExpressRoute circuit from the classic to the Resource Manager environment with no downtime.</span></span> <span data-ttu-id="db59a-121">請依照[使用 PowerShell 將 ExpressRoute 線路從傳統部署模型移至 Resource Manager 部署模型](expressroute-howto-move-arm.md)中的指示執行。</span><span class="sxs-lookup"><span data-stu-id="db59a-121">Follow the instructions in [moving ExpressRoute circuits from the classic to the Resource Manager deployment model using PowerShell](expressroute-howto-move-arm.md).</span></span> <span data-ttu-id="db59a-122">這是將所連接資源移至虛擬網路的必要條件。</span><span class="sxs-lookup"><span data-stu-id="db59a-122">This is a prerequisite to move resources connected to the virtual network.</span></span>
* <span data-ttu-id="db59a-123">虛擬網路、閘道，以及虛擬網路中連結至相同訂用帳戶中 ExpressRoute 線路的相關聯部署，都可以移轉至 Resource Manager 環境，而不需要停機。</span><span class="sxs-lookup"><span data-stu-id="db59a-123">Virtual networks, gateways, and associated deployments within the virtual network that are attached to an ExpressRoute circuit in the same subscription can be migrated to the Resource Manager environment without any downtime.</span></span> <span data-ttu-id="db59a-124">您可以依照稍後描述的步驟來移轉資源，例如虛擬網路、閘道，以及虛擬網路中部署的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="db59a-124">You can follow the steps described later to migrate resources such as virtual networks, gateways, and virtual machines deployed within the virtual network.</span></span> <span data-ttu-id="db59a-125">您必須確保虛擬網路在移轉之前都已正確設定。</span><span class="sxs-lookup"><span data-stu-id="db59a-125">You must ensure that the virtual networks are configured correctly before they are migrated.</span></span> 
* <span data-ttu-id="db59a-126">虛擬網路、閘道，以及虛擬網路內與 ExpressRoute 線路位於不同訂用帳戶的相關聯部署，都需要一些停機時間，才能完成移轉。</span><span class="sxs-lookup"><span data-stu-id="db59a-126">Virtual networks, gateways, and associated deployments within the virtual network that are not in the same subscription as the ExpressRoute circuit require some downtime to complete the migration.</span></span> <span data-ttu-id="db59a-127">本文件的最後一節描述移轉資源所需遵循的步驟。</span><span class="sxs-lookup"><span data-stu-id="db59a-127">The last section of the document describes the steps to be followed to migrate resources.</span></span>
* <span data-ttu-id="db59a-128">無法移轉同時具有「ExpressRoute 閘道」和「VPN 閘道」的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="db59a-128">A virtual network with both ExpressRoute Gateway and VPN Gateway can't be migrated.</span></span>

## <a name="move-an-expressroute-circuit-from-classic-to-resource-manager"></a><span data-ttu-id="db59a-129">將 ExpressRoute 線路從傳統移到 Resource Manager</span><span class="sxs-lookup"><span data-stu-id="db59a-129">Move an ExpressRoute circuit from classic to Resource Manager</span></span>
<span data-ttu-id="db59a-130">嘗試移轉已連結至 ExpressRoute 線路的資源之前，您必須先將 ExpressRoute 線路從傳統移至 Resource Manager 環境。</span><span class="sxs-lookup"><span data-stu-id="db59a-130">You must move an ExpressRoute circuit from the classic to the Resource Manager environment before you try to migrate resources that are attached to the ExpressRoute circuit.</span></span> <span data-ttu-id="db59a-131">若要完成此工作，請參閱下列文章：</span><span class="sxs-lookup"><span data-stu-id="db59a-131">To accomplish this task, see the following articles:</span></span>

* <span data-ttu-id="db59a-132">請檢閱[將 ExpressRoute 電路從傳統移至 Resource Manager](expressroute-move.md) 下提供的資訊。</span><span class="sxs-lookup"><span data-stu-id="db59a-132">Review the information that is provided under [Moving an ExpressRoute circuit from classic to Resource Manager](expressroute-move.md).</span></span>
* <span data-ttu-id="db59a-133">[使用 Azure PowerShell 將戲路從傳統移至 Resource Manager](expressroute-howto-move-arm.md)。</span><span class="sxs-lookup"><span data-stu-id="db59a-133">[Move a circuit from classic to Resource Manager using Azure PowerShell](expressroute-howto-move-arm.md).</span></span>
* <span data-ttu-id="db59a-134">使用 Azure 服務管理入口網站。</span><span class="sxs-lookup"><span data-stu-id="db59a-134">Use the Azure Service Management portal.</span></span> <span data-ttu-id="db59a-135">您可以依照工作流程來[建立新的 ExpressRoute 線路](expressroute-howto-circuit-portal-resource-manager.md)並選取匯入選項。</span><span class="sxs-lookup"><span data-stu-id="db59a-135">You can follow the workflow to [create a new ExpressRoute circuit](expressroute-howto-circuit-portal-resource-manager.md) and select the import option.</span></span> 

<span data-ttu-id="db59a-136">這項作業不需要停機。</span><span class="sxs-lookup"><span data-stu-id="db59a-136">This operation does not involve downtime.</span></span> <span data-ttu-id="db59a-137">進行移轉時，您可以繼續在內部部署與 Microsoft 之間傳輸資料。</span><span class="sxs-lookup"><span data-stu-id="db59a-137">You can continue to transfer data between your premises and Microsoft while the migration is in progress.</span></span>

## <a name="migrate-virtual-networks-gateways-and-associated-deployments"></a><span data-ttu-id="db59a-138">移轉虛擬網路、閘道與關聯的部署</span><span class="sxs-lookup"><span data-stu-id="db59a-138">Migrate virtual networks, gateways, and associated deployments</span></span>

<span data-ttu-id="db59a-139">移轉步驟取決於您的資源位於相同訂用帳戶、位於不同訂用帳戶，或混合兩者的情況。</span><span class="sxs-lookup"><span data-stu-id="db59a-139">The steps you follow to migrate depend on whether your resources are in the same subscription, different subscriptions, or both.</span></span>

### <a name="migrate-virtual-networks-gateways-and-associated-deployments-in-the-same-subscription-as-the-expressroute-circuit"></a><span data-ttu-id="db59a-140">移轉虛擬網路、閘道，以及與 ExpressRoute 線路位於相同訂用帳戶的相關聯部署。</span><span class="sxs-lookup"><span data-stu-id="db59a-140">Migrate virtual networks, gateways, and associated deployments in the same subscription as the ExpressRoute circuit</span></span>
<span data-ttu-id="db59a-141">這一節說明移轉虛擬網路、閘道，以及與 ExpressRoute 線路位於相同訂用帳戶的相關聯部署所需遵循的步驟。</span><span class="sxs-lookup"><span data-stu-id="db59a-141">This section describes the steps to be followed to migrate a virtual network, gateway, and associated deployments in the same subscription as the ExpressRoute circuit.</span></span> <span data-ttu-id="db59a-142">這項移轉不需要停機。</span><span class="sxs-lookup"><span data-stu-id="db59a-142">No downtime is associated with this migration.</span></span> <span data-ttu-id="db59a-143">您可以透過移轉程序繼續使用所有資源。</span><span class="sxs-lookup"><span data-stu-id="db59a-143">You can continue to use all resources through the migration process.</span></span> <span data-ttu-id="db59a-144">管理平面會在移轉進行時遭到封鎖。</span><span class="sxs-lookup"><span data-stu-id="db59a-144">The management plane is locked while the migration is in progress.</span></span> 

1. <span data-ttu-id="db59a-145">確保 ExpressRoute 線路已從傳統移至 Resource Manager 環境。</span><span class="sxs-lookup"><span data-stu-id="db59a-145">Ensure that the ExpressRoute circuit has been moved from the classic to the Resource Manager environment.</span></span>
2. <span data-ttu-id="db59a-146">確保已為了移轉適當地準備虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="db59a-146">Ensure that the virtual network has been prepared appropriately for the migration.</span></span>
3. <span data-ttu-id="db59a-147">註冊您的訂用帳戶以便移轉資源。</span><span class="sxs-lookup"><span data-stu-id="db59a-147">Register your subscription for resource migration.</span></span> <span data-ttu-id="db59a-148">若要註冊您的訂用帳戶以便移轉資源，請使用下列 PowerShell 程式碼片段︰</span><span class="sxs-lookup"><span data-stu-id="db59a-148">To register your subscription for resource migration, use the following PowerShell snippet:</span></span>

  ```powershell 
  Select-AzureRmSubscription -SubscriptionName <Your Subscription Name>
  Register-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
  Get-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
  ```
4. <span data-ttu-id="db59a-149">驗證、準備和移轉。</span><span class="sxs-lookup"><span data-stu-id="db59a-149">Validate, prepare, and migrate.</span></span> <span data-ttu-id="db59a-150">若要移轉虛擬網路，請使用下列 PowerShell 程式碼片段︰</span><span class="sxs-lookup"><span data-stu-id="db59a-150">To move the virtual network, use the following PowerShell snippet:</span></span>

  ```powershell
  Move-AzureVirtualNetwork -Prepare $vnetName  
  Move-AzureVirtualNetwork -Commit $vnetName
  ```

  <span data-ttu-id="db59a-151">您也可以執行下列 PowerShell Cmdlet 來中止移轉：</span><span class="sxs-lookup"><span data-stu-id="db59a-151">You can also abort migration by running the following PowerShell cmdlet:</span></span>

  ```powershell
  Move-AzureVirtualNetwork -Abort $vnetName
  ```

## <a name="next-steps"></a><span data-ttu-id="db59a-152">後續步驟</span><span class="sxs-lookup"><span data-stu-id="db59a-152">Next steps</span></span>
* [<span data-ttu-id="db59a-153">平台支援的 IaaS 資源移轉 (從傳統移轉至 Azure Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="db59a-153">Platform-supported migration of IaaS resources from classic to Azure Resource Manager</span></span>](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager.md)
* [<span data-ttu-id="db59a-154">平台支援的從傳統移轉至 Azure Resource Manager 的技術深入探討</span><span class="sxs-lookup"><span data-stu-id="db59a-154">Technical deep dive on platform-supported migration from classic to Azure Resource Manager</span></span>](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager-deep-dive.md)
* [<span data-ttu-id="db59a-155">常見問題集：平台支援的 IaaS 資源移轉 (從傳統移轉至 Azure Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="db59a-155">FAQs: Platform-supported migration of IaaS resources from classic to Azure Resource Manager</span></span>](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager.md)
* [<span data-ttu-id="db59a-156">檢閱最常見的移轉錯誤和避免方式</span><span class="sxs-lookup"><span data-stu-id="db59a-156">Review most common migration errors and mitigations</span></span>](../virtual-machines/windows/migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
