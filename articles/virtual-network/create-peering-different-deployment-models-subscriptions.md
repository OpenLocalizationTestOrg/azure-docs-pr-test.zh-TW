---
title: "建立 Azure 虛擬網路對等互連 - 不同部署模型 - 不同訂用帳戶 |Microsoft Docs"
description: "了解如何在透過不同 Azure 部署模型建立且存在於不同 Azure 訂用帳戶中的虛擬網路之間，建立虛擬網路對等互連。"
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/17/2017
ms.author: jdial;narayan;annahar
ms.openlocfilehash: 93d5676e9188e67f1f6a9bba1d4d30a93b3883d8
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/29/2017
---
# <a name="create-a-virtual-network-peering---different-deployment-models-and-subscriptions"></a><span data-ttu-id="e8a8f-103">建立虛擬網路對等互連 - 不同部署模型和訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="e8a8f-103">Create a virtual network peering - different deployment models and subscriptions</span></span>

<span data-ttu-id="e8a8f-104">在本教學課程中，您會了解如何在透過不同部署模型建立的虛擬網路之間，建立虛擬網路對等互連。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-104">In this tutorial, you learn to create a virtual network peering between virtual networks created through different deployment models.</span></span> <span data-ttu-id="e8a8f-105">這些虛擬網路存在於不同的訂用帳戶中。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-105">The virtual networks exist in different subscriptions.</span></span> <span data-ttu-id="e8a8f-106">對等互連兩個虛擬網路，可讓不同虛擬網路中的資源彼此通訊，且通訊時會有相同的頻寬和延遲，彷彿這些資源是位於相同的虛擬網路中。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-106">Peering two virtual networks enables resources in different virtual networks to communicate with each other with the same bandwidth and latency as though the resources were in the same virtual network.</span></span> <span data-ttu-id="e8a8f-107">深入了解[虛擬網路對等互連](virtual-network-peering-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-107">Learn more about [Virtual network peering](virtual-network-peering-overview.md).</span></span> 

<span data-ttu-id="e8a8f-108">建立虛擬網路對等互連的步驟會因一些因素而有所不同，這取決於虛擬網路是位於相同還是不同的訂用帳戶中，以及是透過哪一個 [Azure 部署模型](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json)建立虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-108">The steps to create a virtual network peering are different, depending on whether the virtual networks are in the same, or different, subscriptions, and which [Azure deployment model](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) the virtual networks are created through.</span></span> <span data-ttu-id="e8a8f-109">請按一下下表中的案例，以了解如何在其他案例中建立虛擬網路對等互連：</span><span class="sxs-lookup"><span data-stu-id="e8a8f-109">Learn how to create a virtual network peering in other scenarios by clicking the scenario from the following table:</span></span>

