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
# <a name="migrate-expressroute-associated-virtual-networks-from-classic-tooresource-manager"></a><span data-ttu-id="984d6-103">從傳統 tooResource Manager 移轉相關聯的 ExpressRoute 的虛擬網路</span><span class="sxs-lookup"><span data-stu-id="984d6-103">Migrate ExpressRoute associated virtual networks from classic tooResource Manager</span></span>

<span data-ttu-id="984d6-104">本文說明 toomigrate Azure ExpressRoute 移動 ExpressRoute 電路之後所關聯的虛擬網路與 hello 傳統部署模型 toohello Azure Resource Manager 部署模型。</span><span class="sxs-lookup"><span data-stu-id="984d6-104">This article explains how toomigrate Azure ExpressRoute associated virtual networks from hello classic deployment model toohello Azure Resource Manager deployment model after moving your ExpressRoute circuit.</span></span> 


## <a name="before-you-begin"></a><span data-ttu-id="984d6-105">開始之前</span><span class="sxs-lookup"><span data-stu-id="984d6-105">Before you begin</span></span>
* <span data-ttu-id="984d6-106">確認您擁有 hello hello Azure PowerShell 模組最新版本。</span><span class="sxs-lookup"><span data-stu-id="984d6-106">Verify that you have hello latest version of hello Azure PowerShell modules.</span></span> <span data-ttu-id="984d6-107">如需詳細資訊，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="984d6-107">For more information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="984d6-108">請確定您已經檢閱 hello[必要條件](expressroute-prerequisites.md)，[路由需求](expressroute-routing.md)，和[工作流程](expressroute-workflows.md)開始設定之前。</span><span class="sxs-lookup"><span data-stu-id="984d6-108">Make sure that you have reviewed hello [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="984d6-109">檢閱底下提供的 hello 資訊[從傳統 tooResource 管理員移動的 ExpressRoute 電路](expressroute-move.md)。</span><span class="sxs-lookup"><span data-stu-id="984d6-109">Review hello information that is provided under [Moving an ExpressRoute circuit from classic tooResource Manager](expressroute-move.md).</span></span> <span data-ttu-id="984d6-110">請確定您完全瞭解 hello 限制和限制。</span><span class="sxs-lookup"><span data-stu-id="984d6-110">Make sure that you fully understand hello limits and limitations.</span></span>
* <span data-ttu-id="984d6-111">請確認 hello 循環可完全運作 hello 傳統部署模型中。</span><span class="sxs-lookup"><span data-stu-id="984d6-111">Verify that hello circuit is fully operational in hello classic deployment model.</span></span>
* <span data-ttu-id="984d6-112">確定您擁有 hello Resource Manager 部署模型中所建立的資源群組。</span><span class="sxs-lookup"><span data-stu-id="984d6-112">Ensure that you have a resource group that was created in hello Resource Manager deployment model.</span></span>
* <span data-ttu-id="984d6-113">檢閱下列資源移轉文件的 hello:</span><span class="sxs-lookup"><span data-stu-id="984d6-113">Review hello following resource-migration documentation:</span></span>

    * [<span data-ttu-id="984d6-114">平台支援移轉從傳統 tooAzure 資源管理員的 IaaS 資源</span><span class="sxs-lookup"><span data-stu-id="984d6-114">Platform-supported migration of IaaS resources from classic tooAzure Resource Manager</span></span>](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager.md)
    * [<span data-ttu-id="984d6-115">技術的深入剖析平台支援移轉從傳統 tooAzure 資源管理員</span><span class="sxs-lookup"><span data-stu-id="984d6-115">Technical deep dive on platform-supported migration from classic tooAzure Resource Manager</span></span>](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager-deep-dive.md)
    * [<span data-ttu-id="984d6-116">常見問題集： 平台支援移轉 IaaS 資源從傳統 tooAzure 資源管理員</span><span class="sxs-lookup"><span data-stu-id="984d6-116">FAQs: Platform-supported migration of IaaS resources from classic tooAzure Resource Manager</span></span>](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager.md)
    * [<span data-ttu-id="984d6-117">檢閱最常見的移轉錯誤和避免方式</span><span class="sxs-lookup"><span data-stu-id="984d6-117">Review most common migration errors and mitigations</span></span>](../virtual-machines/windows/migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="supported-and-unsupported-scenarios"></a><span data-ttu-id="984d6-118">支援和不支援的案例</span><span class="sxs-lookup"><span data-stu-id="984d6-118">Supported and unsupported scenarios</span></span>

* <span data-ttu-id="984d6-119">可以從 hello 傳統 toohello 資源管理員的環境沒有任何停機時間移動的 ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="984d6-119">An ExpressRoute circuit can be moved from hello classic toohello Resource Manager environment without any downtime.</span></span> <span data-ttu-id="984d6-120">您可以將任何 ExpressRoute 電路移 hello 傳統 toohello 資源管理員環境沒有停機。</span><span class="sxs-lookup"><span data-stu-id="984d6-120">You can move any ExpressRoute circuit from hello classic toohello Resource Manager environment with no downtime.</span></span> <span data-ttu-id="984d6-121">請依照下列中的 hello 指示[hello 傳統 toohello Resource Manager 部署模型使用 PowerShell 從移動 ExpressRoute 電路](expressroute-howto-move-arm.md)。</span><span class="sxs-lookup"><span data-stu-id="984d6-121">Follow hello instructions in [moving ExpressRoute circuits from hello classic toohello Resource Manager deployment model using PowerShell](expressroute-howto-move-arm.md).</span></span> <span data-ttu-id="984d6-122">這是必要條件 toomove 資源連線的 toohello 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="984d6-122">This is a prerequisite toomove resources connected toohello virtual network.</span></span>
* <span data-ttu-id="984d6-123">虛擬網路、 閘道和相關聯的部署 hello 虛擬網路內附加的 tooan hello 可以是相同的訂用帳戶中的 ExpressRoute 電路移轉 toohello 資源管理員環境完全不需要停機。</span><span class="sxs-lookup"><span data-stu-id="984d6-123">Virtual networks, gateways, and associated deployments within hello virtual network that are attached tooan ExpressRoute circuit in hello same subscription can be migrated toohello Resource Manager environment without any downtime.</span></span> <span data-ttu-id="984d6-124">您可以依照 hello 步驟所述更新 toomigrate 資源，例如虛擬網路、 閘道和 hello 虛擬網路內部署的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="984d6-124">You can follow hello steps described later toomigrate resources such as virtual networks, gateways, and virtual machines deployed within hello virtual network.</span></span> <span data-ttu-id="984d6-125">您必須確定在移轉之前 hello 虛擬網路已正確設定。</span><span class="sxs-lookup"><span data-stu-id="984d6-125">You must ensure that hello virtual networks are configured correctly before they are migrated.</span></span> 
* <span data-ttu-id="984d6-126">虛擬網路、 閘道和相關聯的部署中的 hello 虛擬網路內 hello 相同訂用帳戶，因為 hello ExpressRoute 電路需要一些停機時間 toocomplete hello 移轉。</span><span class="sxs-lookup"><span data-stu-id="984d6-126">Virtual networks, gateways, and associated deployments within hello virtual network that are not in hello same subscription as hello ExpressRoute circuit require some downtime toocomplete hello migration.</span></span> <span data-ttu-id="984d6-127">hello hello 文件的最後一節描述 hello 步驟後面的 toobe toomigrate 資源。</span><span class="sxs-lookup"><span data-stu-id="984d6-127">hello last section of hello document describes hello steps toobe followed toomigrate resources.</span></span>
* <span data-ttu-id="984d6-128">無法移轉同時具有「ExpressRoute 閘道」和「VPN 閘道」的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="984d6-128">A virtual network with both ExpressRoute Gateway and VPN Gateway can't be migrated.</span></span>

## <a name="move-an-expressroute-circuit-from-classic-tooresource-manager"></a><span data-ttu-id="984d6-129">從傳統 tooResource 管理員移動的 ExpressRoute 電路</span><span class="sxs-lookup"><span data-stu-id="984d6-129">Move an ExpressRoute circuit from classic tooResource Manager</span></span>
<span data-ttu-id="984d6-130">您必須移動 hello 傳統 toohello 資源管理員環境再 toomigrate 資源從 ExpressRoute 電路附加 toohello ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="984d6-130">You must move an ExpressRoute circuit from hello classic toohello Resource Manager environment before you try toomigrate resources that are attached toohello ExpressRoute circuit.</span></span> <span data-ttu-id="984d6-131">tooaccomplish 這項工作，請參閱下列文章 hello:</span><span class="sxs-lookup"><span data-stu-id="984d6-131">tooaccomplish this task, see hello following articles:</span></span>

* <span data-ttu-id="984d6-132">檢閱底下提供的 hello 資訊[從傳統 tooResource 管理員移動的 ExpressRoute 電路](expressroute-move.md)。</span><span class="sxs-lookup"><span data-stu-id="984d6-132">Review hello information that is provided under [Moving an ExpressRoute circuit from classic tooResource Manager](expressroute-move.md).</span></span>
* <span data-ttu-id="984d6-133">[從傳統 tooResource 管理員使用 Azure PowerShell 移動電路](expressroute-howto-move-arm.md)。</span><span class="sxs-lookup"><span data-stu-id="984d6-133">[Move a circuit from classic tooResource Manager using Azure PowerShell](expressroute-howto-move-arm.md).</span></span>
* <span data-ttu-id="984d6-134">使用 hello Azure 服務管理入口網站。</span><span class="sxs-lookup"><span data-stu-id="984d6-134">Use hello Azure Service Management portal.</span></span> <span data-ttu-id="984d6-135">您可以依照 hello 工作流程太[建立新的 ExpressRoute 電路](expressroute-howto-circuit-portal-resource-manager.md)並選取 hello 匯入選項。</span><span class="sxs-lookup"><span data-stu-id="984d6-135">You can follow hello workflow too[create a new ExpressRoute circuit](expressroute-howto-circuit-portal-resource-manager.md) and select hello import option.</span></span> 

<span data-ttu-id="984d6-136">這項作業不需要停機。</span><span class="sxs-lookup"><span data-stu-id="984d6-136">This operation does not involve downtime.</span></span> <span data-ttu-id="984d6-137">Hello 移轉正在進行時，您可以繼續 tootransfer 您內部部署和 Microsoft 之間的資料。</span><span class="sxs-lookup"><span data-stu-id="984d6-137">You can continue tootransfer data between your premises and Microsoft while hello migration is in progress.</span></span>

## <a name="migrate-virtual-networks-gateways-and-associated-deployments"></a><span data-ttu-id="984d6-138">移轉虛擬網路、閘道與關聯的部署</span><span class="sxs-lookup"><span data-stu-id="984d6-138">Migrate virtual networks, gateways, and associated deployments</span></span>

<span data-ttu-id="984d6-139">hello 遵循 toomigrate 步驟取決於您的資源是否 hello 相同訂用帳戶、 不同的訂用帳戶，或兩者。</span><span class="sxs-lookup"><span data-stu-id="984d6-139">hello steps you follow toomigrate depend on whether your resources are in hello same subscription, different subscriptions, or both.</span></span>

### <a name="migrate-virtual-networks-gateways-and-associated-deployments-in-hello-same-subscription-as-hello-expressroute-circuit"></a><span data-ttu-id="984d6-140">移轉虛擬網路閘道，以及相關聯的部署中 hello 相同訂用帳戶，因為 hello ExpressRoute 電路</span><span class="sxs-lookup"><span data-stu-id="984d6-140">Migrate virtual networks, gateways, and associated deployments in hello same subscription as hello ExpressRoute circuit</span></span>
<span data-ttu-id="984d6-141">本章節描述 hello 步驟後面的 toobe toomigrate 虛擬網路、 閘道和相關聯的部署中 hello 相同訂用帳戶為 hello ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="984d6-141">This section describes hello steps toobe followed toomigrate a virtual network, gateway, and associated deployments in hello same subscription as hello ExpressRoute circuit.</span></span> <span data-ttu-id="984d6-142">這項移轉不需要停機。</span><span class="sxs-lookup"><span data-stu-id="984d6-142">No downtime is associated with this migration.</span></span> <span data-ttu-id="984d6-143">您可以繼續 toouse 透過 hello 移轉程序的所有資源。</span><span class="sxs-lookup"><span data-stu-id="984d6-143">You can continue toouse all resources through hello migration process.</span></span> <span data-ttu-id="984d6-144">hello 移轉正在進行時，會鎖定 hello 管理平面。</span><span class="sxs-lookup"><span data-stu-id="984d6-144">hello management plane is locked while hello migration is in progress.</span></span> 

1. <span data-ttu-id="984d6-145">請從 hello 傳統 toohello 資源管理員環境的 hello ExpressRoute 循環到已移。</span><span class="sxs-lookup"><span data-stu-id="984d6-145">Ensure that hello ExpressRoute circuit has been moved from hello classic toohello Resource Manager environment.</span></span>
2. <span data-ttu-id="984d6-146">請確定該 hello 虛擬網路已經準備適當 hello 移轉。</span><span class="sxs-lookup"><span data-stu-id="984d6-146">Ensure that hello virtual network has been prepared appropriately for hello migration.</span></span>
3. <span data-ttu-id="984d6-147">註冊您的訂用帳戶以便移轉資源。</span><span class="sxs-lookup"><span data-stu-id="984d6-147">Register your subscription for resource migration.</span></span> <span data-ttu-id="984d6-148">tooregister 資源移轉，使用下列 PowerShell 程式碼片段的 hello 的訂用帳戶：</span><span class="sxs-lookup"><span data-stu-id="984d6-148">tooregister your subscription for resource migration, use hello following PowerShell snippet:</span></span>

  ```powershell 
  Select-AzureRmSubscription -SubscriptionName <Your Subscription Name>
  Register-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
  Get-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
  ```
4. <span data-ttu-id="984d6-149">驗證、準備和移轉。</span><span class="sxs-lookup"><span data-stu-id="984d6-149">Validate, prepare, and migrate.</span></span> <span data-ttu-id="984d6-150">toomove hello 虛擬網路，使用下列 PowerShell 程式碼片段的 hello:</span><span class="sxs-lookup"><span data-stu-id="984d6-150">toomove hello virtual network, use hello following PowerShell snippet:</span></span>

  ```powershell
  Move-AzureVirtualNetwork -Prepare $vnetName  
  Move-AzureVirtualNetwork -Commit $vnetName
  ```

  <span data-ttu-id="984d6-151">您也可以藉由執行下列 PowerShell cmdlet 的 hello 中止移轉：</span><span class="sxs-lookup"><span data-stu-id="984d6-151">You can also abort migration by running hello following PowerShell cmdlet:</span></span>

  ```powershell
  Move-AzureVirtualNetwork -Abort $vnetName
  ```

## <a name="next-steps"></a><span data-ttu-id="984d6-152">後續步驟</span><span class="sxs-lookup"><span data-stu-id="984d6-152">Next steps</span></span>
* [<span data-ttu-id="984d6-153">平台支援移轉從傳統 tooAzure 資源管理員的 IaaS 資源</span><span class="sxs-lookup"><span data-stu-id="984d6-153">Platform-supported migration of IaaS resources from classic tooAzure Resource Manager</span></span>](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager.md)
* [<span data-ttu-id="984d6-154">技術的深入剖析平台支援移轉從傳統 tooAzure 資源管理員</span><span class="sxs-lookup"><span data-stu-id="984d6-154">Technical deep dive on platform-supported migration from classic tooAzure Resource Manager</span></span>](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager-deep-dive.md)
* [<span data-ttu-id="984d6-155">常見問題集： 平台支援移轉 IaaS 資源從傳統 tooAzure 資源管理員</span><span class="sxs-lookup"><span data-stu-id="984d6-155">FAQs: Platform-supported migration of IaaS resources from classic tooAzure Resource Manager</span></span>](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager.md)
* [<span data-ttu-id="984d6-156">檢閱最常見的移轉錯誤和避免方式</span><span class="sxs-lookup"><span data-stu-id="984d6-156">Review most common migration errors and mitigations</span></span>](../virtual-machines/windows/migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
