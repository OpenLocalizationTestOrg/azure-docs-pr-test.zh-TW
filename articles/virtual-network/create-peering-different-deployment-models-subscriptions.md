---
title: "Azure 虛擬網路對等互連-aaaCreate 不同的部署模型的不同訂用帳戶 |Microsoft 文件"
description: "了解如何 toocreate 虛擬網路對等互連虛擬網路之間建立透過存在於不同的 Azure 訂用帳戶中的不同的 Azure 部署模型。"
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
ms.openlocfilehash: 865bdabb5b87523ba943d7b5dcbdc2475b78bdb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-peering---different-deployment-models-and-subscriptions"></a><span data-ttu-id="92cc5-103">建立虛擬網路對等互連 - 不同部署模型和訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="92cc5-103">Create a virtual network peering - different deployment models and subscriptions</span></span>

<span data-ttu-id="92cc5-104">在此教學課程中，您學會 toocreate 對等互連是透過不同的部署模型建立的虛擬網路之間的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="92cc5-104">In this tutorial, you learn toocreate a virtual network peering between virtual networks created through different deployment models.</span></span> <span data-ttu-id="92cc5-105">hello 虛擬網路位於不同的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="92cc5-105">hello virtual networks exist in different subscriptions.</span></span> <span data-ttu-id="92cc5-106">在不同的虛擬網路 toocommunicate 彼此具有對等兩個虛擬網路可讓資源 hello 相同的頻寬和延遲好像 hello 資源是在 hello 相同虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="92cc5-106">Peering two virtual networks enables resources in different virtual networks toocommunicate with each other with hello same bandwidth and latency as though hello resources were in hello same virtual network.</span></span> <span data-ttu-id="92cc5-107">深入了解[虛擬網路對等互連](virtual-network-peering-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="92cc5-107">Learn more about [Virtual network peering](virtual-network-peering-overview.md).</span></span> 

<span data-ttu-id="92cc5-108">hello 步驟 toocreate 虛擬網路對等互連會有所不同，hello 虛擬網路是否有相同，或不同的 hello、 訂用帳戶及其中[Azure 部署模型](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json)建立 hello 虛擬網路透過。</span><span class="sxs-lookup"><span data-stu-id="92cc5-108">hello steps toocreate a virtual network peering are different, depending on whether hello virtual networks are in hello same, or different, subscriptions, and which [Azure deployment model](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) hello virtual networks are created through.</span></span> <span data-ttu-id="92cc5-109">了解 toocreate 的虛擬網路在其他情況下，即可從下表中的 hello hello 案例對等互連的方式：</span><span class="sxs-lookup"><span data-stu-id="92cc5-109">Learn how toocreate a virtual network peering in other scenarios by clicking hello scenario from hello following table:</span></span>

|<span data-ttu-id="92cc5-110">Azure 部署模型</span><span class="sxs-lookup"><span data-stu-id="92cc5-110">Azure deployment model</span></span>  | <span data-ttu-id="92cc5-111">Azure 訂閱</span><span class="sxs-lookup"><span data-stu-id="92cc5-111">Azure subscription</span></span>  |
|--------- |---------|
|[<span data-ttu-id="92cc5-112">兩者皆使用 Resource Manager</span><span class="sxs-lookup"><span data-stu-id="92cc5-112">Both Resource Manager</span></span>](virtual-network-create-peering.md) |<span data-ttu-id="92cc5-113">相同</span><span class="sxs-lookup"><span data-stu-id="92cc5-113">Same</span></span>|
|[<span data-ttu-id="92cc5-114">兩者皆使用 Resource Manager</span><span class="sxs-lookup"><span data-stu-id="92cc5-114">Both Resource Manager</span></span>](create-peering-different-subscriptions.md) |<span data-ttu-id="92cc5-115">不同</span><span class="sxs-lookup"><span data-stu-id="92cc5-115">Different</span></span>|
|[<span data-ttu-id="92cc5-116">一個使用 Resource Manager、一個使用傳統部署模型</span><span class="sxs-lookup"><span data-stu-id="92cc5-116">One Resource Manager, one classic</span></span>](create-peering-different-deployment-models.md) |<span data-ttu-id="92cc5-117">相同</span><span class="sxs-lookup"><span data-stu-id="92cc5-117">Same</span></span>|

<span data-ttu-id="92cc5-118">無法透過 hello 傳統部署模型所部署的兩個虛擬網路之間建立的虛擬網路對等互連。</span><span class="sxs-lookup"><span data-stu-id="92cc5-118">A virtual network peering cannot be created between two virtual networks deployed through hello classic deployment model.</span></span> <span data-ttu-id="92cc5-119">虛擬網路對等互連只能建立兩個存在於 hello 相同的虛擬網路之間的 Azure 區域。</span><span class="sxs-lookup"><span data-stu-id="92cc5-119">A virtual network peering can only be created between two virtual networks that exist in hello same Azure region.</span></span> <span data-ttu-id="92cc5-120">當建立對等互連存在不同的訂用帳戶，hello 兩者都必須是訂用帳戶中的虛擬網路之間的虛擬網路相關聯 toohello 相同 Azure Active Directory 租用戶。</span><span class="sxs-lookup"><span data-stu-id="92cc5-120">When creating a virtual network peering between virtual networks that exist in different subscriptions, hello subscriptions must both be associated toohello same Azure Active Directory tenant.</span></span> <span data-ttu-id="92cc5-121">如果您還沒有 Azure Active Directory 租用戶，可以快速地[建立一個租用戶](../active-directory/develop/active-directory-howto-tenant.md?toc=%2fazure%2fvirtual-network%2ftoc.json#start-from-scratch)。</span><span class="sxs-lookup"><span data-stu-id="92cc5-121">If you don't already have an Azure Active Directory tenant, you can quickly [create one](../active-directory/develop/active-directory-howto-tenant.md?toc=%2fazure%2fvirtual-network%2ftoc.json#start-from-scratch).</span></span> <span data-ttu-id="92cc5-122">如果您需要 tooconnect 虛擬網路同時建立透過 hello 傳統部署模型，或存在於不同的 Azure 地區，或存在於訂用帳戶相關聯 toodifferent Azure Active Directory 租用戶，您可以使用 Azure [VPN 閘道](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json)tooconnect hello 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="92cc5-122">If you need tooconnect virtual networks that were both created through hello classic deployment model, or that exist in different Azure regions, or that exist in subscriptions associated toodifferent Azure Active Directory tenants, you can use an Azure [VPN Gateway](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) tooconnect hello virtual networks.</span></span> 

> [!WARNING]
> <span data-ttu-id="92cc5-123">在透過不同 Azure 部署模型建立且存在於不同訂用帳戶中的虛擬網路之間建立虛擬網路對等互連，目前是預覽版功能。</span><span class="sxs-lookup"><span data-stu-id="92cc5-123">Creating a virtual network peering between virtual networks in created through different Azure deployment models that exist in different subscriptions is currently in preview.</span></span> <span data-ttu-id="92cc5-124">在此案例中建立的虛擬網路對等互連無權 hello 相同層級的可用性和可靠性，做為建立虛擬網路對等互連中案例一般可用性版本。</span><span class="sxs-lookup"><span data-stu-id="92cc5-124">Virtual network peerings created in this scenario may not have hello same level of availability and reliability as creating a virtual network peering in scenarios in general availability release.</span></span> <span data-ttu-id="92cc5-125">在此情況下建立的虛擬網路對等互連不受支援、可能功能受限，且可能並非在所有 Azure 區域中都可供使用。</span><span class="sxs-lookup"><span data-stu-id="92cc5-125">Virtual network peerings created in this scenario are not supported, may have constrained capabilities, and may not be available in all Azure regions.</span></span> <span data-ttu-id="92cc5-126">Hello 上這項功能的可用性與狀態的最新通知，請檢查 hello [Azure 虛擬網路更新](https://azure.microsoft.com/updates/?product=virtual-network)頁面。</span><span class="sxs-lookup"><span data-stu-id="92cc5-126">For hello most up-to-date notifications on availability and status of this feature, check hello [Azure Virtual Network updates](https://azure.microsoft.com/updates/?product=virtual-network) page.</span></span>

<span data-ttu-id="92cc5-127">您可以使用 hello [Azure 入口網站](#portal)，hello Azure[命令列介面](#cli)(CLI)，或 Azure [PowerShell](#powershell) toocreate 虛擬網路對等互連。</span><span class="sxs-lookup"><span data-stu-id="92cc5-127">You can use hello [Azure portal](#portal), hello Azure [command-line interface](#cli) (CLI), or Azure [PowerShell](#powershell) toocreate a virtual network peering.</span></span> <span data-ttu-id="92cc5-128">直接 toohello 一個步驟建立的虛擬網路對等互連使用您選擇的工具，請按一下任何先前工具連結 toogo hello。</span><span class="sxs-lookup"><span data-stu-id="92cc5-128">Click any of hello previous tool links toogo directly toohello steps for creating a virtual network peering using your tool of choice.</span></span>

## <span data-ttu-id="92cc5-129"><a name="register"></a>Hello preview 的註冊</span><span class="sxs-lookup"><span data-stu-id="92cc5-129"><a name="register"></a>Register for hello preview</span></span>

<span data-ttu-id="92cc5-130">hello preview tooregister，完成 hello 遵照的步驟，針對包含虛擬網路的 hello 這兩個訂閱您想 toopeer。</span><span class="sxs-lookup"><span data-stu-id="92cc5-130">tooregister for hello preview, complete hello steps that follow for both subscriptions that contain hello virtual networks you want toopeer.</span></span> <span data-ttu-id="92cc5-131">hello tooregister 用於 hello 預覽的工具是 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="92cc5-131">hello only tool you can use tooregister for hello preview is PowerShell.</span></span>

1. <span data-ttu-id="92cc5-132">安裝 hello hello PowerShell 最新版本[AzureRm](https://www.powershellgallery.com/packages/AzureRM/)模組。</span><span class="sxs-lookup"><span data-stu-id="92cc5-132">Install hello latest version of hello PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) module.</span></span> <span data-ttu-id="92cc5-133">如果您是新 tooAzure PowerShell，請參閱[Azure PowerShell 概觀](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="92cc5-133">If you're new tooAzure PowerShell, see [Azure PowerShell overview](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="92cc5-134">啟動 PowerShell 工作階段，並登入使用 hello tooAzure`login-azurermaccount`命令。</span><span class="sxs-lookup"><span data-stu-id="92cc5-134">Start a PowerShell session and log in tooAzure using hello `login-azurermaccount` command.</span></span>
3. <span data-ttu-id="92cc5-135">輸入下列命令的 hello 註冊 hello 預覽的訂用帳戶：</span><span class="sxs-lookup"><span data-stu-id="92cc5-135">Register your subscription for hello preview by entering hello following commands:</span></span>

    ```powershell
    Register-AzureRmProviderFeature `
      -FeatureName AllowClassicCrossSubscriptionPeering `
      -ProviderNamespace Microsoft.Network
    
    Register-AzureRmResourceProvider `
      -ProviderNamespace Microsoft.Network
    ```
    <span data-ttu-id="92cc5-136">無法完成這篇文章的 hello 入口網站、 Azure CLI 或 PowerShell 章節中的 hello 步驟直到 hello **RegistrationState**輸出之後輸入下列命令的 hello 收到**註冊**這兩個訂用帳戶：</span><span class="sxs-lookup"><span data-stu-id="92cc5-136">Do not complete hello steps in hello Portal, Azure CLI, or PowerShell sections of this article until hello **RegistrationState** output you receive after entering hello following command is **Registered** for both subscriptions:</span></span>

    ```powershell    
    Get-AzureRmProviderFeature `
      -FeatureName AllowClassicCrossSubscriptionPeering `
      -ProviderNamespace Microsoft.Network
    ```

## <span data-ttu-id="92cc5-137"><a name="portal"></a>建立對等互連 - Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="92cc5-137"><a name="portal"></a>Create peering - Azure portal</span></span>

<span data-ttu-id="92cc5-138">本教學課程針對每個訂用帳戶使用不同的帳戶。</span><span class="sxs-lookup"><span data-stu-id="92cc5-138">This tutorial uses different accounts for each subscription.</span></span> <span data-ttu-id="92cc5-139">如果您使用具有權限 tooboth 訂用帳戶的帳戶，您可以使用相同的所有步驟的帳戶，請略過記錄超出 hello 入口網站的 hello 步驟和略過 hello 步驟指定另一位使用者的權限 toohello 虛擬網路的 hello。</span><span class="sxs-lookup"><span data-stu-id="92cc5-139">If you're using an account that has permissions tooboth subscriptions, you can use hello same account for all steps, skip hello steps for logging out of hello portal, and skip hello steps for assigning another user permissions toohello virtual networks.</span></span> <span data-ttu-id="92cc5-140">在完成之前任何 hello 下列步驟，您必須註冊 hello 預覽。</span><span class="sxs-lookup"><span data-stu-id="92cc5-140">Before completing any of hello following steps, you must register for hello preview.</span></span> <span data-ttu-id="92cc5-141">tooregister，hello 步驟完成 hello[註冊 hello 預覽](#register)本文一節。</span><span class="sxs-lookup"><span data-stu-id="92cc5-141">tooregister, complete hello steps in hello [Register for hello preview](#register) section of this article.</span></span> <span data-ttu-id="92cc5-142">請勿繼續 hello 這兩個訂用帳戶中註冊的 hello 預覽的剩餘步驟。</span><span class="sxs-lookup"><span data-stu-id="92cc5-142">Do not continue with hello remaining steps until both subscriptions are registered for hello preview.</span></span>
 
1. <span data-ttu-id="92cc5-143">登入 toohello [Azure 入口網站](https://portal.azure.com)UserA 為。</span><span class="sxs-lookup"><span data-stu-id="92cc5-143">Log in toohello [Azure portal](https://portal.azure.com) as UserA.</span></span> <span data-ttu-id="92cc5-144">登入的 hello 帳戶必須具有 hello 必要的權限 toocreate 虛擬網路對等互連。</span><span class="sxs-lookup"><span data-stu-id="92cc5-144">hello account you log in with must have hello necessary permissions toocreate a virtual network peering.</span></span> <span data-ttu-id="92cc5-145">請參閱 hello[權限](#permissions)本文，如需詳細資訊一節。</span><span class="sxs-lookup"><span data-stu-id="92cc5-145">See hello [Permissions](#permissions) section of this article for details.</span></span>
2. <span data-ttu-id="92cc5-146">依序按一下 [新增]、[網路] 及 [虛擬網路]。</span><span class="sxs-lookup"><span data-stu-id="92cc5-146">Click **+ New**, click **Networking**, then click **Virtual network**.</span></span>
3. <span data-ttu-id="92cc5-147">在 hello**建立虛擬網路**刀鋒視窗中，輸入，或選取值 hello 下列設定，然後按一下 **建立**:</span><span class="sxs-lookup"><span data-stu-id="92cc5-147">In hello **Create virtual network** blade, enter, or select values for hello following settings, then click **Create**:</span></span>
    - <span data-ttu-id="92cc5-148">**名稱**：*myVnetA*</span><span class="sxs-lookup"><span data-stu-id="92cc5-148">**Name**: *myVnetA*</span></span>
    - <span data-ttu-id="92cc5-149">**位址空間**：*10.0.0.0/16*</span><span class="sxs-lookup"><span data-stu-id="92cc5-149">**Address space**: *10.0.0.0/16*</span></span>
    - <span data-ttu-id="92cc5-150">**子網路名稱**：*預設值*</span><span class="sxs-lookup"><span data-stu-id="92cc5-150">**Subnet name**: *default*</span></span>
    - <span data-ttu-id="92cc5-151">**子網路位址範圍**：*10.0.0.0/24*</span><span class="sxs-lookup"><span data-stu-id="92cc5-151">**Subnet address range**: *10.0.0.0/24*</span></span>
    - <span data-ttu-id="92cc5-152">**訂用帳戶**︰選取訂用帳戶 A。</span><span class="sxs-lookup"><span data-stu-id="92cc5-152">**Subscription**: Select subscription A.</span></span>
    - <span data-ttu-id="92cc5-153">**資源群組**：選取 [建立新項目]，然後輸入 *myResourceGroupA*</span><span class="sxs-lookup"><span data-stu-id="92cc5-153">**Resource group**: Select **Create new** and enter *myResourceGroupA*</span></span>
    - <span data-ttu-id="92cc5-154">**位置**：*美國東部*</span><span class="sxs-lookup"><span data-stu-id="92cc5-154">**Location**: *East US*</span></span>
4. <span data-ttu-id="92cc5-155">在 hello**搜尋資源**方塊上方的 hello 入口網站中，型別 hello *myVnetA*。</span><span class="sxs-lookup"><span data-stu-id="92cc5-155">In hello **Search resources** box at hello top of hello portal, type *myVnetA*.</span></span> <span data-ttu-id="92cc5-156">按一下**myVnetA** hello 搜尋結果中出現。</span><span class="sxs-lookup"><span data-stu-id="92cc5-156">Click **myVnetA** when it appears in hello search results.</span></span> <span data-ttu-id="92cc5-157">刀鋒視窗會顯示 hello **myVnetA**虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="92cc5-157">A blade appears for hello **myVnetA** virtual network.</span></span>
5. <span data-ttu-id="92cc5-158">在 [hello **myVnetA**刀鋒視窗中，按一下**存取控制 (IAM)**從 hello 垂直 hello 左邊的 hello] 刀鋒視窗上的選項清單。</span><span class="sxs-lookup"><span data-stu-id="92cc5-158">In hello **myVnetA** blade that appears, click **Access control (IAM)** from hello vertical list of options on hello left side of hello blade.</span></span>
6. <span data-ttu-id="92cc5-159">在 hello **myVnetA-存取控制 (IAM)**刀鋒視窗中，按一下**+ 加**。</span><span class="sxs-lookup"><span data-stu-id="92cc5-159">In hello **myVnetA - Access control (IAM)** blade that appears, click **+ Add**.</span></span>
7. <span data-ttu-id="92cc5-160">在 hello**新增權限**刀鋒視窗中，選取**網路參與者**在 hello**角色**方塊。</span><span class="sxs-lookup"><span data-stu-id="92cc5-160">In hello **Add permissions** blade that appears, select **Network contributor** in hello **Role** box.</span></span>
8. <span data-ttu-id="92cc5-161">在 hello**選取**方塊中，選取使用者 b，或輸入使用者 b 的電子郵件地址 toosearch。</span><span class="sxs-lookup"><span data-stu-id="92cc5-161">In hello **Select** box, select UserB, or type UserB's email address toosearch for it.</span></span> <span data-ttu-id="92cc5-162">hello 使用者顯示的清單是來自 hello 與 hello 虛擬網路的同一個 Azure Active Directory 租用戶您正要設定 hello 對等。</span><span class="sxs-lookup"><span data-stu-id="92cc5-162">hello list of users shown is from hello same Azure Active Directory tenant as hello virtual network you're setting up hello peering for.</span></span> <span data-ttu-id="92cc5-163">當它出現在 hello 清單，請按一下使用者 b。</span><span class="sxs-lookup"><span data-stu-id="92cc5-163">Click UserB when it appears in hello list.</span></span>
9. <span data-ttu-id="92cc5-164">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="92cc5-164">Click **Save**.</span></span>
10. <span data-ttu-id="92cc5-165">登出 hello 入口網站為使用者 a，則 UserB 身分登入。</span><span class="sxs-lookup"><span data-stu-id="92cc5-165">Log out of hello portal as UserA, then log in as UserB.</span></span>
11. <span data-ttu-id="92cc5-166">按一下**+ 新增**，型別*虛擬網路*在 hello**搜尋 hello Marketplace**方塊，然後按一下**虛擬網路**hello 搜尋結果中.</span><span class="sxs-lookup"><span data-stu-id="92cc5-166">Click **+ New**, type *Virtual network* in hello **Search hello Marketplace** box, then click **Virtual network** in hello search results.</span></span>
12. <span data-ttu-id="92cc5-167">在 hello**虛擬網路**刀鋒視窗中，選取**傳統**在 hello**選取部署模型**方塊，然後按一下 **建立**。</span><span class="sxs-lookup"><span data-stu-id="92cc5-167">In hello **Virtual Network** blade that appears, select **Classic** in hello **Select a deployment model** box, then click **Create**.</span></span>
13.   <span data-ttu-id="92cc5-168">會顯示 hello 建立虛擬網路 （傳統） 方塊中輸入下列值的 hello:</span><span class="sxs-lookup"><span data-stu-id="92cc5-168">In hello Create virtual network (classic) box that appears, enter hello following values:</span></span>

    - <span data-ttu-id="92cc5-169">**名稱**：*myVnetB*</span><span class="sxs-lookup"><span data-stu-id="92cc5-169">**Name**: *myVnetB*</span></span>
    - <span data-ttu-id="92cc5-170">**位址空間**：*10.1.0.0/16*</span><span class="sxs-lookup"><span data-stu-id="92cc5-170">**Address space**: *10.1.0.0/16*</span></span>
    - <span data-ttu-id="92cc5-171">**子網路名稱**：*預設值*</span><span class="sxs-lookup"><span data-stu-id="92cc5-171">**Subnet name**: *default*</span></span>
    - <span data-ttu-id="92cc5-172">**子網路位址範圍**：*10.1.0.0/24*</span><span class="sxs-lookup"><span data-stu-id="92cc5-172">**Subnet address range**: *10.1.0.0/24*</span></span>
    - <span data-ttu-id="92cc5-173">**訂用帳戶**︰選取訂用帳戶 B。</span><span class="sxs-lookup"><span data-stu-id="92cc5-173">**Subscription**: Select subscription B.</span></span>
    - <span data-ttu-id="92cc5-174">**資源群組**：選取 [建立新項目]，然後輸入 *myResourceGroupB*</span><span class="sxs-lookup"><span data-stu-id="92cc5-174">**Resource group**: Select **Create new** and enter *myResourceGroupB*</span></span>
    - <span data-ttu-id="92cc5-175">**位置**：*美國東部*</span><span class="sxs-lookup"><span data-stu-id="92cc5-175">**Location**: *East US*</span></span>

14. <span data-ttu-id="92cc5-176">在 hello**搜尋資源**方塊上方的 hello 入口網站中，型別 hello *myVnetB*。</span><span class="sxs-lookup"><span data-stu-id="92cc5-176">In hello **Search resources** box at hello top of hello portal, type *myVnetB*.</span></span> <span data-ttu-id="92cc5-177">按一下**myVnetB** hello 搜尋結果中出現。</span><span class="sxs-lookup"><span data-stu-id="92cc5-177">Click **myVnetB** when it appears in hello search results.</span></span> <span data-ttu-id="92cc5-178">刀鋒視窗會顯示 hello **myVnetB**虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="92cc5-178">A blade appears for hello **myVnetB** virtual network.</span></span>
15. <span data-ttu-id="92cc5-179">在 [hello **myVnetB**刀鋒視窗中，按一下**屬性**從 hello 垂直 hello 左邊的 hello] 刀鋒視窗上的選項清單。</span><span class="sxs-lookup"><span data-stu-id="92cc5-179">In hello **myVnetB** blade that appears, click **Properties** from hello vertical list of options on hello left side of hello blade.</span></span> <span data-ttu-id="92cc5-180">複製 hello**資源識別碼**，這用於後續的步驟。</span><span class="sxs-lookup"><span data-stu-id="92cc5-180">Copy hello **RESOURCE ID**, which is used in a later step.</span></span> <span data-ttu-id="92cc5-181">hello 資源識別碼是下列範例類似 toohello: /subscriptions/<Susbscription ID>/resourceGroups/myResoureGroupB/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB</span><span class="sxs-lookup"><span data-stu-id="92cc5-181">hello resource ID is similar toohello following example: /subscriptions/<Susbscription ID>/resourceGroups/myResoureGroupB/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB</span></span>
16. <span data-ttu-id="92cc5-182">針對 myVnetB 完成步驟 5-9，其中在步驟 8 輸入 **UserA**。</span><span class="sxs-lookup"><span data-stu-id="92cc5-182">Complete steps 5-9 for myVnetB, entering **UserA** in step 8.</span></span>
17. <span data-ttu-id="92cc5-183">登出為 UserB hello 入口網站，並以 UserA 登入。</span><span class="sxs-lookup"><span data-stu-id="92cc5-183">Log out of hello portal as UserB and log in as UserA.</span></span>
18. <span data-ttu-id="92cc5-184">在 hello**搜尋資源**方塊上方的 hello 入口網站中，型別 hello *myVnetA*。</span><span class="sxs-lookup"><span data-stu-id="92cc5-184">In hello **Search resources** box at hello top of hello portal, type *myVnetA*.</span></span> <span data-ttu-id="92cc5-185">按一下**myVnetA** hello 搜尋結果中出現。</span><span class="sxs-lookup"><span data-stu-id="92cc5-185">Click **myVnetA** when it appears in hello search results.</span></span> <span data-ttu-id="92cc5-186">刀鋒視窗會顯示 hello **myVnet**虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="92cc5-186">A blade appears for hello **myVnet** virtual network.</span></span>
19. <span data-ttu-id="92cc5-187">按一下 [myVnetA]。</span><span class="sxs-lookup"><span data-stu-id="92cc5-187">Click **myVnetA**.</span></span>
20. <span data-ttu-id="92cc5-188">在 [hello **myVnetA**刀鋒視窗中，按一下**對等互連**從 hello 垂直 hello 左邊的 hello] 刀鋒視窗上的選項清單。</span><span class="sxs-lookup"><span data-stu-id="92cc5-188">In hello **myVnetA** blade that appears, click **Peerings** from hello vertical list of options on hello left side of hello blade.</span></span>
21. <span data-ttu-id="92cc5-189">在 hello **myVnetA-對等互連**刀鋒視窗中出現，按一下**+ 新增**</span><span class="sxs-lookup"><span data-stu-id="92cc5-189">In hello **myVnetA - Peerings** blade that appeared, click **+ Add**</span></span>
22. <span data-ttu-id="92cc5-190">在 hello**新增對等互連**刀鋒視窗中，輸入，或選取 hello 下列選項，然後按一下 **確定**:</span><span class="sxs-lookup"><span data-stu-id="92cc5-190">In hello **Add peering** blade that appears, enter, or select hello following options, then click **OK**:</span></span>
     - <span data-ttu-id="92cc5-191">**名稱**：*myVnetAToMyVnetB*</span><span class="sxs-lookup"><span data-stu-id="92cc5-191">**Name**: *myVnetAToMyVnetB*</span></span>
     - <span data-ttu-id="92cc5-192">**虛擬網路部署模型**︰選取 [傳統]。</span><span class="sxs-lookup"><span data-stu-id="92cc5-192">**Virtual network deployment model**:  Select **Classic**.</span></span>
     - <span data-ttu-id="92cc5-193">**我知道我的資源識別碼**：核取此方塊。</span><span class="sxs-lookup"><span data-stu-id="92cc5-193">**I know my resource ID**: Check this box.</span></span>
     - <span data-ttu-id="92cc5-194">**資源識別碼**： 輸入 myVnetB hello 資源識別碼，從步驟 15。</span><span class="sxs-lookup"><span data-stu-id="92cc5-194">**Resource ID**: Enter hello resource ID of myVnetB from step 15.</span></span>
     - <span data-ttu-id="92cc5-195">**允許虛擬網路存取**：確定已選取 [啟用]。</span><span class="sxs-lookup"><span data-stu-id="92cc5-195">**Allow virtual network access:** Ensure that **Enabled** is selected.</span></span>
    <span data-ttu-id="92cc5-196">本教學課程中不會使用其他設定。</span><span class="sxs-lookup"><span data-stu-id="92cc5-196">No other settings are used in this tutorial.</span></span> <span data-ttu-id="92cc5-197">讀取所有的對等設定的相關 toolearn[管理虛擬網路對等互連](virtual-network-manage-peering.md#create-a-peering)。</span><span class="sxs-lookup"><span data-stu-id="92cc5-197">toolearn about all peering settings, read [Manage virtual network peerings](virtual-network-manage-peering.md#create-a-peering).</span></span>
23. <span data-ttu-id="92cc5-198">按一下後**[確定]** hello 先前步驟中，在 hello**新增對等互連**刀鋒視窗會關閉，而且您會看見 hello **myVnetA-對等互連**刀鋒視窗一次。</span><span class="sxs-lookup"><span data-stu-id="92cc5-198">After clicking **OK** in hello previous step, hello **Add peering** blade closes and you see hello **myVnetA - Peerings** blade again.</span></span> <span data-ttu-id="92cc5-199">幾秒之後，對等互連您所建立的 hello 會出現在 [hello] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="92cc5-199">After a few seconds, hello peering you created appears in hello blade.</span></span> <span data-ttu-id="92cc5-200">**連接**會列在 hello**對等互連狀態**hello 的資料行**myVnetAToMyVnetB**對等互連您建立。</span><span class="sxs-lookup"><span data-stu-id="92cc5-200">**Connected** is listed in hello **PEERING STATUS** column for hello **myVnetAToMyVnetB** peering you created.</span></span> <span data-ttu-id="92cc5-201">現在建立 hello 對等互連。</span><span class="sxs-lookup"><span data-stu-id="92cc5-201">hello peering is now established.</span></span> <span data-ttu-id="92cc5-202">沒有需要 toopeer hello 虛擬網路 （傳統） toohello 虛擬網路 （資源管理員）。</span><span class="sxs-lookup"><span data-stu-id="92cc5-202">There is no need toopeer hello virtual network (classic) toohello virtual network (Resource Manager).</span></span>

    <span data-ttu-id="92cc5-203">所建立的其中一個虛擬網路中任何 Azure 資源，現在都能 toocommunicate 彼此透過其 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="92cc5-203">Any Azure resources you create in either virtual network are now able toocommunicate with each other through their IP addresses.</span></span> <span data-ttu-id="92cc5-204">如果您使用預設 Azure 名稱解析為 hello 虛擬網路，hello hello 虛擬網路中沒有資源無法 tooresolve 名稱在 hello 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="92cc5-204">If you're using default Azure name resolution for hello virtual networks, hello resources in hello virtual networks are not able tooresolve names across hello virtual networks.</span></span> <span data-ttu-id="92cc5-205">如果您想 tooresolve 名稱多個虛擬網路中的對等互連，您必須建立您自己的 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="92cc5-205">If you want tooresolve names across virtual networks in a peering, you must create your own DNS server.</span></span> <span data-ttu-id="92cc5-206">深入了解如何註冊 tooset[使用您自己的 DNS 伺服器的名稱解析](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server)。</span><span class="sxs-lookup"><span data-stu-id="92cc5-206">Learn how tooset up [Name resolution using your own DNS server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span></span>

24. <span data-ttu-id="92cc5-207">**選擇性**： 未涵蓋在本教學課程中建立虛擬機器，雖然您可以在每個虛擬網路中建立虛擬機器，並從一個虛擬機器 toohello 其他 toovalidate 連線連接。</span><span class="sxs-lookup"><span data-stu-id="92cc5-207">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine toohello other, toovalidate connectivity.</span></span>
25. <span data-ttu-id="92cc5-208">**選擇性**: toodelete hello 您在本教學課程中建立的資源，hello 步驟完成 hello[刪除資源](#delete-portal)本文一節。</span><span class="sxs-lookup"><span data-stu-id="92cc5-208">**Optional**: toodelete hello resources that you create in this tutorial, complete hello steps in hello [Delete resources](#delete-portal) section of this article.</span></span>

## <span data-ttu-id="92cc5-209"><a name="cli"></a>建立對等互連 - Azure CLI</span><span class="sxs-lookup"><span data-stu-id="92cc5-209"><a name="cli"></a>Create peering - Azure CLI</span></span>

<span data-ttu-id="92cc5-210">本教學課程針對每個訂用帳戶使用不同的帳戶。</span><span class="sxs-lookup"><span data-stu-id="92cc5-210">This tutorial uses different accounts for each subscription.</span></span> <span data-ttu-id="92cc5-211">如果您使用具有權限 tooboth 訂用帳戶的帳戶，您可以使用的 hello 相同所有步驟的帳戶，請略過 hello 步驟記錄移出 Azure，並移除 hello 行指令碼，建立使用者角色指派。</span><span class="sxs-lookup"><span data-stu-id="92cc5-211">If you're using an account that has permissions tooboth subscriptions, you can use hello same account for all steps, skip hello steps for logging out of Azure, and remove hello lines of script that create user role assignments.</span></span> <span data-ttu-id="92cc5-212">取代UserA@azure.com和UserB@azure.com所有 hello 遵循您所使用的 Dby 與 Dbz hello 使用者名稱與指令碼中。</span><span class="sxs-lookup"><span data-stu-id="92cc5-212">Replace UserA@azure.com and UserB@azure.com in all of hello following scripts with hello usernames you're using for UserA and UserB.</span></span> 

<span data-ttu-id="92cc5-213">在完成之前任何 hello 下列步驟，您必須註冊 hello 預覽。</span><span class="sxs-lookup"><span data-stu-id="92cc5-213">Before completing any of hello following steps, you must register for hello preview.</span></span> <span data-ttu-id="92cc5-214">tooregister，hello 步驟完成 hello[註冊 hello 預覽](#register)本文一節。</span><span class="sxs-lookup"><span data-stu-id="92cc5-214">tooregister, complete hello steps in hello [Register for hello preview](#register) section of this article.</span></span> <span data-ttu-id="92cc5-215">請勿繼續 hello 這兩個訂用帳戶中註冊的 hello 預覽的剩餘步驟。</span><span class="sxs-lookup"><span data-stu-id="92cc5-215">Do not continue with hello remaining steps until both subscriptions are registered for hello preview.</span></span>

1. <span data-ttu-id="92cc5-216">[安裝](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json)hello Azure CLI 1.0 toocreate hello 虛擬網路 （傳統）。</span><span class="sxs-lookup"><span data-stu-id="92cc5-216">[Install](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) hello Azure CLI 1.0 toocreate hello virtual network (classic).</span></span>
2. <span data-ttu-id="92cc5-217">開啟 CLI 工作階段，並以使用者 b 使用 hello 登入 tooAzure`azure login`命令。</span><span class="sxs-lookup"><span data-stu-id="92cc5-217">Open a CLI session and log in tooAzure as UserB using hello `azure login` command.</span></span>
3. <span data-ttu-id="92cc5-218">服務管理模式中執行 hello CLI，方式是輸入 hello`azure config mode asm`命令。</span><span class="sxs-lookup"><span data-stu-id="92cc5-218">Run hello CLI in Service Management mode by entering hello `azure config mode asm` command.</span></span>
4. <span data-ttu-id="92cc5-219">輸入下列命令 toocreate hello 虛擬網路 （傳統） 的 hello:</span><span class="sxs-lookup"><span data-stu-id="92cc5-219">Enter hello following command toocreate hello virtual network (classic):</span></span>
 
    ```azurecli
    azure network vnet create --vnet myVnetB --address-space 10.1.0.0 --cidr 16 --location "East US"
    ```
5. <span data-ttu-id="92cc5-220">bash 殼層中使用 Azure CLI 2.0.4 hello 必須完成剩餘步驟 hello 或更新版本[安裝](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json)，或使用 hello Azure 雲端殼層。</span><span class="sxs-lookup"><span data-stu-id="92cc5-220">hello remaining steps must be completed using a bash shell with hello Azure CLI 2.0.4 or later [installed](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json), or by using hello Azure Cloud Shell.</span></span> <span data-ttu-id="92cc5-221">hello Azure 雲端殼層是免費的 Bash 殼層，您可以直接在 hello Azure 入口網站中執行。</span><span class="sxs-lookup"><span data-stu-id="92cc5-221">hello Azure Cloud Shell is a free Bash shell that you can run directly within hello Azure portal.</span></span> <span data-ttu-id="92cc5-222">它有的 hello Azure CLI 預先安裝和設定 toouse 與您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="92cc5-222">It has hello Azure CLI preinstalled and configured toouse with your account.</span></span> <span data-ttu-id="92cc5-223">按一下 hello**試試**hello 中的按鈕的指令碼後面，這會開啟您登入 Azure 帳戶 tooyour 雲端殼層。</span><span class="sxs-lookup"><span data-stu-id="92cc5-223">Click hello **Try it** button in hello scripts that follow, which opens a Cloud Shell that logs you in tooyour Azure account.</span></span> <span data-ttu-id="92cc5-224">如選項上執行被 Windows 用戶端上的 CLI 指令碼，請參閱 < [Windows 中執行 hello Azure CLI](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="92cc5-224">For options on running bash CLI scripts on a Windows client, see [Running hello Azure CLI in Windows](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> 
6. <span data-ttu-id="92cc5-225">複製下列指令碼 tooa 文字編輯器在您的電腦上的 hello。</span><span class="sxs-lookup"><span data-stu-id="92cc5-225">Copy hello following script tooa text editor on your PC.</span></span> <span data-ttu-id="92cc5-226">使用您的訂用帳戶 ID 來取代 `<SubscriptionB-Id>` 。</span><span class="sxs-lookup"><span data-stu-id="92cc5-226">Replace `<SubscriptionB-Id>` with your subscription ID.</span></span> <span data-ttu-id="92cc5-227">如果您不知道您的訂用帳戶 Id，請輸入 hello`az account show`命令。</span><span class="sxs-lookup"><span data-stu-id="92cc5-227">If you don't know your subscription Id, enter hello `az account show` command.</span></span> <span data-ttu-id="92cc5-228">hello 值**識別碼**在 hello 的輸出會是您的訂用帳戶 id。複製 hello 修改指令碼，將它貼入 tooyour CLI 2.0 工作階段中，然後按`Enter`。</span><span class="sxs-lookup"><span data-stu-id="92cc5-228">hello value for **id** in hello output is your subscription Id. Copy hello modified script, paste it in tooyour CLI 2.0 session, and then press `Enter`.</span></span> 

    ```azurecli-interactive
    az role assignment create \
      --assignee UserA@azure.com \
      --role "Classic Network Contributor" \
      --scope /subscriptions/<SubscriptionB-Id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB
    ```

    <span data-ttu-id="92cc5-229">當您建立 hello 虛擬網路 （傳統） 在步驟 4 中時，Azure 會建立 hello 的 hello 虛擬網路*預設網路*資源群組。</span><span class="sxs-lookup"><span data-stu-id="92cc5-229">When you created hello virtual network (classic) in step 4, Azure created hello virtual network in hello *Default-Networking* resource group.</span></span>
7. <span data-ttu-id="92cc5-230">記錄超出 Azure 與記錄檔中的 UserB 為 UserA hello CLI 2.0。</span><span class="sxs-lookup"><span data-stu-id="92cc5-230">Log UserB out of Azure and log in as UserA in hello CLI 2.0.</span></span>
8. <span data-ttu-id="92cc5-231">建立資源群組和虛擬網路 (Resource Manager)。</span><span class="sxs-lookup"><span data-stu-id="92cc5-231">Create a resource group and a virtual network (Resource Manager).</span></span> <span data-ttu-id="92cc5-232">複製 hello 下列指令碼，將它貼入 tooyour CLI 工作階段中，然後按`Enter`。</span><span class="sxs-lookup"><span data-stu-id="92cc5-232">Copy hello following script, paste it in tooyour CLI session, and then press `Enter`.</span></span> 

    ```azurecli-interactive
    #!/bin/bash

    # Variables for common values used throughout hello script.
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

    # Get hello id for myVnetA.
    vNetAId=$(az network vnet show \
      --resource-group $rgName \
      --name myVnetA \
      --query id --out tsv)

    # Assign UserB permissions toomyVnetA.
    az role assignment create \
      --assignee UserB@azure.com \
      --role "Network Contributor" \
      --scope $vNetAId
    ```

9. <span data-ttu-id="92cc5-233">建立虛擬網路之間 hello 兩個虛擬網路透過 hello 不同的部署模型建立對等互連。</span><span class="sxs-lookup"><span data-stu-id="92cc5-233">Create a virtual network peering between hello two virtual networks created through hello different deployment models.</span></span> <span data-ttu-id="92cc5-234">複製下列指令碼 tooa 文字編輯器在您的電腦上的 hello。</span><span class="sxs-lookup"><span data-stu-id="92cc5-234">Copy hello following script tooa text editor on your PC.</span></span> <span data-ttu-id="92cc5-235">使用您的訂用帳戶 ID 來取代 `<SubscriptionB-id>` 。如果您不知道您的訂用帳戶 Id，請輸入 hello`az account show`命令。</span><span class="sxs-lookup"><span data-stu-id="92cc5-235">Replace `<SubscriptionB-id>` with your subscription Id. If you don't know your subscription Id, enter hello `az account show` command.</span></span> <span data-ttu-id="92cc5-236">hello 值**識別碼**在 hello 的輸出會是您的訂用帳戶 id。Azure 建立 hello 虛擬網路 （傳統） 您在步驟 4 建立的資源群組中名為*預設網路*。</span><span class="sxs-lookup"><span data-stu-id="92cc5-236">hello value for **id** in hello output is your subscription Id. Azure created hello virtual network (classic) you created in step 4 in a resource group named *Default-Networking*.</span></span> <span data-ttu-id="92cc5-237">在您 CLI 工作階段中，貼上 hello 修改指令碼，然後按下`Enter`。</span><span class="sxs-lookup"><span data-stu-id="92cc5-237">Paste hello modified script in your CLI session, and then press `Enter`.</span></span>

    ```azurecli-interactive
    # Peer VNet1 tooVNet2.
    az network vnet peering create \
      --name myVnetAToMyVnetB \
      --resource-group $rgName \
      --vnet-name myVnetA \
      --remote-vnet-id  /subscriptions/<SubscriptionB-id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB \
      --allow-vnet-access
    ```

10. <span data-ttu-id="92cc5-238">Hello 指令碼執行之後，請檢閱 hello 對等互連 hello 虛擬網路 （資源管理員）。</span><span class="sxs-lookup"><span data-stu-id="92cc5-238">After hello script executes, review hello peering for hello virtual network (Resource Manager).</span></span> <span data-ttu-id="92cc5-239">複製下列指令碼的 hello，並再將它貼入您 CLI 的工作階段中：</span><span class="sxs-lookup"><span data-stu-id="92cc5-239">Copy hello following script, and then paste it in your CLI session:</span></span>

    ```azurecli-interactive
    az network vnet peering list \
      --resource-group $rgName \
      --vnet-name myVnetA \
      --output table
    ```
    <span data-ttu-id="92cc5-240">輸出中顯示 hello **Connected**在 hello **PeeringState**資料行。</span><span class="sxs-lookup"><span data-stu-id="92cc5-240">hello output shows **Connected** in hello **PeeringState** column.</span></span>

    <span data-ttu-id="92cc5-241">所建立的其中一個虛擬網路中任何 Azure 資源，現在都能 toocommunicate 彼此透過其 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="92cc5-241">Any Azure resources you create in either virtual network are now able toocommunicate with each other through their IP addresses.</span></span> <span data-ttu-id="92cc5-242">如果您使用預設 Azure 名稱解析為 hello 虛擬網路，hello hello 虛擬網路中沒有資源無法 tooresolve 名稱在 hello 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="92cc5-242">If you're using default Azure name resolution for hello virtual networks, hello resources in hello virtual networks are not able tooresolve names across hello virtual networks.</span></span> <span data-ttu-id="92cc5-243">如果您想 tooresolve 名稱多個虛擬網路中的對等互連，您必須建立您自己的 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="92cc5-243">If you want tooresolve names across virtual networks in a peering, you must create your own DNS server.</span></span> <span data-ttu-id="92cc5-244">深入了解如何註冊 tooset[使用您自己的 DNS 伺服器的名稱解析](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server)。</span><span class="sxs-lookup"><span data-stu-id="92cc5-244">Learn how tooset up [Name resolution using your own DNS server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span></span>

11. <span data-ttu-id="92cc5-245">**選擇性**： 未涵蓋在本教學課程中建立虛擬機器，雖然您可以在每個虛擬網路中建立虛擬機器，並從一個虛擬機器 toohello 其他 toovalidate 連線連接。</span><span class="sxs-lookup"><span data-stu-id="92cc5-245">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine toohello other, toovalidate connectivity.</span></span>
12. <span data-ttu-id="92cc5-246">**選擇性**: toodelete hello 您在本教學課程中建立的資源，步驟完成 hello[刪除資源](#delete-cli)本文中。</span><span class="sxs-lookup"><span data-stu-id="92cc5-246">**Optional**: toodelete hello resources that you create in this tutorial, complete hello steps in [Delete resources](#delete-cli) in this article.</span></span>

## <span data-ttu-id="92cc5-247"><a name="powershell"></a>建立對等互連 - PowerShell</span><span class="sxs-lookup"><span data-stu-id="92cc5-247"><a name="powershell"></a>Create peering - PowerShell</span></span>

<span data-ttu-id="92cc5-248">本教學課程針對每個訂用帳戶使用不同的帳戶。</span><span class="sxs-lookup"><span data-stu-id="92cc5-248">This tutorial uses different accounts for each subscription.</span></span> <span data-ttu-id="92cc5-249">如果您使用具有權限 tooboth 訂用帳戶的帳戶，您可以使用的 hello 相同所有步驟的帳戶，請略過 hello 步驟記錄移出 Azure，並移除 hello 行指令碼，建立使用者角色指派。</span><span class="sxs-lookup"><span data-stu-id="92cc5-249">If you're using an account that has permissions tooboth subscriptions, you can use hello same account for all steps, skip hello steps for logging out of Azure, and remove hello lines of script that create user role assignments.</span></span> <span data-ttu-id="92cc5-250">取代UserA@azure.com和UserB@azure.com所有 hello 遵循您所使用的 Dby 與 Dbz hello 使用者名稱與指令碼中。</span><span class="sxs-lookup"><span data-stu-id="92cc5-250">Replace UserA@azure.com and UserB@azure.com in all of hello following scripts with hello usernames you're using for UserA and UserB.</span></span> 

<span data-ttu-id="92cc5-251">在完成之前任何 hello 下列步驟，您必須註冊 hello 預覽。</span><span class="sxs-lookup"><span data-stu-id="92cc5-251">Before completing any of hello following steps, you must register for hello preview.</span></span> <span data-ttu-id="92cc5-252">tooregister，hello 步驟完成 hello[註冊 hello 預覽](#register)本文一節。</span><span class="sxs-lookup"><span data-stu-id="92cc5-252">tooregister, complete hello steps in hello [Register for hello preview](#register) section of this article.</span></span> <span data-ttu-id="92cc5-253">請勿繼續 hello 這兩個訂用帳戶中註冊的 hello 預覽的剩餘步驟。</span><span class="sxs-lookup"><span data-stu-id="92cc5-253">Do not continue with hello remaining steps until both subscriptions are registered for hello preview.</span></span>

1. <span data-ttu-id="92cc5-254">安裝 hello hello PowerShell 最新版本[Azure](https://www.powershellgallery.com/packages/Azure)和[AzureRm](https://www.powershellgallery.com/packages/AzureRM/)模組。</span><span class="sxs-lookup"><span data-stu-id="92cc5-254">Install hello latest version of hello PowerShell [Azure](https://www.powershellgallery.com/packages/Azure) and [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) modules.</span></span> <span data-ttu-id="92cc5-255">如果您是新 tooAzure PowerShell，請參閱[Azure PowerShell 概觀](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="92cc5-255">If you're new tooAzure PowerShell, see [Azure PowerShell overview](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="92cc5-256">啟動 PowerShell 工作階段。</span><span class="sxs-lookup"><span data-stu-id="92cc5-256">Start a PowerShell session.</span></span>
3. <span data-ttu-id="92cc5-257">在 PowerShell 中，記錄 Dbz tooUserB 的訂用帳戶中輸入 hello`Add-AzureAccount`命令。</span><span class="sxs-lookup"><span data-stu-id="92cc5-257">In PowerShell, log in tooUserB's subscription as UserB by entering hello `Add-AzureAccount` command.</span></span>
4. <span data-ttu-id="92cc5-258">toocreate 具有 PowerShell （傳統） 的虛擬網路，您必須建立新的或修改現有的網路組態檔。</span><span class="sxs-lookup"><span data-stu-id="92cc5-258">toocreate a virtual network (classic) with PowerShell, you must create a new, or modify an existing, network configuration file.</span></span> <span data-ttu-id="92cc5-259">了解如何太[匯出、 更新和匯入網路組態檔](virtual-networks-using-network-configuration-file.md)。</span><span class="sxs-lookup"><span data-stu-id="92cc5-259">Learn how too[export, update, and import network configuration files](virtual-networks-using-network-configuration-file.md).</span></span> <span data-ttu-id="92cc5-260">hello 檔案應該包含 hello 下列**VirtualNetworkSite** hello 這個教學課程中使用的虛擬網路的項目：</span><span class="sxs-lookup"><span data-stu-id="92cc5-260">hello file should include hello following **VirtualNetworkSite** element for hello virtual network used in this tutorial:</span></span>

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
    > <span data-ttu-id="92cc5-261">匯入已變更的網路組態檔，可能會導致變更 tooexisting （傳統） 您的訂用帳戶中的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="92cc5-261">Importing a changed network configuration file can cause changes tooexisting virtual networks (classic) in your subscription.</span></span> <span data-ttu-id="92cc5-262">確定您只有新增 hello 的上一個虛擬網路，且您不變更或移除任何現有的虛擬網路從您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="92cc5-262">Ensure you only add hello previous virtual network and that you don't change or remove any existing virtual networks from your subscription.</span></span> 

5. <span data-ttu-id="92cc5-263">記錄 Dbz toouse 資源管理員命令 tooUserB 的訂用帳戶中，輸入 hello`login-azurermaccount`命令。</span><span class="sxs-lookup"><span data-stu-id="92cc5-263">Log in tooUserB's subscription as UserB toouse Resource Manager commands by entering hello `login-azurermaccount` command.</span></span>
6. <span data-ttu-id="92cc5-264">指派使用者 a 的權限 toovirtual 網路 b 複製 hello 下列指令碼 tooa 文字編輯器，在您的電腦上，並取代`<SubscriptionB-id>`訂閱 b 的 hello 識別碼如果您不知道 hello 訂用帳戶 Id，請輸入 hello`Get-AzureRmSubscription`命令 tooview 它。</span><span class="sxs-lookup"><span data-stu-id="92cc5-264">Assign UserA permissions toovirtual network B. Copy hello following script tooa text editor on your PC and replace `<SubscriptionB-id>` with hello ID of subscription B. If you don't know hello subscription Id, enter hello `Get-AzureRmSubscription` command tooview it.</span></span> <span data-ttu-id="92cc5-265">hello 值**識別碼**hello 傳回輸出是您的訂用帳戶 id。</span><span class="sxs-lookup"><span data-stu-id="92cc5-265">hello value for **Id** in hello returned output is your subscription ID.</span></span> <span data-ttu-id="92cc5-266">Azure 建立 hello 虛擬網路 （傳統） 您在步驟 4 建立的資源群組中名為*預設網路*。</span><span class="sxs-lookup"><span data-stu-id="92cc5-266">Azure created hello virtual network (classic) you created in step 4 in a resource group named *Default-Networking*.</span></span> <span data-ttu-id="92cc5-267">tooexecute hello 指令碼中，複製 hello 修改指令碼，將它貼入 tooPowerShell 中,，然後按`Enter`。</span><span class="sxs-lookup"><span data-stu-id="92cc5-267">tooexecute hello script, copy hello modified script, paste it in tooPowerShell, and then press `Enter`.</span></span>
    
    ```powershell 
    New-AzureRmRoleAssignment `
      -SignInName UserA@azure.com `
      -RoleDefinitionName "Classic Network Contributor" `
      -Scope /subscriptions/<SubscriptionB-id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB
    ```

7. <span data-ttu-id="92cc5-268">登出 Azure 以做為 UserB 和記錄 UserA tooUserA 的訂用帳戶中，輸入 hello`login-azurermaccount`命令。</span><span class="sxs-lookup"><span data-stu-id="92cc5-268">Log out of Azure as UserB and log in tooUserA's subscription as UserA by entering hello `login-azurermaccount` command.</span></span> <span data-ttu-id="92cc5-269">登入的 hello 帳戶必須具有 hello 必要的權限 toocreate 虛擬網路對等互連。</span><span class="sxs-lookup"><span data-stu-id="92cc5-269">hello account you log in with must have hello necessary permissions toocreate a virtual network peering.</span></span> <span data-ttu-id="92cc5-270">請參閱 hello[權限](#permissions)本文，如需詳細資訊一節。</span><span class="sxs-lookup"><span data-stu-id="92cc5-270">See hello [Permissions](#permissions) section of this article for details.</span></span>
8. <span data-ttu-id="92cc5-271">複製下列指令碼，將它貼在 tooPowerShell，，然後按下的 hello 建立 hello 虛擬網路 （資源管理員） `Enter`:</span><span class="sxs-lookup"><span data-stu-id="92cc5-271">Create hello virtual network (Resource Manager) by copying hello following script, pasting it in tooPowerShell, and then pressing `Enter`:</span></span>

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

9. <span data-ttu-id="92cc5-272">指派使用者 b 的權限 toomyVnetA。</span><span class="sxs-lookup"><span data-stu-id="92cc5-272">Assign UserB permissions toomyVnetA.</span></span> <span data-ttu-id="92cc5-273">複製 hello 下列指令碼 tooa 文字編輯器，在您的電腦上，並取代`<SubscriptionA-Id>`識別碼為訂用帳戶 A.hello如果您不知道 hello 訂用帳戶 Id，請輸入 hello`Get-AzureRmSubscription`命令 tooview 它。</span><span class="sxs-lookup"><span data-stu-id="92cc5-273">Copy hello following script tooa text editor on your PC and replace `<SubscriptionA-Id>` with hello ID of subscription A. If you don't know hello subscription Id, enter hello `Get-AzureRmSubscription` command tooview it.</span></span> <span data-ttu-id="92cc5-274">hello 值**識別碼**hello 傳回輸出是您的訂用帳戶 id。</span><span class="sxs-lookup"><span data-stu-id="92cc5-274">hello value for **Id** in hello returned output is your subscription ID.</span></span> <span data-ttu-id="92cc5-275">在 PowerShell 中，貼上 hello hello 指令碼已修改的版本，然後按下`Enter`tooexecute 它。</span><span class="sxs-lookup"><span data-stu-id="92cc5-275">Paste hello modified version of hello script in PowerShell, and then press `Enter` tooexecute it.</span></span>

    ```powershell
    New-AzureRmRoleAssignment `
      -SignInName UserB@azure.com `
      -RoleDefinitionName "Network Contributor" `
      -Scope /subscriptions/<SubscriptionA-Id>/resourceGroups/myResourceGroupA/providers/Microsoft.Network/VirtualNetworks/myVnetA
    ```

10. <span data-ttu-id="92cc5-276">複製 hello 下列指令碼 tooa 文字編輯器，在您的電腦，並取代`<SubscriptionB-id>`識別碼 hello 為訂用帳戶 B.toopeer myVnetA toomyVNetB，複製 hello 修改指令碼，將它貼入 tooPowerShell 中,，然後按`Enter`。</span><span class="sxs-lookup"><span data-stu-id="92cc5-276">Copy hello following script tooa text editor on your PC, and replace `<SubscriptionB-id>` with hello ID of subscription B. toopeer myVnetA toomyVNetB, copy hello modified script, paste it in tooPowerShell, and then press `Enter`.</span></span>

    ```powershell
    Add-AzureRmVirtualNetworkPeering `
      -Name 'myVnetAToMyVnetB' `
      -VirtualNetwork $vnetA `
      -RemoteVirtualNetworkId /subscriptions/<SubscriptionB-id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB
    ```

11. <span data-ttu-id="92cc5-277">複製下列指令碼，將它貼到 PowerShell，並按下的 hello 檢視 myVnetA hello 對等互連狀態`Enter`。</span><span class="sxs-lookup"><span data-stu-id="92cc5-277">View hello peering state of myVnetA by copying hello following script, pasting it into PowerShell, and pressing `Enter`.</span></span>

    ```powershell
    Get-AzureRmVirtualNetworkPeering `
      -ResourceGroupName $rgName `
      -VirtualNetworkName myVnetA `
      | Format-Table VirtualNetworkName, PeeringState
    ```

    <span data-ttu-id="92cc5-278">hello 狀態是**Connected**。</span><span class="sxs-lookup"><span data-stu-id="92cc5-278">hello state is **Connected**.</span></span> <span data-ttu-id="92cc5-279">它會隨之變更**Connected**一旦您設定從 myVnetB hello 對等互連 toomyVnetA。</span><span class="sxs-lookup"><span data-stu-id="92cc5-279">It changes too**Connected** once you setup hello peering toomyVnetA from myVnetB.</span></span>

    <span data-ttu-id="92cc5-280">所建立的其中一個虛擬網路中任何 Azure 資源，現在都能 toocommunicate 彼此透過其 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="92cc5-280">Any Azure resources you create in either virtual network are now able toocommunicate with each other through their IP addresses.</span></span> <span data-ttu-id="92cc5-281">如果您使用預設 Azure 名稱解析為 hello 虛擬網路，hello hello 虛擬網路中沒有資源無法 tooresolve 名稱在 hello 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="92cc5-281">If you're using default Azure name resolution for hello virtual networks, hello resources in hello virtual networks are not able tooresolve names across hello virtual networks.</span></span> <span data-ttu-id="92cc5-282">如果您想 tooresolve 名稱多個虛擬網路中的對等互連，您必須建立您自己的 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="92cc5-282">If you want tooresolve names across virtual networks in a peering, you must create your own DNS server.</span></span> <span data-ttu-id="92cc5-283">深入了解如何註冊 tooset[使用您自己的 DNS 伺服器的名稱解析](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server)。</span><span class="sxs-lookup"><span data-stu-id="92cc5-283">Learn how tooset up [Name resolution using your own DNS server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span></span>

12. <span data-ttu-id="92cc5-284">**選擇性**： 未涵蓋在本教學課程中建立虛擬機器，雖然您可以在每個虛擬網路中建立虛擬機器，並從一個虛擬機器 toohello 其他 toovalidate 連線連接。</span><span class="sxs-lookup"><span data-stu-id="92cc5-284">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine toohello other, toovalidate connectivity.</span></span>
13. <span data-ttu-id="92cc5-285">**選擇性**: toodelete hello 您在本教學課程中建立的資源，步驟完成 hello[刪除資源](#delete-powershell)本文中。</span><span class="sxs-lookup"><span data-stu-id="92cc5-285">**Optional**: toodelete hello resources that you create in this tutorial, complete hello steps in [Delete resources](#delete-powershell) in this article.</span></span>

## <span data-ttu-id="92cc5-286"><a name="permissions"></a>權限</span><span class="sxs-lookup"><span data-stu-id="92cc5-286"><a name="permissions"></a>Permissions</span></span>

<span data-ttu-id="92cc5-287">您使用的虛擬網路對等互連 toocreate hello 帳戶都必須 hello 必要的角色或權限。</span><span class="sxs-lookup"><span data-stu-id="92cc5-287">hello accounts you use toocreate a virtual network peering must have hello necessary role or permissions.</span></span> <span data-ttu-id="92cc5-288">例如，如果您已對等互連名為 myVnetA 和 myVnetB 的兩個虛擬網路，您的帳戶必須指派下列最小的角色或權限，每個虛擬網路的 hello:</span><span class="sxs-lookup"><span data-stu-id="92cc5-288">For example, if you were peering two virtual networks named myVnetA and myVnetB, your account must be assigned hello following minimum role or permissions for each virtual network:</span></span>
    
|<span data-ttu-id="92cc5-289">虛擬網路</span><span class="sxs-lookup"><span data-stu-id="92cc5-289">Virtual network</span></span>|<span data-ttu-id="92cc5-290">部署模型</span><span class="sxs-lookup"><span data-stu-id="92cc5-290">Deployment model</span></span>|<span data-ttu-id="92cc5-291">角色</span><span class="sxs-lookup"><span data-stu-id="92cc5-291">Role</span></span>|<span data-ttu-id="92cc5-292">權限</span><span class="sxs-lookup"><span data-stu-id="92cc5-292">Permissions</span></span>|
|---|---|---|---|
|<span data-ttu-id="92cc5-293">myVnetA</span><span class="sxs-lookup"><span data-stu-id="92cc5-293">myVnetA</span></span>|<span data-ttu-id="92cc5-294">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="92cc5-294">Resource Manager</span></span>|[<span data-ttu-id="92cc5-295">網路參與者</span><span class="sxs-lookup"><span data-stu-id="92cc5-295">Network Contributor</span></span>](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|<span data-ttu-id="92cc5-296">Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write</span><span class="sxs-lookup"><span data-stu-id="92cc5-296">Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write</span></span>|
| |<span data-ttu-id="92cc5-297">傳統</span><span class="sxs-lookup"><span data-stu-id="92cc5-297">Classic</span></span>|[<span data-ttu-id="92cc5-298">傳統網路參與者</span><span class="sxs-lookup"><span data-stu-id="92cc5-298">Classic Network Contributor</span></span>](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|<span data-ttu-id="92cc5-299">N/A</span><span class="sxs-lookup"><span data-stu-id="92cc5-299">N/A</span></span>|
|<span data-ttu-id="92cc5-300">myVnetB</span><span class="sxs-lookup"><span data-stu-id="92cc5-300">myVnetB</span></span>|<span data-ttu-id="92cc5-301">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="92cc5-301">Resource Manager</span></span>|[<span data-ttu-id="92cc5-302">網路參與者</span><span class="sxs-lookup"><span data-stu-id="92cc5-302">Network Contributor</span></span>](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|<span data-ttu-id="92cc5-303">Microsoft.Network/virtualNetworks/peer</span><span class="sxs-lookup"><span data-stu-id="92cc5-303">Microsoft.Network/virtualNetworks/peer</span></span>|
||<span data-ttu-id="92cc5-304">傳統</span><span class="sxs-lookup"><span data-stu-id="92cc5-304">Classic</span></span>|[<span data-ttu-id="92cc5-305">傳統網路參與者</span><span class="sxs-lookup"><span data-stu-id="92cc5-305">Classic Network Contributor</span></span>](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|<span data-ttu-id="92cc5-306">Microsoft.ClassicNetwork/virtualNetworks/peer</span><span class="sxs-lookup"><span data-stu-id="92cc5-306">Microsoft.ClassicNetwork/virtualNetworks/peer</span></span>|

<span data-ttu-id="92cc5-307">深入了解[內建角色](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)並指派特定權限太[自訂角色](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json)（資源管理員）。</span><span class="sxs-lookup"><span data-stu-id="92cc5-307">Learn more about [built-in roles](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) and assigning specific permissions too[custom roles](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (Resource Manager only).</span></span>

## <span data-ttu-id="92cc5-308"><a name="delete"></a>刪除資源</span><span class="sxs-lookup"><span data-stu-id="92cc5-308"><a name="delete"></a>Delete resources</span></span>
<span data-ttu-id="92cc5-309">當您完成本教學課程時，您可能想 toodelete hello 資源，您建立 hello 教學課程中，因此您不必承受使用費用。</span><span class="sxs-lookup"><span data-stu-id="92cc5-309">When you've finished this tutorial, you might want toodelete hello resources you created in hello tutorial, so you don't incur usage charges.</span></span> <span data-ttu-id="92cc5-310">刪除資源群組時，也會刪除 hello 資源群組中的所有資源。</span><span class="sxs-lookup"><span data-stu-id="92cc5-310">Deleting a resource group also deletes all resources that are in hello resource group.</span></span>

### <span data-ttu-id="92cc5-311"><a name="delete-portal"></a>Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="92cc5-311"><a name="delete-portal"></a>Azure portal</span></span>

1. <span data-ttu-id="92cc5-312">在 [hello] 入口網站搜尋方塊中，輸入**myResourceGroupA**。</span><span class="sxs-lookup"><span data-stu-id="92cc5-312">In hello portal search box, enter **myResourceGroupA**.</span></span> <span data-ttu-id="92cc5-313">在 hello 搜尋結果中，按一下  **myResourceGroupA**。</span><span class="sxs-lookup"><span data-stu-id="92cc5-313">In hello search results, click **myResourceGroupA**.</span></span>
2. <span data-ttu-id="92cc5-314">在 hello **myResourceGroupA**刀鋒視窗中，按一下 hello**刪除**圖示。</span><span class="sxs-lookup"><span data-stu-id="92cc5-314">On hello **myResourceGroupA** blade, click hello **Delete** icon.</span></span>
3. <span data-ttu-id="92cc5-315">tooconfirm hello 刪除、 hello**類型 hello 資源群組名稱**方塊中，輸入**myResourceGroupA**，然後按一下**刪除**。</span><span class="sxs-lookup"><span data-stu-id="92cc5-315">tooconfirm hello deletion, in hello **TYPE hello RESOURCE GROUP NAME** box, enter **myResourceGroupA**, and then click **Delete**.</span></span>
4. <span data-ttu-id="92cc5-316">在 hello**搜尋資源**方塊上方的 hello 入口網站中，型別 hello *myVnetB*。</span><span class="sxs-lookup"><span data-stu-id="92cc5-316">In hello **Search resources** box at hello top of hello portal, type *myVnetB*.</span></span> <span data-ttu-id="92cc5-317">按一下**myVnetB** hello 搜尋結果中出現。</span><span class="sxs-lookup"><span data-stu-id="92cc5-317">Click **myVnetB** when it appears in hello search results.</span></span> <span data-ttu-id="92cc5-318">刀鋒視窗會顯示 hello **myVnetB**虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="92cc5-318">A blade appears for hello **myVnetB** virtual network.</span></span>
5. <span data-ttu-id="92cc5-319">在 hello **myVnetB**刀鋒視窗中，按一下 **刪除**。</span><span class="sxs-lookup"><span data-stu-id="92cc5-319">In hello **myVnetB** blade, click **Delete**.</span></span>
6. <span data-ttu-id="92cc5-320">tooconfirm hello 刪除、 按一下**是**在 hello**刪除虛擬網路**方塊。</span><span class="sxs-lookup"><span data-stu-id="92cc5-320">tooconfirm hello deletion, click **Yes** in hello **Delete virtual network** box.</span></span>

### <span data-ttu-id="92cc5-321"><a name="delete-cli"></a>Azure CLI</span><span class="sxs-lookup"><span data-stu-id="92cc5-321"><a name="delete-cli"></a>Azure CLI</span></span>

1. <span data-ttu-id="92cc5-322">登入使用 hello tooAzure CLI 2.0 toodelete hello 虛擬網路 （資源管理員） 以 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="92cc5-322">Log in tooAzure using hello CLI 2.0 toodelete hello virtual network (Resource Manager) with hello following command:</span></span>

    ```azurecli-interactive
    az group delete --name myResourceGroupA --yes
    ```

2. <span data-ttu-id="92cc5-323">登入使用 hello tooAzure Azure CLI 1.0 toodelete hello 虛擬網路 （傳統） 以 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="92cc5-323">Log in tooAzure using hello Azure CLI 1.0 toodelete hello virtual network (classic) with hello following commands:</span></span>

    ```azurecli
    azure config mode asm 

    azure network vnet delete --vnet myVnetB --quiet
    ```

### <span data-ttu-id="92cc5-324"><a name="delete-powershell"></a>PowerShell</span><span class="sxs-lookup"><span data-stu-id="92cc5-324"><a name="delete-powershell"></a>PowerShell</span></span>

1. <span data-ttu-id="92cc5-325">Hello PowerShell 命令提示字元中輸入下列命令 toodelete hello 虛擬網路 （資源管理員） 的 hello:</span><span class="sxs-lookup"><span data-stu-id="92cc5-325">At hello PowerShell command prompt, enter hello following command toodelete hello virtual network (Resource Manager):</span></span>

    ```powershell
    Remove-AzureRmResourceGroup -Name myResourceGroupA -Force
    ```

2. <span data-ttu-id="92cc5-326">toodelete hello 虛擬網路 （傳統） 使用 PowerShell，您必須修改現有的網路組態檔。</span><span class="sxs-lookup"><span data-stu-id="92cc5-326">toodelete hello virtual network (classic) with PowerShell, you must modify an existing network configuration file.</span></span> <span data-ttu-id="92cc5-327">了解如何太[匯出、 更新和匯入網路組態檔](virtual-networks-using-network-configuration-file.md)。</span><span class="sxs-lookup"><span data-stu-id="92cc5-327">Learn how too[export, update, and import network configuration files](virtual-networks-using-network-configuration-file.md).</span></span> <span data-ttu-id="92cc5-328">移除下列 hello 這個教學課程中使用的虛擬網路的 VirtualNetworkSite 元素 hello:</span><span class="sxs-lookup"><span data-stu-id="92cc5-328">Remove hello following VirtualNetworkSite element for hello virtual network used in this tutorial:</span></span>

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
    > <span data-ttu-id="92cc5-329">匯入已變更的網路組態檔，可能會導致變更 tooexisting （傳統） 您的訂用帳戶中的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="92cc5-329">Importing a changed network configuration file can cause changes tooexisting virtual networks (classic) in your subscription.</span></span> <span data-ttu-id="92cc5-330">請務必僅卸除 hello 的上一個虛擬網路，且您不變更或移除您的訂用帳戶中的任何其他現有的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="92cc5-330">Ensure you only remove hello previous virtual network and that you don't change or remove any other existing virtual networks from your subscription.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="92cc5-331">後續步驟</span><span class="sxs-lookup"><span data-stu-id="92cc5-331">Next steps</span></span>

- <span data-ttu-id="92cc5-332">請先徹底熟悉重要[虛擬網路對等互連的條件約束和行為](virtual-network-manage-peering.md#requirements-and-constraints)，再建立虛擬網路對等互連以供生產環境使用。</span><span class="sxs-lookup"><span data-stu-id="92cc5-332">Thoroughly familiarize yourself with important [virtual network peering constraints and behaviors](virtual-network-manage-peering.md#requirements-and-constraints) before creating a virtual network peering for production use.</span></span>
- <span data-ttu-id="92cc5-333">了解所有[虛擬網路對等互連設定](virtual-network-manage-peering.md#create-a-peering)。</span><span class="sxs-lookup"><span data-stu-id="92cc5-333">Learn about all [virtual network peering settings](virtual-network-manage-peering.md#create-a-peering).</span></span>
- <span data-ttu-id="92cc5-334">了解如何太[建立中樞和支點網路拓樸](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering)與虛擬網路對等互連。</span><span class="sxs-lookup"><span data-stu-id="92cc5-334">Learn how too[create a hub and spoke network topology](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) with virtual network peering.</span></span>