|<span data-ttu-id="e8a8f-110">Azure 部署模型</span><span class="sxs-lookup"><span data-stu-id="e8a8f-110">Azure deployment model</span></span>  | <span data-ttu-id="e8a8f-111">Azure 訂閱</span><span class="sxs-lookup"><span data-stu-id="e8a8f-111">Azure subscription</span></span>  |
|--------- |---------|
|[<span data-ttu-id="e8a8f-112">兩者皆使用 Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e8a8f-112">Both Resource Manager</span></span>](virtual-network-create-peering.md) |<span data-ttu-id="e8a8f-113">相同</span><span class="sxs-lookup"><span data-stu-id="e8a8f-113">Same</span></span>|
|[<span data-ttu-id="e8a8f-114">兩者皆使用 Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e8a8f-114">Both Resource Manager</span></span>](create-peering-different-subscriptions.md) |<span data-ttu-id="e8a8f-115">不同</span><span class="sxs-lookup"><span data-stu-id="e8a8f-115">Different</span></span>|
|[<span data-ttu-id="e8a8f-116">一個使用 Resource Manager、一個使用傳統部署模型</span><span class="sxs-lookup"><span data-stu-id="e8a8f-116">One Resource Manager, one classic</span></span>](create-peering-different-deployment-models.md) |<span data-ttu-id="e8a8f-117">相同</span><span class="sxs-lookup"><span data-stu-id="e8a8f-117">Same</span></span>|

<span data-ttu-id="e8a8f-118">虛擬網路對等互連無法在透過傳統部署模型建立的兩個虛擬網路之間建立。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-118">A virtual network peering cannot be created between two virtual networks deployed through the classic deployment model.</span></span> <span data-ttu-id="e8a8f-119">只能在存在於相同 Azure 區域中的兩個虛擬網路之間建立虛擬網路對等互連。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-119">A virtual network peering can only be created between two virtual networks that exist in the same Azure region.</span></span> <span data-ttu-id="e8a8f-120">在存在於不同訂用帳戶中的虛擬網路之間建立虛擬網路對等互連時，兩個訂用帳戶必須都與相同的 Azure Active Directory 租用戶關聯。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-120">When creating a virtual network peering between virtual networks that exist in different subscriptions, the subscriptions must both be associated to the same Azure Active Directory tenant.</span></span> <span data-ttu-id="e8a8f-121">如果您還沒有 Azure Active Directory 租用戶，可以快速地[建立一個租用戶](../active-directory/develop/active-directory-howto-tenant.md?toc=%2fazure%2fvirtual-network%2ftoc.json#start-from-scratch)。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-121">If you don't already have an Azure Active Directory tenant, you can quickly [create one](../active-directory/develop/active-directory-howto-tenant.md?toc=%2fazure%2fvirtual-network%2ftoc.json#start-from-scratch).</span></span> <span data-ttu-id="e8a8f-122">如果您需要將兩個都是透過傳統部署模型建立的虛擬網路連接、將存在於不同 Azure 區域中的虛擬網路連接，或是將存在於與不同 Azure Active Directory 租用戶關聯之訂用帳戶中的虛擬網路連接，可以使用 Azure [VPN 閘道](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json)來連接這些虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-122">If you need to connect virtual networks that were both created through the classic deployment model, or that exist in different Azure regions, or that exist in subscriptions associated to different Azure Active Directory tenants, you can use an Azure [VPN Gateway](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) to connect the virtual networks.</span></span> 

> [!WARNING]
> <span data-ttu-id="e8a8f-123">在透過不同 Azure 部署模型建立且存在於不同訂用帳戶中的虛擬網路之間建立虛擬網路對等互連，目前是預覽版功能。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-123">Creating a virtual network peering between virtual networks in created through different Azure deployment models that exist in different subscriptions is currently in preview.</span></span> <span data-ttu-id="e8a8f-124">在此情況下建立的虛擬網路對等互連，與在正式發行版情況下建立的虛擬網路對等互連，可能不會有相同等級的可用性和可靠性。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-124">Virtual network peerings created in this scenario may not have the same level of availability and reliability as creating a virtual network peering in scenarios in general availability release.</span></span> <span data-ttu-id="e8a8f-125">在此情況下建立的虛擬網路對等互連不受支援、可能功能受限，且可能並非在所有 Azure 區域中都可供使用。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-125">Virtual network peerings created in this scenario are not supported, may have constrained capabilities, and may not be available in all Azure regions.</span></span> <span data-ttu-id="e8a8f-126">如需此功能可用性和狀態的最新通知，請查看 [Azure 虛擬網路更新](https://azure.microsoft.com/updates/?product=virtual-network) 頁面。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-126">For the most up-to-date notifications on availability and status of this feature, check the [Azure Virtual Network updates](https://azure.microsoft.com/updates/?product=virtual-network) page.</span></span>

<span data-ttu-id="e8a8f-127">您可以使用 [Azure 入口網站](#portal)、Azure [命令列介面](#cli) (CLI) 或 Azure [PowerShell](#powershell) 來建立虛擬網路對等互連。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-127">You can use the [Azure portal](#portal), the Azure [command-line interface](#cli) (CLI), or Azure [PowerShell](#powershell) to create a virtual network peering.</span></span> <span data-ttu-id="e8a8f-128">按一下任何先前的工具連結，直接前往使用您所選工具建立虛擬網路對等互連的步驟。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-128">Click any of the previous tool links to go directly to the steps for creating a virtual network peering using your tool of choice.</span></span>

## <span data-ttu-id="e8a8f-129"><a name="register"></a>註冊預覽版</span><span class="sxs-lookup"><span data-stu-id="e8a8f-129"><a name="register"></a>Register for the preview</span></span>

<span data-ttu-id="e8a8f-130">若要註冊預覽版，請針對包含您想要對等互連之虛擬網路的兩個訂用帳戶，完成接下來的步驟。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-130">To register for the preview, complete the steps that follow for both subscriptions that contain the virtual networks you want to peer.</span></span> <span data-ttu-id="e8a8f-131">您唯一可用來註冊預覽版的工具是 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-131">The only tool you can use to register for the preview is PowerShell.</span></span>

1. <span data-ttu-id="e8a8f-132">安裝最新版的 PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) 模組。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-132">Install the latest version of the PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) module.</span></span> <span data-ttu-id="e8a8f-133">如果您不熟悉 Azure PowerShell，請參閱 [Azure PowerShell 概觀](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-133">If you're new to Azure PowerShell, see [Azure PowerShell overview](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="e8a8f-134">啟動 PowerShell 工作階段，然後使用 `login-azurermaccount` 命令來登入 Azure。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-134">Start a PowerShell session and log in to Azure using the `login-azurermaccount` command.</span></span>
3. <span data-ttu-id="e8a8f-135">輸入下列命令來針對預覽版註冊您的訂用帳戶︰</span><span class="sxs-lookup"><span data-stu-id="e8a8f-135">Register your subscription for the preview by entering the following commands:</span></span>

    ```powershell
    Register-AzureRmProviderFeature `
      -FeatureName AllowClassicCrossSubscriptionPeering `
      -ProviderNamespace Microsoft.Network
    
    Register-AzureRmResourceProvider `
      -ProviderNamespace Microsoft.Network
    ```
    <span data-ttu-id="e8a8f-136">請等到您為兩個訂用帳戶輸入下列命令後所收到的 **RegistrationState** 輸出都變成 **Registered** 之後，才完成本文中入口網站、Azure CLI 或 PowerShell 等節中的步驟：</span><span class="sxs-lookup"><span data-stu-id="e8a8f-136">Do not complete the steps in the Portal, Azure CLI, or PowerShell sections of this article until the **RegistrationState** output you receive after entering the following command is **Registered** for both subscriptions:</span></span>

    ```powershell    
    Get-AzureRmProviderFeature `
      -FeatureName AllowClassicCrossSubscriptionPeering `
      -ProviderNamespace Microsoft.Network
    ```

## <span data-ttu-id="e8a8f-137"><a name="portal"></a>建立對等互連 - Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="e8a8f-137"><a name="portal"></a>Create peering - Azure portal</span></span>

<span data-ttu-id="e8a8f-138">本教學課程針對每個訂用帳戶使用不同的帳戶。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-138">This tutorial uses different accounts for each subscription.</span></span> <span data-ttu-id="e8a8f-139">如果您使用對兩個訂用帳戶都有權限的帳戶，便可以使用該相同帳戶來進行所有步驟、略過登出入口網站的步驟，以及略過指派另一位使用者權限給虛擬網路的步驟。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-139">If you're using an account that has permissions to both subscriptions, you can use the same account for all steps, skip the steps for logging out of the portal, and skip the steps for assigning another user permissions to the virtual networks.</span></span> <span data-ttu-id="e8a8f-140">在完成下列任何步驟之前，您必須先註冊預覽版。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-140">Before completing any of the following steps, you must register for the preview.</span></span> <span data-ttu-id="e8a8f-141">若要註冊，請完成本文中[註冊預覽版](#register)一節中的步驟。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-141">To register, complete the steps in the [Register for the preview](#register) section of this article.</span></span> <span data-ttu-id="e8a8f-142">請等到兩個訂用帳戶都已針對預覽版註冊之後，才繼續進行剩餘的步驟。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-142">Do not continue with the remaining steps until both subscriptions are registered for the preview.</span></span>
 
1. <span data-ttu-id="e8a8f-143">以 UserA 身分登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-143">Log in to the [Azure portal](https://portal.azure.com) as UserA.</span></span> <span data-ttu-id="e8a8f-144">您登入時使用的帳戶必須擁有必要的權限，才能建立虛擬網路對等互連。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-144">The account you log in with must have the necessary permissions to create a virtual network peering.</span></span> <span data-ttu-id="e8a8f-145">如需詳細資訊，請參閱本文的[權限](#permissions)一節。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-145">See the [Permissions](#permissions) section of this article for details.</span></span>
2. <span data-ttu-id="e8a8f-146">依序按一下 [新增]、[網路] 及 [虛擬網路]。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-146">Click **+ New**, click **Networking**, then click **Virtual network**.</span></span>
3. <span data-ttu-id="e8a8f-147">在 [建立虛擬網路] 刀鋒視窗上，輸入或選取下列設定的值，然後按一下 [建立]：</span><span class="sxs-lookup"><span data-stu-id="e8a8f-147">In the **Create virtual network** blade, enter, or select values for the following settings, then click **Create**:</span></span>
    - <span data-ttu-id="e8a8f-148">**名稱**：*myVnetA*</span><span class="sxs-lookup"><span data-stu-id="e8a8f-148">**Name**: *myVnetA*</span></span>
    - <span data-ttu-id="e8a8f-149">**位址空間**：*10.0.0.0/16*</span><span class="sxs-lookup"><span data-stu-id="e8a8f-149">**Address space**: *10.0.0.0/16*</span></span>
    - <span data-ttu-id="e8a8f-150">**子網路名稱**：*預設值*</span><span class="sxs-lookup"><span data-stu-id="e8a8f-150">**Subnet name**: *default*</span></span>
    - <span data-ttu-id="e8a8f-151">**子網路位址範圍**：*10.0.0.0/24*</span><span class="sxs-lookup"><span data-stu-id="e8a8f-151">**Subnet address range**: *10.0.0.0/24*</span></span>
    - <span data-ttu-id="e8a8f-152">**訂用帳戶**︰選取訂用帳戶 A。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-152">**Subscription**: Select subscription A.</span></span>
    - <span data-ttu-id="e8a8f-153">**資源群組**：選取 [建立新項目]，然後輸入 *myResourceGroupA*</span><span class="sxs-lookup"><span data-stu-id="e8a8f-153">**Resource group**: Select **Create new** and enter *myResourceGroupA*</span></span>
    - <span data-ttu-id="e8a8f-154">**位置**：*美國東部*</span><span class="sxs-lookup"><span data-stu-id="e8a8f-154">**Location**: *East US*</span></span>
4. <span data-ttu-id="e8a8f-155">在入口網站頂端的 [搜尋資源] 方塊中，輸入 *myVnetA*。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-155">In the **Search resources** box at the top of the portal, type *myVnetA*.</span></span> <span data-ttu-id="e8a8f-156">當 myVnetA 出現在搜尋結果中時，按一下 [myVnetA]。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-156">Click **myVnetA** when it appears in the search results.</span></span> <span data-ttu-id="e8a8f-157">隨即會顯示 [myVnetA] 虛擬網路刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-157">A blade appears for the **myVnetA** virtual network.</span></span>
5. <span data-ttu-id="e8a8f-158">在顯示的 [myVnetA] 刀鋒視窗中，從刀鋒視窗左側的垂直選項清單中按一下 [存取控制 (IAM)]。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-158">In the **myVnetA** blade that appears, click **Access control (IAM)** from the vertical list of options on the left side of the blade.</span></span>
6. <span data-ttu-id="e8a8f-159">在顯示的 [myVnetA - 存取控制 (IAM)] 刀鋒視窗中，按一下 [+ 新增]。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-159">In the **myVnetA - Access control (IAM)** blade that appears, click **+ Add**.</span></span>
7. <span data-ttu-id="e8a8f-160">在顯示的 [新增權限] 刀鋒視窗中，選取 [角色] 方塊中的 [網路參與者]。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-160">In the **Add permissions** blade that appears, select **Network contributor** in the **Role** box.</span></span>
8. <span data-ttu-id="e8a8f-161">在 [選取] 方塊中，選取 [UserB]，或輸入 UserB 的電子郵件地址來搜尋它。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-161">In the **Select** box, select UserB, or type UserB's email address to search for it.</span></span> <span data-ttu-id="e8a8f-162">顯示的使用者清單來自與您設定對等互連之虛擬網路相同的 Azure Active Directory 租用戶。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-162">The list of users shown is from the same Azure Active Directory tenant as the virtual network you're setting up the peering for.</span></span> <span data-ttu-id="e8a8f-163">當 UserB 出現在清單中時，按一下 [UserB]。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-163">Click UserB when it appears in the list.</span></span>
9. <span data-ttu-id="e8a8f-164">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-164">Click **Save**.</span></span>
10. <span data-ttu-id="e8a8f-165">以 UserA 身分登出入口網站，然後以 UserB 身分登入。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-165">Log out of the portal as UserA, then log in as UserB.</span></span>
11. <span data-ttu-id="e8a8f-166">按一下 [+ 新增]，在 [搜尋 Marketplace] 方塊中輸入*虛擬網路*，然後按一下搜尋結果中的 [虛擬網路]。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-166">Click **+ New**, type *Virtual network* in the **Search the Marketplace** box, then click **Virtual network** in the search results.</span></span>
12. <span data-ttu-id="e8a8f-167">在出現的 [虛擬網路] 刀鋒視窗中，於 [選取部署模型] 方塊中選取 [傳統]，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-167">In the **Virtual Network** blade that appears, select **Classic** in the **Select a deployment model** box, then click **Create**.</span></span>
13.   <span data-ttu-id="e8a8f-168">在顯示的 [建立虛擬網路 (傳統)] 方塊中，輸入下列值：</span><span class="sxs-lookup"><span data-stu-id="e8a8f-168">In the Create virtual network (classic) box that appears, enter the following values:</span></span>

    - <span data-ttu-id="e8a8f-169">**名稱**：*myVnetB*</span><span class="sxs-lookup"><span data-stu-id="e8a8f-169">**Name**: *myVnetB*</span></span>
    - <span data-ttu-id="e8a8f-170">**位址空間**：*10.1.0.0/16*</span><span class="sxs-lookup"><span data-stu-id="e8a8f-170">**Address space**: *10.1.0.0/16*</span></span>
    - <span data-ttu-id="e8a8f-171">**子網路名稱**：*預設值*</span><span class="sxs-lookup"><span data-stu-id="e8a8f-171">**Subnet name**: *default*</span></span>
    - <span data-ttu-id="e8a8f-172">**子網路位址範圍**：*10.1.0.0/24*</span><span class="sxs-lookup"><span data-stu-id="e8a8f-172">**Subnet address range**: *10.1.0.0/24*</span></span>
    - <span data-ttu-id="e8a8f-173">**訂用帳戶**︰選取訂用帳戶 B。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-173">**Subscription**: Select subscription B.</span></span>
    - <span data-ttu-id="e8a8f-174">**資源群組**：選取 [建立新項目]，然後輸入 *myResourceGroupB*</span><span class="sxs-lookup"><span data-stu-id="e8a8f-174">**Resource group**: Select **Create new** and enter *myResourceGroupB*</span></span>
    - <span data-ttu-id="e8a8f-175">**位置**：*美國東部*</span><span class="sxs-lookup"><span data-stu-id="e8a8f-175">**Location**: *East US*</span></span>

14. <span data-ttu-id="e8a8f-176">在入口網站頂端的 [搜尋資源] 方塊中，輸入 *myVnetB*。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-176">In the **Search resources** box at the top of the portal, type *myVnetB*.</span></span> <span data-ttu-id="e8a8f-177">當 myVnetB 出現在搜尋結果中時，按一下 [myVnetB]。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-177">Click **myVnetB** when it appears in the search results.</span></span> <span data-ttu-id="e8a8f-178">隨即會顯示 [myVnetB] 虛擬網路刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-178">A blade appears for the **myVnetB** virtual network.</span></span>
15. <span data-ttu-id="e8a8f-179">在顯示的 [myVnetB] 刀鋒視窗中，從刀鋒視窗左側的垂直選項清單中按一下 [屬性]。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-179">In the **myVnetB** blade that appears, click **Properties** from the vertical list of options on the left side of the blade.</span></span> <span data-ttu-id="e8a8f-180">複製 [資源識別碼]，在稍後的步驟中將會用到此識別碼。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-180">Copy the **RESOURCE ID**, which is used in a later step.</span></span> <span data-ttu-id="e8a8f-181">資源識別碼與以下範例類似：/subscriptions/<Susbscription ID>/resourceGroups/myResoureGroupB/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB</span><span class="sxs-lookup"><span data-stu-id="e8a8f-181">The resource ID is similar to the following example: /subscriptions/<Susbscription ID>/resourceGroups/myResoureGroupB/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB</span></span>
16. <span data-ttu-id="e8a8f-182">針對 myVnetB 完成步驟 5-9，其中在步驟 8 輸入 **UserA**。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-182">Complete steps 5-9 for myVnetB, entering **UserA** in step 8.</span></span>
17. <span data-ttu-id="e8a8f-183">以 UserB 身分登出入口網站，然後以 UserA 身分登入。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-183">Log out of the portal as UserB and log in as UserA.</span></span>
18. <span data-ttu-id="e8a8f-184">在入口網站頂端的 [搜尋資源] 方塊中，輸入 *myVnetA*。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-184">In the **Search resources** box at the top of the portal, type *myVnetA*.</span></span> <span data-ttu-id="e8a8f-185">當 myVnetA 出現在搜尋結果中時，按一下 [myVnetA]。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-185">Click **myVnetA** when it appears in the search results.</span></span> <span data-ttu-id="e8a8f-186">隨即會顯示 [myVnet] 虛擬網路刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-186">A blade appears for the **myVnet** virtual network.</span></span>
19. <span data-ttu-id="e8a8f-187">按一下 [myVnetA]。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-187">Click **myVnetA**.</span></span>
20. <span data-ttu-id="e8a8f-188">在顯示的 [myVnetA] 刀鋒視窗中，從刀鋒視窗左側的垂直選項清單中按一下 [對等]。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-188">In the **myVnetA** blade that appears, click **Peerings** from the vertical list of options on the left side of the blade.</span></span>
21. <span data-ttu-id="e8a8f-189">在顯示的 [myVnetA - 對等互連] 刀鋒視窗中，按一下 [+ 新增]</span><span class="sxs-lookup"><span data-stu-id="e8a8f-189">In the **myVnetA - Peerings** blade that appeared, click **+ Add**</span></span>
22. <span data-ttu-id="e8a8f-190">在顯示的 [新增對等互連] 刀鋒視窗中，輸入或選取下列選項，然後按一下 [確定]：</span><span class="sxs-lookup"><span data-stu-id="e8a8f-190">In the **Add peering** blade that appears, enter, or select the following options, then click **OK**:</span></span>
     - <span data-ttu-id="e8a8f-191">**名稱**：*myVnetAToMyVnetB*</span><span class="sxs-lookup"><span data-stu-id="e8a8f-191">**Name**: *myVnetAToMyVnetB*</span></span>
     - <span data-ttu-id="e8a8f-192">**虛擬網路部署模型**︰選取 [傳統]。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-192">**Virtual network deployment model**:  Select **Classic**.</span></span>
     - <span data-ttu-id="e8a8f-193">**我知道我的資源識別碼**：核取此方塊。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-193">**I know my resource ID**: Check this box.</span></span>
     - <span data-ttu-id="e8a8f-194">**資源識別碼**： 輸入來自步驟 15 的 myVnetB 資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-194">**Resource ID**: Enter the resource ID of myVnetB from step 15.</span></span>
     - <span data-ttu-id="e8a8f-195">**允許虛擬網路存取**：確定已選取 [啟用]。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-195">**Allow virtual network access:** Ensure that **Enabled** is selected.</span></span>
    <span data-ttu-id="e8a8f-196">本教學課程中不會使用其他設定。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-196">No other settings are used in this tutorial.</span></span> <span data-ttu-id="e8a8f-197">若要了解所有對等互連設定，請閱讀[管理虛擬網路對等互連](virtual-network-manage-peering.md#create-a-peering)。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-197">To learn about all peering settings, read [Manage virtual network peerings](virtual-network-manage-peering.md#create-a-peering).</span></span>
23. <span data-ttu-id="e8a8f-198">在上一個步驟中按一下 [確定] 之後，[新增對等互連] 刀鋒視窗隨就會關閉，而您則會再次看到 [myVnetA - 對等] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-198">After clicking **OK** in the previous step, the **Add peering** blade closes and you see the **myVnetA - Peerings** blade again.</span></span> <span data-ttu-id="e8a8f-199">幾秒之後，您建立的對等互連會出現在刀鋒視窗中。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-199">After a few seconds, the peering you created appears in the blade.</span></span> <span data-ttu-id="e8a8f-200">您所建立之 **myVnetAToMyVnetB** 對等互連的 [對等互連狀態] 資料行中會列出 [已連接]。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-200">**Connected** is listed in the **PEERING STATUS** column for the **myVnetAToMyVnetB** peering you created.</span></span> <span data-ttu-id="e8a8f-201">現在已建立對等互連。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-201">The peering is now established.</span></span> <span data-ttu-id="e8a8f-202">沒有必要將虛擬網路 (傳統) 對等互連到虛擬網路 (Resource Manager)。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-202">There is no need to peer the virtual network (classic) to the virtual network (Resource Manager).</span></span>

    <span data-ttu-id="e8a8f-203">您在任何一個虛擬網路中建立的任何 Azure 資源現在能夠透過其 IP 位址彼此通訊。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-203">Any Azure resources you create in either virtual network are now able to communicate with each other through their IP addresses.</span></span> <span data-ttu-id="e8a8f-204">如果您使用虛擬網路的預設 Azure 名稱解析，則虛擬網路中的資源無法跨虛擬網路解析名稱。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-204">If you're using default Azure name resolution for the virtual networks, the resources in the virtual networks are not able to resolve names across the virtual networks.</span></span> <span data-ttu-id="e8a8f-205">如果您想要跨對等互連中的虛擬網路解析名稱，您必須建立自己的 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-205">If you want to resolve names across virtual networks in a peering, you must create your own DNS server.</span></span> <span data-ttu-id="e8a8f-206">了解如何設定[使用自己的 DNS 伺服器進行名稱解析](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server)。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-206">Learn how to set up [Name resolution using your own DNS server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span></span>

24. <span data-ttu-id="e8a8f-207">**選擇性**：雖然本教學課程未涵蓋建立虛擬機器，但您可以在每個虛擬網路中建立一部虛擬機器，並從一部虛擬機器連線至另一部來驗證連線。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-207">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine to the other, to validate connectivity.</span></span>
25. <span data-ttu-id="e8a8f-208">**選擇性︰**若要刪除您在本教學課程中建立的資源，請完成本文之[刪除資源](#delete-portal)一節中的步驟。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-208">**Optional**: To delete the resources that you create in this tutorial, complete the steps in the [Delete resources](#delete-portal) section of this article.</span></span>

## <span data-ttu-id="e8a8f-209"><a name="cli"></a>建立對等互連 - Azure CLI</span><span class="sxs-lookup"><span data-stu-id="e8a8f-209"><a name="cli"></a>Create peering - Azure CLI</span></span>

<span data-ttu-id="e8a8f-210">本教學課程針對每個訂用帳戶使用不同的帳戶。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-210">This tutorial uses different accounts for each subscription.</span></span> <span data-ttu-id="e8a8f-211">如果您使用對兩個訂用帳戶都有權限的帳戶，便可以使用該相同帳戶來進行所有步驟、略過登出 Azure 的步驟，以及移除建立使用者角色指派項目的指令碼行。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-211">If you're using an account that has permissions to both subscriptions, you can use the same account for all steps, skip the steps for logging out of Azure, and remove the lines of script that create user role assignments.</span></span> <span data-ttu-id="e8a8f-212">請使用您要用於 UserA 和 UserB 的使用者名稱來取代下列指令碼中的 UserA@azure.com 和 UserB@azure.com。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-212">Replace UserA@azure.com and UserB@azure.com in all of the following scripts with the usernames you're using for UserA and UserB.</span></span> 

<span data-ttu-id="e8a8f-213">在完成下列任何步驟之前，您必須先註冊預覽版。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-213">Before completing any of the following steps, you must register for the preview.</span></span> <span data-ttu-id="e8a8f-214">若要註冊，請完成本文中[註冊預覽版](#register)一節中的步驟。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-214">To register, complete the steps in the [Register for the preview](#register) section of this article.</span></span> <span data-ttu-id="e8a8f-215">請等到兩個訂用帳戶都已針對預覽版註冊之後，才繼續進行剩餘的步驟。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-215">Do not continue with the remaining steps until both subscriptions are registered for the preview.</span></span>

1. <span data-ttu-id="e8a8f-216">[安裝](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) Azure CLI 1.0 以建立虛擬網路 (傳統)。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-216">[Install](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) the Azure CLI 1.0 to create the virtual network (classic).</span></span>
2. <span data-ttu-id="e8a8f-217">開啟 CLI 工作階段，然後使用 `azure login` 命令來以 UserB 身分登入 Azure。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-217">Open a CLI session and log in to Azure as UserB using the `azure login` command.</span></span>
3. <span data-ttu-id="e8a8f-218">輸入 `azure config mode asm` 命令來以「服務管理」模式執行 CLI。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-218">Run the CLI in Service Management mode by entering the `azure config mode asm` command.</span></span>
4. <span data-ttu-id="e8a8f-219">輸入下列命令來建立虛擬網路 (傳統)：</span><span class="sxs-lookup"><span data-stu-id="e8a8f-219">Enter the following command to create the virtual network (classic):</span></span>
 
    ```azurecli
    azure network vnet create --vnet myVnetB --address-space 10.1.0.0 --cidr 16 --location "East US"
    ```
5. <span data-ttu-id="e8a8f-220">完成剩餘步驟的方式是必須使用 Bash 殼層並搭配[安裝](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json) Azure CLI 2.0.4 或更新版本，或是使用 Azure Cloud Shell。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-220">The remaining steps must be completed using a bash shell with the Azure CLI 2.0.4 or later [installed](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json), or by using the Azure Cloud Shell.</span></span> <span data-ttu-id="e8a8f-221">Azure Cloud Shell 是免費的 Bash Shell，您可以直接在 Azure 入口網站內執行。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-221">The Azure Cloud Shell is a free Bash shell that you can run directly within the Azure portal.</span></span> <span data-ttu-id="e8a8f-222">它具有預先安裝和設定的 Azure CLI，可與您的帳戶搭配使用。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-222">It has the Azure CLI preinstalled and configured to use with your account.</span></span> <span data-ttu-id="e8a8f-223">按一下以下指令碼中的 [試試看] 按鈕，這會開啟可讓您登入 Azure 帳戶的 Cloud Shell。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-223">Click the **Try it** button in the scripts that follow, which opens a Cloud Shell that logs you in to your Azure account.</span></span> <span data-ttu-id="e8a8f-224">如需在 Windows 用戶端上執行 Bash CLI 指令碼的選項，請參閱[在 Windows 中執行 Azure CLI](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-224">For options on running bash CLI scripts on a Windows client, see [Running the Azure CLI in Windows](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> 
6. <span data-ttu-id="e8a8f-225">將下列指令碼複製到您電腦上的文字編輯器中。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-225">Copy the following script to a text editor on your PC.</span></span> <span data-ttu-id="e8a8f-226">使用您的訂用帳戶 ID 來取代 `<SubscriptionB-Id>` 。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-226">Replace `<SubscriptionB-Id>` with your subscription ID.</span></span> <span data-ttu-id="e8a8f-227">如果您不知道您的訂用帳戶 ID，請輸入 `az account show` 命令。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-227">If you don't know your subscription Id, enter the `az account show` command.</span></span> <span data-ttu-id="e8a8f-228">輸出中的 **id** 值就是您的訂用帳戶 ID。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-228">The value for **id** in the output is your subscription Id.</span></span> <span data-ttu-id="e8a8f-229">請複製修改過的指令碼並貼到您的 CLI 2.0 工作階段中，然後按 `Enter`。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-229">Copy the modified script, paste it in to your CLI 2.0 session, and then press `Enter`.</span></span> 

    ```azurecli-interactive
    az role assignment create \
      --assignee UserA@azure.com \
      --role "Classic Network Contributor" \
      --scope /subscriptions/<SubscriptionB-Id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB
    ```

    <span data-ttu-id="e8a8f-230">當您在步驟 4 中建立虛擬網路 (傳統) 時，Azure 是在 *Default-Networking* 資源群組中建立該虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-230">When you created the virtual network (classic) in step 4, Azure created the virtual network in the *Default-Networking* resource group.</span></span>
7. <span data-ttu-id="e8a8f-231">將 UserB 登出 Azure，然後在 CLI 2.0 中以 UserA 身分登入。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-231">Log UserB out of Azure and log in as UserA in the CLI 2.0.</span></span>
8. <span data-ttu-id="e8a8f-232">建立資源群組和虛擬網路 (Resource Manager)。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-232">Create a resource group and a virtual network (Resource Manager).</span></span> <span data-ttu-id="e8a8f-233">請複製下列指令碼並貼到您的 CLI 工作階段中，然後按 `Enter`。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-233">Copy the following script, paste it in to your CLI session, and then press `Enter`.</span></span> 

    ```azurecli-interactive
    #!/bin/bash

    # Variables for common values used throughout the script.
    rgName="myResourceGroupA"
    location="eastus"

    # Create a resource group.
    az group create \
      --name $rgName \
      --location $location

    # Create virtual network A (Resource Manager).
    az network vnet create \
      --name myVnetA \
      --resource-group $rgName \
      --location $location \
      --address-prefix 10.0.0.0/16

    # Get the id for myVnetA.
    vNetAId=$(az network vnet show \
      --resource-group $rgName \
      --name myVnetA \
      --query id --out tsv)

    # Assign UserB permissions to myVnetA.
    az role assignment create \
      --assignee UserB@azure.com \
      --role "Network Contributor" \
      --scope $vNetAId
    ```

9. <span data-ttu-id="e8a8f-234">在透過不同部署模型建立的兩個虛擬網路之間，建立虛擬網路對等互連。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-234">Create a virtual network peering between the two virtual networks created through the different deployment models.</span></span> <span data-ttu-id="e8a8f-235">將下列指令碼複製到您電腦上的文字編輯器中。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-235">Copy the following script to a text editor on your PC.</span></span> <span data-ttu-id="e8a8f-236">使用您的訂用帳戶 ID 來取代 `<SubscriptionB-id>` 。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-236">Replace `<SubscriptionB-id>` with your subscription Id.</span></span> <span data-ttu-id="e8a8f-237">如果您不知道您的訂用帳戶 ID，請輸入 `az account show` 命令。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-237">If you don't know your subscription Id, enter the `az account show` command.</span></span> <span data-ttu-id="e8a8f-238">輸出中的 **id** 值就是您的訂用帳戶 ID。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-238">The value for **id** in the output is your subscription Id.</span></span> <span data-ttu-id="e8a8f-239">Azure 已將您在步驟 4 中建立的虛擬網路 (傳統) 建立在名為 *Default-Networking* 的資源群組中。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-239">Azure created the virtual network (classic) you created in step 4 in a resource group named *Default-Networking*.</span></span> <span data-ttu-id="e8a8f-240">請將修改過的指令碼貼到您的 CLI 工作階段中，然後按 `Enter`。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-240">Paste the modified script in your CLI session, and then press `Enter`.</span></span>

    ```azurecli-interactive
    # Peer VNet1 to VNet2.
    az network vnet peering create \
      --name myVnetAToMyVnetB \
      --resource-group $rgName \
      --vnet-name myVnetA \
      --remote-vnet-id  /subscriptions/<SubscriptionB-id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB \
      --allow-vnet-access
    ```

10. <span data-ttu-id="e8a8f-241">在指令碼執行之後，檢閱虛擬網路 (Resource Manager) 的對等互連。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-241">After the script executes, review the peering for the virtual network (Resource Manager).</span></span> <span data-ttu-id="e8a8f-242">請複製下列指令碼，然後將它貼到您的 CLI 工作階段中：</span><span class="sxs-lookup"><span data-stu-id="e8a8f-242">Copy the following script, and then paste it in your CLI session:</span></span>

    ```azurecli-interactive
    az network vnet peering list \
      --resource-group $rgName \
      --vnet-name myVnetA \
      --output table
    ```
    <span data-ttu-id="e8a8f-243">輸出會在 **PeeringState** 資料行中顯示 **Connected**。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-243">The output shows **Connected** in the **PeeringState** column.</span></span>

    <span data-ttu-id="e8a8f-244">您在任何一個虛擬網路中建立的任何 Azure 資源現在能夠透過其 IP 位址彼此通訊。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-244">Any Azure resources you create in either virtual network are now able to communicate with each other through their IP addresses.</span></span> <span data-ttu-id="e8a8f-245">如果您使用虛擬網路的預設 Azure 名稱解析，則虛擬網路中的資源無法跨虛擬網路解析名稱。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-245">If you're using default Azure name resolution for the virtual networks, the resources in the virtual networks are not able to resolve names across the virtual networks.</span></span> <span data-ttu-id="e8a8f-246">如果您想要跨對等互連中的虛擬網路解析名稱，您必須建立自己的 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-246">If you want to resolve names across virtual networks in a peering, you must create your own DNS server.</span></span> <span data-ttu-id="e8a8f-247">了解如何設定[使用自己的 DNS 伺服器進行名稱解析](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server)。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-247">Learn how to set up [Name resolution using your own DNS server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span></span>

11. <span data-ttu-id="e8a8f-248">**選擇性**：雖然本教學課程未涵蓋建立虛擬機器，但您可以在每個虛擬網路中建立一部虛擬機器，並從一部虛擬機器連線至另一部來驗證連線。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-248">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine to the other, to validate connectivity.</span></span>
12. <span data-ttu-id="e8a8f-249">**選擇性︰**若要刪除您在本教學課程中所建立的資源，請完成本文之[刪除資源](#delete-cli)中的步驟。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-249">**Optional**: To delete the resources that you create in this tutorial, complete the steps in [Delete resources](#delete-cli) in this article.</span></span>

## <span data-ttu-id="e8a8f-250"><a name="powershell"></a>建立對等互連 - PowerShell</span><span class="sxs-lookup"><span data-stu-id="e8a8f-250"><a name="powershell"></a>Create peering - PowerShell</span></span>

<span data-ttu-id="e8a8f-251">本教學課程針對每個訂用帳戶使用不同的帳戶。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-251">This tutorial uses different accounts for each subscription.</span></span> <span data-ttu-id="e8a8f-252">如果您使用對兩個訂用帳戶都有權限的帳戶，便可以使用該相同帳戶來進行所有步驟、略過登出 Azure 的步驟，以及移除建立使用者角色指派項目的指令碼行。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-252">If you're using an account that has permissions to both subscriptions, you can use the same account for all steps, skip the steps for logging out of Azure, and remove the lines of script that create user role assignments.</span></span> <span data-ttu-id="e8a8f-253">請使用您要用於 UserA 和 UserB 的使用者名稱來取代下列指令碼中的 UserA@azure.com 和 UserB@azure.com。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-253">Replace UserA@azure.com and UserB@azure.com in all of the following scripts with the usernames you're using for UserA and UserB.</span></span> 

<span data-ttu-id="e8a8f-254">在完成下列任何步驟之前，您必須先註冊預覽版。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-254">Before completing any of the following steps, you must register for the preview.</span></span> <span data-ttu-id="e8a8f-255">若要註冊，請完成本文中[註冊預覽版](#register)一節中的步驟。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-255">To register, complete the steps in the [Register for the preview](#register) section of this article.</span></span> <span data-ttu-id="e8a8f-256">請等到兩個訂用帳戶都已針對預覽版註冊之後，才繼續進行剩餘的步驟。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-256">Do not continue with the remaining steps until both subscriptions are registered for the preview.</span></span>

1. <span data-ttu-id="e8a8f-257">安裝最新版的 PowerShell [Azure](https://www.powershellgallery.com/packages/Azure) 和 [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) 模組。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-257">Install the latest version of the PowerShell [Azure](https://www.powershellgallery.com/packages/Azure) and [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) modules.</span></span> <span data-ttu-id="e8a8f-258">如果您不熟悉 Azure PowerShell，請參閱 [Azure PowerShell 概觀](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-258">If you're new to Azure PowerShell, see [Azure PowerShell overview](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="e8a8f-259">啟動 PowerShell 工作階段。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-259">Start a PowerShell session.</span></span>
3. <span data-ttu-id="e8a8f-260">在 PowerShell 中，輸入 `Add-AzureAccount` 命令來以 UserB 身分登入 UserB 的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-260">In PowerShell, log in to UserB's subscription as UserB by entering the `Add-AzureAccount` command.</span></span>
4. <span data-ttu-id="e8a8f-261">若要使用 PowerShell 來建立虛擬網路 (傳統)，您必須建立一個新的或修改現有的網路組態檔。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-261">To create a virtual network (classic) with PowerShell, you must create a new, or modify an existing, network configuration file.</span></span> <span data-ttu-id="e8a8f-262">了解如何[匯出、更新及匯入網路組態檔](virtual-networks-using-network-configuration-file.md)。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-262">Learn how to [export, update, and import network configuration files](virtual-networks-using-network-configuration-file.md).</span></span> <span data-ttu-id="e8a8f-263">就本教學課程中使用的虛擬網路而言，此檔案應該包含下列 **VirtualNetworkSite** 元素：</span><span class="sxs-lookup"><span data-stu-id="e8a8f-263">The file should include the following **VirtualNetworkSite** element for the virtual network used in this tutorial:</span></span>

    ```xml
    <VirtualNetworkSite name="myVnetB" Location="East US">
      <AddressSpace>
        <AddressPrefix>10.1.0.0/16</AddressPrefix>
      </AddressSpace>
      <Subnets>
        <Subnet name="default">
          <AddressPrefix>10.1.0.0/24</AddressPrefix>
        </Subnet>
      </Subnets>
    </VirtualNetworkSite>
    ```

    > [!WARNING]
    > <span data-ttu-id="e8a8f-264">匯入變更過的網路組態檔會導致您訂用帳戶中現有的虛擬網路 (傳統) 發生變更。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-264">Importing a changed network configuration file can cause changes to existing virtual networks (classic) in your subscription.</span></span> <span data-ttu-id="e8a8f-265">請確定您只新增先前的虛擬網路，並且未變更或移除您訂用帳戶中任何現有的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-265">Ensure you only add the previous virtual network and that you don't change or remove any existing virtual networks from your subscription.</span></span> 

5. <span data-ttu-id="e8a8f-266">輸入 `login-azurermaccount` 命令來以 UserB 身分登入 UserB 的訂用帳戶，以使用 Resource Manager 命令。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-266">Log in to UserB's subscription as UserB to use Resource Manager commands by entering the `login-azurermaccount` command.</span></span>
6. <span data-ttu-id="e8a8f-267">將 UserA 權限指派給虛擬網路 B。將下列指令碼複製到您電腦上的文字編輯器中，並使用訂用帳戶 B 的 ID 來取代 `<SubscriptionB-id>`。如果您不知道訂用帳戶 ID，請輸入 `Get-AzureRmSubscription` 命令來檢視它。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-267">Assign UserA permissions to virtual network B. Copy the following script to a text editor on your PC and replace `<SubscriptionB-id>` with the ID of subscription B. If you don't know the subscription Id, enter the `Get-AzureRmSubscription` command to view it.</span></span> <span data-ttu-id="e8a8f-268">傳回之輸出中的 **Id** 值就是您的訂用帳戶 ID。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-268">The value for **Id** in the returned output is your subscription ID.</span></span> <span data-ttu-id="e8a8f-269">Azure 已將您在步驟 4 中建立的虛擬網路 (傳統) 建立在名為 *Default-Networking* 的資源群組中。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-269">Azure created the virtual network (classic) you created in step 4 in a resource group named *Default-Networking*.</span></span> <span data-ttu-id="e8a8f-270">若要執行指令碼，請複製修改過的指令碼並貼到 PowerShell 中，然後按 `Enter`。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-270">To execute the script, copy the modified script, paste it in to PowerShell, and then press `Enter`.</span></span>
    
    ```powershell 
    New-AzureRmRoleAssignment `
      -SignInName UserA@azure.com `
      -RoleDefinitionName "Classic Network Contributor" `
      -Scope /subscriptions/<SubscriptionB-id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB
    ```

7. <span data-ttu-id="e8a8f-271">以 UserB 身分登出 Azure，然後輸入 `login-azurermaccount` 命令來以 UserA 身分登入 UserA 的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-271">Log out of Azure as UserB and log in to UserA's subscription as UserA by entering the `login-azurermaccount` command.</span></span> <span data-ttu-id="e8a8f-272">您登入時使用的帳戶必須擁有必要的權限，才能建立虛擬網路對等互連。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-272">The account you log in with must have the necessary permissions to create a virtual network peering.</span></span> <span data-ttu-id="e8a8f-273">如需詳細資訊，請參閱本文的[權限](#permissions)一節。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-273">See the [Permissions](#permissions) section of this article for details.</span></span>
8. <span data-ttu-id="e8a8f-274">複製下列指令碼並貼到 PowerShell 中，然後按 `Enter`，以建立虛擬網路 (Resource Manager)：</span><span class="sxs-lookup"><span data-stu-id="e8a8f-274">Create the virtual network (Resource Manager) by copying the following script, pasting it in to PowerShell, and then pressing `Enter`:</span></span>

    ```powershell
    # Variables for common values
      $rgName='MyResourceGroupA'
      $location='eastus'

    # Create a resource group.
    New-AzureRmResourceGroup `
      -Name $rgName `
      -Location $location

    # Create virtual network A.
    $vnetA = New-AzureRmVirtualNetwork `
      -ResourceGroupName $rgName `
      -Name 'myVnetA' `
      -AddressPrefix '10.0.0.0/16' `
      -Location $location
    ```

9. <span data-ttu-id="e8a8f-275">將 UserB 權限指派給 myVnetA。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-275">Assign UserB permissions to myVnetA.</span></span> <span data-ttu-id="e8a8f-276">將下列指令碼複製到您電腦上的文字編輯器中，並使用訂用帳戶 A 的 ID 來取代 `<SubscriptionA-Id>`。如果您不知道訂用帳戶 ID，請輸入 `Get-AzureRmSubscription` 命令來檢視它。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-276">Copy the following script to a text editor on your PC and replace `<SubscriptionA-Id>` with the ID of subscription A. If you don't know the subscription Id, enter the `Get-AzureRmSubscription` command to view it.</span></span> <span data-ttu-id="e8a8f-277">傳回之輸出中的 **Id** 值就是您的訂用帳戶 ID。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-277">The value for **Id** in the returned output is your subscription ID.</span></span> <span data-ttu-id="e8a8f-278">將修改過的指令碼版本貼到 PowerShell 中，然後按 `Enter` 來執行它。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-278">Paste the modified version of the script in PowerShell, and then press `Enter` to execute it.</span></span>

    ```powershell
    New-AzureRmRoleAssignment `
      -SignInName UserB@azure.com `
      -RoleDefinitionName "Network Contributor" `
      -Scope /subscriptions/<SubscriptionA-Id>/resourceGroups/myResourceGroupA/providers/Microsoft.Network/VirtualNetworks/myVnetA
    ```

10. <span data-ttu-id="e8a8f-279">將下列指令碼複製到您電腦上的文字編輯器中，並使用訂用帳戶 B 的 ID 來取代 `<SubscriptionB-id>`。若要將 myVnetA 對等互連到 myVNetB，請複製修改過的指令碼並貼到 PowerShell 中，然後按 `Enter`。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-279">Copy the following script to a text editor on your PC, and replace `<SubscriptionB-id>` with the ID of subscription B. To peer myVnetA to myVNetB, copy the modified script, paste it in to PowerShell, and then press `Enter`.</span></span>

    ```powershell
    Add-AzureRmVirtualNetworkPeering `
      -Name 'myVnetAToMyVnetB' `
      -VirtualNetwork $vnetA `
      -RemoteVirtualNetworkId /subscriptions/<SubscriptionB-id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB
    ```

11. <span data-ttu-id="e8a8f-280">複製下列指令碼並貼到 PowerShell 中，然後按 `Enter`，以檢視 myVnetA 的對等互連狀態。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-280">View the peering state of myVnetA by copying the following script, pasting it into PowerShell, and pressing `Enter`.</span></span>

    ```powershell
    Get-AzureRmVirtualNetworkPeering `
      -ResourceGroupName $rgName `
      -VirtualNetworkName myVnetA `
      | Format-Table VirtualNetworkName, PeeringState
    ```

    <span data-ttu-id="e8a8f-281">狀態為 **Connected**。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-281">The state is **Connected**.</span></span> <span data-ttu-id="e8a8f-282">在您設定從 myVnetB 到 myVnetA 的對等互連之後，它就會變更為 **Connected**。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-282">It changes to **Connected** once you setup the peering to myVnetA from myVnetB.</span></span>

    <span data-ttu-id="e8a8f-283">您在任何一個虛擬網路中建立的任何 Azure 資源現在能夠透過其 IP 位址彼此通訊。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-283">Any Azure resources you create in either virtual network are now able to communicate with each other through their IP addresses.</span></span> <span data-ttu-id="e8a8f-284">如果您使用虛擬網路的預設 Azure 名稱解析，則虛擬網路中的資源無法跨虛擬網路解析名稱。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-284">If you're using default Azure name resolution for the virtual networks, the resources in the virtual networks are not able to resolve names across the virtual networks.</span></span> <span data-ttu-id="e8a8f-285">如果您想要跨對等互連中的虛擬網路解析名稱，您必須建立自己的 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-285">If you want to resolve names across virtual networks in a peering, you must create your own DNS server.</span></span> <span data-ttu-id="e8a8f-286">了解如何設定[使用自己的 DNS 伺服器進行名稱解析](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server)。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-286">Learn how to set up [Name resolution using your own DNS server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span></span>

12. <span data-ttu-id="e8a8f-287">**選擇性**：雖然本教學課程未涵蓋建立虛擬機器，但您可以在每個虛擬網路中建立一部虛擬機器，並從一部虛擬機器連線至另一部來驗證連線。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-287">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine to the other, to validate connectivity.</span></span>
13. <span data-ttu-id="e8a8f-288">**選擇性︰**若要刪除您在本教學課程中所建立的資源，請完成本文之[刪除資源](#delete-powershell)中的步驟。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-288">**Optional**: To delete the resources that you create in this tutorial, complete the steps in [Delete resources](#delete-powershell) in this article.</span></span>

## <span data-ttu-id="e8a8f-289"><a name="permissions"></a>權限</span><span class="sxs-lookup"><span data-stu-id="e8a8f-289"><a name="permissions"></a>Permissions</span></span>

<span data-ttu-id="e8a8f-290">您用於建立虛擬網路對等互連的帳戶必須具有必要的角色或權限。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-290">The accounts you use to create a virtual network peering must have the necessary role or permissions.</span></span> <span data-ttu-id="e8a8f-291">例如，如果您是將名為 myVnetA 和 myVnetB 的兩個虛擬網路對等互連，您的帳戶就必須獲指派各個虛擬網路的下列最基本角色或權限：</span><span class="sxs-lookup"><span data-stu-id="e8a8f-291">For example, if you were peering two virtual networks named myVnetA and myVnetB, your account must be assigned the following minimum role or permissions for each virtual network:</span></span>
    
|<span data-ttu-id="e8a8f-292">虛擬網路</span><span class="sxs-lookup"><span data-stu-id="e8a8f-292">Virtual network</span></span>|<span data-ttu-id="e8a8f-293">部署模型</span><span class="sxs-lookup"><span data-stu-id="e8a8f-293">Deployment model</span></span>|<span data-ttu-id="e8a8f-294">角色</span><span class="sxs-lookup"><span data-stu-id="e8a8f-294">Role</span></span>|<span data-ttu-id="e8a8f-295">權限</span><span class="sxs-lookup"><span data-stu-id="e8a8f-295">Permissions</span></span>|
|---|---|---|---|
|<span data-ttu-id="e8a8f-296">myVnetA</span><span class="sxs-lookup"><span data-stu-id="e8a8f-296">myVnetA</span></span>|<span data-ttu-id="e8a8f-297">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e8a8f-297">Resource Manager</span></span>|[<span data-ttu-id="e8a8f-298">網路參與者</span><span class="sxs-lookup"><span data-stu-id="e8a8f-298">Network Contributor</span></span>](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|<span data-ttu-id="e8a8f-299">Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write</span><span class="sxs-lookup"><span data-stu-id="e8a8f-299">Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write</span></span>|
| |<span data-ttu-id="e8a8f-300">傳統</span><span class="sxs-lookup"><span data-stu-id="e8a8f-300">Classic</span></span>|[<span data-ttu-id="e8a8f-301">傳統網路參與者</span><span class="sxs-lookup"><span data-stu-id="e8a8f-301">Classic Network Contributor</span></span>](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|<span data-ttu-id="e8a8f-302">N/A</span><span class="sxs-lookup"><span data-stu-id="e8a8f-302">N/A</span></span>|
|<span data-ttu-id="e8a8f-303">myVnetB</span><span class="sxs-lookup"><span data-stu-id="e8a8f-303">myVnetB</span></span>|<span data-ttu-id="e8a8f-304">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e8a8f-304">Resource Manager</span></span>|[<span data-ttu-id="e8a8f-305">網路參與者</span><span class="sxs-lookup"><span data-stu-id="e8a8f-305">Network Contributor</span></span>](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|<span data-ttu-id="e8a8f-306">Microsoft.Network/virtualNetworks/peer</span><span class="sxs-lookup"><span data-stu-id="e8a8f-306">Microsoft.Network/virtualNetworks/peer</span></span>|
||<span data-ttu-id="e8a8f-307">傳統</span><span class="sxs-lookup"><span data-stu-id="e8a8f-307">Classic</span></span>|[<span data-ttu-id="e8a8f-308">傳統網路參與者</span><span class="sxs-lookup"><span data-stu-id="e8a8f-308">Classic Network Contributor</span></span>](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|<span data-ttu-id="e8a8f-309">Microsoft.ClassicNetwork/virtualNetworks/peer</span><span class="sxs-lookup"><span data-stu-id="e8a8f-309">Microsoft.ClassicNetwork/virtualNetworks/peer</span></span>|

<span data-ttu-id="e8a8f-310">深入了解[內建角色](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)以及如何對[自訂角色](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json)指派特定權限 (僅限 Resource Manager)。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-310">Learn more about [built-in roles](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) and assigning specific permissions to [custom roles](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (Resource Manager only).</span></span>

## <span data-ttu-id="e8a8f-311"><a name="delete"></a>刪除資源</span><span class="sxs-lookup"><span data-stu-id="e8a8f-311"><a name="delete"></a>Delete resources</span></span>
<span data-ttu-id="e8a8f-312">當您完成本教學課程時，您可能會想刪除您在教學課程中建立的資源，以免產生使用費。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-312">When you've finished this tutorial, you might want to delete the resources you created in the tutorial, so you don't incur usage charges.</span></span> <span data-ttu-id="e8a8f-313">刪除資源群組同時會刪除其內含的所有資源。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-313">Deleting a resource group also deletes all resources that are in the resource group.</span></span>

### <span data-ttu-id="e8a8f-314"><a name="delete-portal"></a>Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="e8a8f-314"><a name="delete-portal"></a>Azure portal</span></span>

1. <span data-ttu-id="e8a8f-315">在入口網站搜尋方塊中，輸入 **myResourceGroupA**。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-315">In the portal search box, enter **myResourceGroupA**.</span></span> <span data-ttu-id="e8a8f-316">在搜尋結果中，按一下 [myResourceGroupA]。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-316">In the search results, click **myResourceGroupA**.</span></span>
2. <span data-ttu-id="e8a8f-317">在 [myResourceGroupA] 刀鋒視窗中，按一下 [刪除] 圖示。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-317">On the **myResourceGroupA** blade, click the **Delete** icon.</span></span>
3. <span data-ttu-id="e8a8f-318">若要確認刪除，請在 [輸入資源群組名稱] 方塊中輸入 **myResourceGroupA**，然後按一下 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-318">To confirm the deletion, in the **TYPE THE RESOURCE GROUP NAME** box, enter **myResourceGroupA**, and then click **Delete**.</span></span>
4. <span data-ttu-id="e8a8f-319">在入口網站頂端的 [搜尋資源] 方塊中，輸入 *myVnetB*。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-319">In the **Search resources** box at the top of the portal, type *myVnetB*.</span></span> <span data-ttu-id="e8a8f-320">當 myVnetB 出現在搜尋結果中時，按一下 [myVnetB]。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-320">Click **myVnetB** when it appears in the search results.</span></span> <span data-ttu-id="e8a8f-321">隨即會顯示 [myVnetB] 虛擬網路刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-321">A blade appears for the **myVnetB** virtual network.</span></span>
5. <span data-ttu-id="e8a8f-322">在 [myVnetB] 刀鋒視窗中，按一下 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-322">In the **myVnetB** blade, click **Delete**.</span></span>
6. <span data-ttu-id="e8a8f-323">若要確認刪除，請在 [刪除虛擬網路] 方塊中，按一下 [是]。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-323">To confirm the deletion, click **Yes** in the **Delete virtual network** box.</span></span>

### <span data-ttu-id="e8a8f-324"><a name="delete-cli"></a>Azure CLI</span><span class="sxs-lookup"><span data-stu-id="e8a8f-324"><a name="delete-cli"></a>Azure CLI</span></span>

1. <span data-ttu-id="e8a8f-325">使用 CLI 2.0 來登入 Azure，以使用下列命令來刪除虛擬網路 (Resource Manager)：</span><span class="sxs-lookup"><span data-stu-id="e8a8f-325">Log in to Azure using the CLI 2.0 to delete the virtual network (Resource Manager) with the following command:</span></span>

    ```azurecli-interactive
    az group delete --name myResourceGroupA --yes
    ```

2. <span data-ttu-id="e8a8f-326">使用 Azure CLI 1.0 來登入 Azure，以使用下列命令來刪除虛擬網路 (傳統)：</span><span class="sxs-lookup"><span data-stu-id="e8a8f-326">Log in to Azure using the Azure CLI 1.0 to delete the virtual network (classic) with the following commands:</span></span>

    ```azurecli
    azure config mode asm 

    azure network vnet delete --vnet myVnetB --quiet
    ```

### <span data-ttu-id="e8a8f-327"><a name="delete-powershell"></a>PowerShell</span><span class="sxs-lookup"><span data-stu-id="e8a8f-327"><a name="delete-powershell"></a>PowerShell</span></span>

1. <span data-ttu-id="e8a8f-328">在 PowerShell 命令提示字元中，輸入下列命令來刪除虛擬網路 (Resource Manager)：</span><span class="sxs-lookup"><span data-stu-id="e8a8f-328">At the PowerShell command prompt, enter the following command to delete the virtual network (Resource Manager):</span></span>

    ```powershell
    Remove-AzureRmResourceGroup -Name myResourceGroupA -Force
    ```

2. <span data-ttu-id="e8a8f-329">若要使用 PowerShell 來刪除虛擬網路 (傳統)，您必須修改現有的網路組態檔。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-329">To delete the virtual network (classic) with PowerShell, you must modify an existing network configuration file.</span></span> <span data-ttu-id="e8a8f-330">了解如何[匯出、更新及匯入網路組態檔](virtual-networks-using-network-configuration-file.md)。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-330">Learn how to [export, update, and import network configuration files](virtual-networks-using-network-configuration-file.md).</span></span> <span data-ttu-id="e8a8f-331">針對本教學課程中使用的虛擬網路，請移除下列 VirtualNetworkSite 元素：</span><span class="sxs-lookup"><span data-stu-id="e8a8f-331">Remove the following VirtualNetworkSite element for the virtual network used in this tutorial:</span></span>

    ```xml
    <VirtualNetworkSite name="myVnetB" Location="East US">
      <AddressSpace>
        <AddressPrefix>10.1.0.0/16</AddressPrefix>
      </AddressSpace>
      <Subnets>
        <Subnet name="default">
          <AddressPrefix>10.1.0.0/24</AddressPrefix>
        </Subnet>
      </Subnets>
    </VirtualNetworkSite>
    ```

    > [!WARNING]
    > <span data-ttu-id="e8a8f-332">匯入變更過的網路組態檔會導致您訂用帳戶中現有的虛擬網路 (傳統) 發生變更。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-332">Importing a changed network configuration file can cause changes to existing virtual networks (classic) in your subscription.</span></span> <span data-ttu-id="e8a8f-333">請確定您只移除先前的虛擬網路，並且未變更或移除您訂用帳戶中任何其他現有的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-333">Ensure you only remove the previous virtual network and that you don't change or remove any other existing virtual networks from your subscription.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="e8a8f-334">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e8a8f-334">Next steps</span></span>

- <span data-ttu-id="e8a8f-335">請先徹底熟悉重要[虛擬網路對等互連的條件約束和行為](virtual-network-manage-peering.md#requirements-and-constraints)，再建立虛擬網路對等互連以供生產環境使用。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-335">Thoroughly familiarize yourself with important [virtual network peering constraints and behaviors](virtual-network-manage-peering.md#requirements-and-constraints) before creating a virtual network peering for production use.</span></span>
- <span data-ttu-id="e8a8f-336">了解所有[虛擬網路對等互連設定](virtual-network-manage-peering.md#create-a-peering)。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-336">Learn about all [virtual network peering settings](virtual-network-manage-peering.md#create-a-peering).</span></span>
- <span data-ttu-id="e8a8f-337">了解如何透過虛擬網路對等互連來[建立中樞和輪輻網路拓撲](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering)。</span><span class="sxs-lookup"><span data-stu-id="e8a8f-337">Learn how to [create a hub and spoke network topology](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) with virtual network peering.</span></span>