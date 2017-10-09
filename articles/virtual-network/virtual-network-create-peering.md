---
title: "Azure 虛擬網路對等互連-aaaCreate 資源管理員的相同訂用帳戶 |Microsoft 文件"
description: "了解如何 toocreate 虛擬網路對等虛擬網路之間透過 Resource Manager 建立存在於 hello 相同 Azure 訂用帳戶。"
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 026bca75-2946-4c03-b4f6-9f3c5809c69a
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/17/2017
ms.author: jdial;narayan;annahar
ms.openlocfilehash: c2d24fdc8103c09c3bfb8e59be12e301d9e9a55a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-peering---resource-manager-same-subscription"></a><span data-ttu-id="93a61-103">建立虛擬網路對等互連 - Resource Manager，相同訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="93a61-103">Create a virtual network peering - Resource Manager, same subscription</span></span>

<span data-ttu-id="93a61-104">在此教學課程中，您學會 toocreate 虛擬網路透過 Resource Manager 建立的虛擬網路之間的對等互連。</span><span class="sxs-lookup"><span data-stu-id="93a61-104">In this tutorial, you learn toocreate a virtual network peering between virtual networks created through Resource Manager.</span></span> <span data-ttu-id="93a61-105">這兩個虛擬網路中存在 hello 相同訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="93a61-105">Both virtual networks exist in hello same subscription.</span></span> <span data-ttu-id="93a61-106">在不同的虛擬網路 toocommunicate 彼此具有對等兩個虛擬網路可讓資源 hello 相同的頻寬和延遲好像 hello 資源是在 hello 相同虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="93a61-106">Peering two virtual networks enables resources in different virtual networks toocommunicate with each other with hello same bandwidth and latency as though hello resources were in hello same virtual network.</span></span> <span data-ttu-id="93a61-107">深入了解[虛擬網路對等互連](virtual-network-peering-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="93a61-107">Learn more about [Virtual network peering](virtual-network-peering-overview.md).</span></span> 

<span data-ttu-id="93a61-108">hello 步驟 toocreate 虛擬網路對等互連會有所不同，hello 虛擬網路是否有相同，或不同的 hello、 訂用帳戶及其中[Azure 部署模型](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json)建立 hello 虛擬網路透過。</span><span class="sxs-lookup"><span data-stu-id="93a61-108">hello steps toocreate a virtual network peering are different, depending on whether hello virtual networks are in hello same, or different, subscriptions, and which [Azure deployment model](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) hello virtual networks are created through.</span></span> <span data-ttu-id="93a61-109">了解 toocreate 的虛擬網路在其他情況下，即可從下表中的 hello hello 案例對等互連的方式：</span><span class="sxs-lookup"><span data-stu-id="93a61-109">Learn how toocreate a virtual network peering in other scenarios by clicking hello scenario from hello following table:</span></span>

|<span data-ttu-id="93a61-110">Azure 部署模型</span><span class="sxs-lookup"><span data-stu-id="93a61-110">Azure deployment model</span></span>  | <span data-ttu-id="93a61-111">Azure 訂閱</span><span class="sxs-lookup"><span data-stu-id="93a61-111">Azure subscription</span></span>  |
|--------- |---------|
|[<span data-ttu-id="93a61-112">兩者皆使用 Resource Manager</span><span class="sxs-lookup"><span data-stu-id="93a61-112">Both Resource Manager</span></span>](create-peering-different-subscriptions.md) |<span data-ttu-id="93a61-113">不同</span><span class="sxs-lookup"><span data-stu-id="93a61-113">Different</span></span>|
|[<span data-ttu-id="93a61-114">一個使用 Resource Manager、一個使用傳統部署模型</span><span class="sxs-lookup"><span data-stu-id="93a61-114">One Resource Manager, one classic</span></span>](create-peering-different-deployment-models.md) |<span data-ttu-id="93a61-115">相同</span><span class="sxs-lookup"><span data-stu-id="93a61-115">Same</span></span>|
|[<span data-ttu-id="93a61-116">一個使用 Resource Manager、一個使用傳統部署模型</span><span class="sxs-lookup"><span data-stu-id="93a61-116">One Resource Manager, one classic</span></span>](create-peering-different-deployment-models-subscriptions.md) |<span data-ttu-id="93a61-117">不同</span><span class="sxs-lookup"><span data-stu-id="93a61-117">Different</span></span>|

<span data-ttu-id="93a61-118">無法透過 hello 傳統部署模型所部署的兩個虛擬網路之間建立的虛擬網路對等互連。</span><span class="sxs-lookup"><span data-stu-id="93a61-118">A virtual network peering cannot be created between two virtual networks deployed through hello classic deployment model.</span></span> <span data-ttu-id="93a61-119">虛擬網路對等互連只能建立兩個存在於 hello 相同的虛擬網路之間的 Azure 區域。</span><span class="sxs-lookup"><span data-stu-id="93a61-119">A virtual network peering can only be created between two virtual networks that exist in hello same Azure region.</span></span> <span data-ttu-id="93a61-120">如果您需要同時建立透過 hello 傳統部署模型，或存在於不同的 Azure 地區 tooconnect 虛擬網路，您可以使用 Azure [VPN 閘道](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json)tooconnect hello 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="93a61-120">If you need tooconnect virtual networks that were both created through hello classic deployment model, or that exist in different Azure regions, you can use an Azure [VPN Gateway](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) tooconnect hello virtual networks.</span></span> 

<span data-ttu-id="93a61-121">您可以使用 hello [Azure 入口網站](#portal)，hello Azure[命令列介面](#cli)(CLI)，Azure [PowerShell](#powershell)，或[Azure Resource Manager 範本](#template) toocreate 虛擬網路對等互連。</span><span class="sxs-lookup"><span data-stu-id="93a61-121">You can use hello [Azure portal](#portal), hello Azure [command-line interface](#cli) (CLI), Azure [PowerShell](#powershell), or an [Azure Resource Manager template](#template) toocreate a virtual network peering.</span></span> <span data-ttu-id="93a61-122">直接 toohello 一個步驟建立的虛擬網路對等互連使用您選擇的工具，請按一下任何先前工具連結 toogo hello。</span><span class="sxs-lookup"><span data-stu-id="93a61-122">Click any of hello previous tool links toogo directly toohello steps for creating a virtual network peering using your tool of choice.</span></span>

## <span data-ttu-id="93a61-123"><a name="portal"></a>建立對等互連 - Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="93a61-123"><a name="portal"></a>Create peering - Azure portal</span></span>

1. <span data-ttu-id="93a61-124">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="93a61-124">Log in toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="93a61-125">登入的 hello 帳戶必須具有 hello 必要的權限 toocreate 虛擬網路對等互連。</span><span class="sxs-lookup"><span data-stu-id="93a61-125">hello account you log in with must have hello necessary permissions toocreate a virtual network peering.</span></span> <span data-ttu-id="93a61-126">請參閱 hello[權限](#permissions)本文，如需詳細資訊一節。</span><span class="sxs-lookup"><span data-stu-id="93a61-126">See hello [Permissions](#permissions) section of this article for details.</span></span>
2. <span data-ttu-id="93a61-127">依序按一下 [新增]、[網路] 及 [虛擬網路]。</span><span class="sxs-lookup"><span data-stu-id="93a61-127">Click **+ New**, click **Networking**, then click **Virtual network**.</span></span>
3. <span data-ttu-id="93a61-128">在 hello**建立虛擬網路**刀鋒視窗中，輸入，或選取值 hello 下列設定，然後按一下 **建立**:</span><span class="sxs-lookup"><span data-stu-id="93a61-128">In hello **Create virtual network** blade, enter, or select values for hello following settings, then click **Create**:</span></span>
    - <span data-ttu-id="93a61-129">**名稱**：*myVnet1*</span><span class="sxs-lookup"><span data-stu-id="93a61-129">**Name**: *myVnet1*</span></span>
    - <span data-ttu-id="93a61-130">**位址空間**：*10.0.0.0/16*</span><span class="sxs-lookup"><span data-stu-id="93a61-130">**Address space**: *10.0.0.0/16*</span></span>
    - <span data-ttu-id="93a61-131">**子網路名稱**：*預設值*</span><span class="sxs-lookup"><span data-stu-id="93a61-131">**Subnet name**: *default*</span></span>
    - <span data-ttu-id="93a61-132">**子網路位址範圍**：*10.0.0.0/24*</span><span class="sxs-lookup"><span data-stu-id="93a61-132">**Subnet address range**: *10.0.0.0/24*</span></span>
    - <span data-ttu-id="93a61-133">**訂用帳戶**︰選取您的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="93a61-133">**Subscription**: Select your subscription</span></span>
    - <span data-ttu-id="93a61-134">**資源群組**：選取 [新建] 並輸入 *myResourceGroup*</span><span class="sxs-lookup"><span data-stu-id="93a61-134">**Resource group**: Select **Create new** and enter *myResourceGroup*</span></span>
    - <span data-ttu-id="93a61-135">**位置**：*美國東部*</span><span class="sxs-lookup"><span data-stu-id="93a61-135">**Location**: *East US*</span></span>
4. <span data-ttu-id="93a61-136">完成步驟 2-3 再次指定 hello 遵循步驟 3 中的值：</span><span class="sxs-lookup"><span data-stu-id="93a61-136">Complete steps 2-3 again specifying hello following values in step 3:</span></span>
    - <span data-ttu-id="93a61-137">**名稱**： *myVnet2*</span><span class="sxs-lookup"><span data-stu-id="93a61-137">**Name**: *myVnet2*</span></span>
    - <span data-ttu-id="93a61-138">**位址空間**：*10.1.0.0/16*</span><span class="sxs-lookup"><span data-stu-id="93a61-138">**Address space**: *10.1.0.0/16*</span></span>
    - <span data-ttu-id="93a61-139">**子網路名稱**：*預設值*</span><span class="sxs-lookup"><span data-stu-id="93a61-139">**Subnet name**: *default*</span></span>
    - <span data-ttu-id="93a61-140">**子網路位址範圍**：*10.1.0.0/24*</span><span class="sxs-lookup"><span data-stu-id="93a61-140">**Subnet address range**: *10.1.0.0/24*</span></span>
    - <span data-ttu-id="93a61-141">**訂用帳戶**︰選取您的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="93a61-141">**Subscription**: Select your subscription</span></span>
    - <span data-ttu-id="93a61-142">**資源群組**：選取 [使用現有] 並選取 *myResourceGroup*</span><span class="sxs-lookup"><span data-stu-id="93a61-142">**Resource group**: Select **Use existing** and select *myResourceGroup*</span></span>
    - <span data-ttu-id="93a61-143">**位置**：*美國東部*</span><span class="sxs-lookup"><span data-stu-id="93a61-143">**Location**: *East US*</span></span>
5. <span data-ttu-id="93a61-144">在 hello**搜尋資源**方塊上方的 hello 入口網站中，型別 hello *myResourceGroup*。</span><span class="sxs-lookup"><span data-stu-id="93a61-144">In hello **Search resources** box at hello top of hello portal, type *myResourceGroup*.</span></span> <span data-ttu-id="93a61-145">按一下**myResourceGroup** hello 搜尋結果中出現。</span><span class="sxs-lookup"><span data-stu-id="93a61-145">Click **myResourceGroup** when it appears in hello search results.</span></span> <span data-ttu-id="93a61-146">刀鋒視窗會顯示 hello **myresourcegroup**資源群組。</span><span class="sxs-lookup"><span data-stu-id="93a61-146">A blade appears for hello **myresourcegroup** resource group.</span></span> <span data-ttu-id="93a61-147">hello 資源群組包含兩個 hello 前述步驟中建立虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="93a61-147">hello resource group contains hello two virtual networks created in previous steps.</span></span>
6. <span data-ttu-id="93a61-148">按一下 [myVNet1]。</span><span class="sxs-lookup"><span data-stu-id="93a61-148">Click **myVNet1**.</span></span>
7. <span data-ttu-id="93a61-149">在 [hello **myVnet1**刀鋒視窗中，按一下**對等互連**從 hello 垂直 hello 左邊的 hello] 刀鋒視窗上的選項清單。</span><span class="sxs-lookup"><span data-stu-id="93a61-149">In hello **myVnet1** blade that appears, click **Peerings** from hello vertical list of options on hello left side of hello blade.</span></span>
8. <span data-ttu-id="93a61-150">在 hello **myVnet1-對等互連**刀鋒視窗中出現，按一下**+ 新增**</span><span class="sxs-lookup"><span data-stu-id="93a61-150">In hello **myVnet1 - Peerings** blade that appeared, click **+ Add**</span></span>
9. <span data-ttu-id="93a61-151">在 hello**新增對等互連**刀鋒視窗中，輸入，或選取 hello 下列選項，然後按一下 **確定**:</span><span class="sxs-lookup"><span data-stu-id="93a61-151">In hello **Add peering** blade that appears, enter, or select hello following options, then click **OK**:</span></span>
     - <span data-ttu-id="93a61-152">**名稱**：*myVnet1ToMyVnet2*</span><span class="sxs-lookup"><span data-stu-id="93a61-152">**Name**: *myVnet1ToMyVnet2*</span></span>
     - <span data-ttu-id="93a61-153">**虛擬網路部署模型**：選取 [Resource Manager]。</span><span class="sxs-lookup"><span data-stu-id="93a61-153">**Virtual network deployment model**:  Select **Resource Manager**.</span></span> 
     - <span data-ttu-id="93a61-154">**訂用帳戶**︰選取您的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="93a61-154">**Subscription**: Select your subscription</span></span>
     - <span data-ttu-id="93a61-155">**虛擬網路**：按一下 [選擇虛擬網路]，然後按一下 [myVnet2]。</span><span class="sxs-lookup"><span data-stu-id="93a61-155">**Virtual network**:  Click **Choose a virtual network**, then click **myVnet2**.</span></span>
     - <span data-ttu-id="93a61-156">**允許虛擬網路存取**：確定已選取 [啟用]。</span><span class="sxs-lookup"><span data-stu-id="93a61-156">**Allow virtual network access:** Ensure that **Enabled** is selected.</span></span>
    <span data-ttu-id="93a61-157">本教學課程中不會使用其他設定。</span><span class="sxs-lookup"><span data-stu-id="93a61-157">No other settings are used in this tutorial.</span></span> <span data-ttu-id="93a61-158">讀取所有的對等設定的相關 toolearn[管理虛擬網路對等互連](virtual-network-manage-peering.md#create-a-peering)。</span><span class="sxs-lookup"><span data-stu-id="93a61-158">toolearn about all peering settings, read [Manage virtual network peerings](virtual-network-manage-peering.md#create-a-peering).</span></span>
10. <span data-ttu-id="93a61-159">按一下後**[確定]** hello 先前步驟中，在 hello**新增對等互連**刀鋒視窗會關閉，而且您會看見 hello **myVnet1-對等互連**刀鋒視窗一次。</span><span class="sxs-lookup"><span data-stu-id="93a61-159">After clicking **OK** in hello previous step, hello **Add peering** blade closes and you see hello **myVnet1 - Peerings** blade again.</span></span> <span data-ttu-id="93a61-160">幾秒之後，對等互連您所建立的 hello 會出現在 [hello] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="93a61-160">After a few seconds, hello peering you created appears in hello blade.</span></span> <span data-ttu-id="93a61-161">**起始**會列在 hello**對等互連狀態**hello 的資料行**myVnet1ToMyVnet2**對等互連您建立。</span><span class="sxs-lookup"><span data-stu-id="93a61-161">**Initiated** is listed in hello **PEERING STATUS** column for hello **myVnet1ToMyVnet2** peering you created.</span></span> <span data-ttu-id="93a61-162">您已所以 Vnet1 tooVnet2，但現在 myVnet2 toomyVnet1 必須對等。</span><span class="sxs-lookup"><span data-stu-id="93a61-162">You've peered Vnet1 tooVnet2, but now you must peer myVnet2 toomyVnet1.</span></span> <span data-ttu-id="93a61-163">對等互連 hello 必須建立兩個方向 hello 虛擬網路 toocommunicate tooenable 資源彼此。</span><span class="sxs-lookup"><span data-stu-id="93a61-163">hello peering must be created in both directions tooenable resources in hello virtual networks toocommunicate with each other.</span></span>
11. <span data-ttu-id="93a61-164">針對 myVnet2 再次完成步驟 5-10。</span><span class="sxs-lookup"><span data-stu-id="93a61-164">Complete steps 5-10 again for myVnet2.</span></span>  <span data-ttu-id="93a61-165">名稱 hello 對等互連*myVnet2ToMyVnet1*。</span><span class="sxs-lookup"><span data-stu-id="93a61-165">Name hello peering *myVnet2ToMyVnet1*.</span></span>
12. <span data-ttu-id="93a61-166">幾秒鐘後按一下**[確定]** toocreate hello 對等 MyVnet2，hello **myVnet2ToMyVnet1**對等互連您剛建立列為**已連接**hello中**對等互連狀態**資料行。</span><span class="sxs-lookup"><span data-stu-id="93a61-166">A few seconds after clicking **OK** toocreate hello peering for MyVnet2, hello **myVnet2ToMyVnet1** peering you just created is listed with **Connected** in hello **PEERING STATUS** column.</span></span>
13. <span data-ttu-id="93a61-167">針對 MyVnet1 再次完成步驟 5-7。</span><span class="sxs-lookup"><span data-stu-id="93a61-167">Complete steps 5-7 again for MyVnet1.</span></span> <span data-ttu-id="93a61-168">hello**對等互連狀態**hello **myVnet1ToVNet2**對等互連現在也是**Connected**。</span><span class="sxs-lookup"><span data-stu-id="93a61-168">hello **PEERING STATUS** for hello **myVnet1ToVNet2** peering is now also **Connected**.</span></span> <span data-ttu-id="93a61-169">之後您會看到 hello 對等互連已成功建立**Connected**在 hello**對等互連狀態**中 hello 對等互連這兩個虛擬網路的資料行。</span><span class="sxs-lookup"><span data-stu-id="93a61-169">hello peering is successfully established after you see **Connected** in hello **PEERING STATUS** column for both virtual networks in hello peering.</span></span>
14. <span data-ttu-id="93a61-170">**選擇性**： 未涵蓋在本教學課程中建立虛擬機器，雖然您可以在每個虛擬網路中建立虛擬機器，並從一個虛擬機器 toohello 其他 toovalidate 連線連接。</span><span class="sxs-lookup"><span data-stu-id="93a61-170">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine toohello other, toovalidate connectivity.</span></span>
15. <span data-ttu-id="93a61-171">**選擇性**: toodelete hello 您在本教學課程中建立的資源，hello 步驟完成 hello[刪除資源](#delete-portal)本文一節。</span><span class="sxs-lookup"><span data-stu-id="93a61-171">**Optional**: toodelete hello resources that you create in this tutorial, complete hello steps in hello [Delete resources](#delete-portal) section of this article.</span></span>

<span data-ttu-id="93a61-172">所建立的其中一個虛擬網路中任何 Azure 資源，現在都能 toocommunicate 彼此透過其 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="93a61-172">Any Azure resources you create in either virtual network are now able toocommunicate with each other through their IP addresses.</span></span> <span data-ttu-id="93a61-173">如果您使用預設 Azure 名稱解析為 hello 虛擬網路，hello hello 虛擬網路中沒有資源無法 tooresolve 名稱在 hello 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="93a61-173">If you're using default Azure name resolution for hello virtual networks, hello resources in hello virtual networks are not able tooresolve names across hello virtual networks.</span></span> <span data-ttu-id="93a61-174">如果您想 tooresolve 名稱多個虛擬網路中的對等互連，您必須建立您自己的 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="93a61-174">If you want tooresolve names across virtual networks in a peering, you must create your own DNS server.</span></span> <span data-ttu-id="93a61-175">深入了解如何註冊 tooset[使用您自己的 DNS 伺服器的名稱解析](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server)。</span><span class="sxs-lookup"><span data-stu-id="93a61-175">Learn how tooset up [Name resolution using your own DNS server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span></span>

## <span data-ttu-id="93a61-176"><a name="cli"></a>建立對等互連 - Azure CLI</span><span class="sxs-lookup"><span data-stu-id="93a61-176"><a name="cli"></a>Create peering - Azure CLI</span></span>

<span data-ttu-id="93a61-177">下列指令碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="93a61-177">hello following script:</span></span>

- <span data-ttu-id="93a61-178">需要 hello Azure CLI 版本 2.0.4 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="93a61-178">Requires hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="93a61-179">toofind hello 版本，執行 hello`az --version`命令。</span><span class="sxs-lookup"><span data-stu-id="93a61-179">toofind hello version, run hello `az --version` command.</span></span> <span data-ttu-id="93a61-180">如果您需要 tooupgrade，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="93a61-180">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
- <span data-ttu-id="93a61-181">適用於 Bash 殼層。</span><span class="sxs-lookup"><span data-stu-id="93a61-181">Works in a Bash shell.</span></span> <span data-ttu-id="93a61-182">在 Windows 用戶端上執行 Azure CLI 指令碼選項，請參閱[Windows 中執行 hello Azure CLI](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="93a61-182">For options on running Azure CLI scripts on Windows client, see [Running hello Azure CLI in Windows](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> 

<span data-ttu-id="93a61-183">而不是安裝 hello CLI 和其相依性，您可以使用 hello Azure 雲端殼層。</span><span class="sxs-lookup"><span data-stu-id="93a61-183">Instead of installing hello CLI and its dependencies, you can use hello Azure Cloud Shell.</span></span> <span data-ttu-id="93a61-184">hello Azure 雲端殼層是免費的 Bash 殼層，您可以直接在 hello Azure 入口網站中執行。</span><span class="sxs-lookup"><span data-stu-id="93a61-184">hello Azure Cloud Shell is a free Bash shell that you can run directly within hello Azure portal.</span></span> <span data-ttu-id="93a61-185">它有的 hello Azure CLI 預先安裝和設定 toouse 與您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="93a61-185">It has hello Azure CLI preinstalled and configured toouse with your account.</span></span> <span data-ttu-id="93a61-186">按一下 hello**試試**按鈕，如下所示，記錄您的雲端殼層會叫用來登入 tooyour hello 指令碼中使用的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="93a61-186">Click hello **Try it** button in hello script that follows, which invokes a Cloud Shell that logs you can log in tooyour Azure account with.</span></span> <span data-ttu-id="93a61-187">tooexecute hello 指令碼中，按一下 hello**複製**按鈕，然後將 hello 內容貼到您的雲端 Shell。</span><span class="sxs-lookup"><span data-stu-id="93a61-187">tooexecute hello script, click hello **Copy** button and paste hello contents into your Cloud Shell.</span></span>

1. <span data-ttu-id="93a61-188">建立一個資源群組和兩個虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="93a61-188">Create a resource group and two virtual networks.</span></span>

    ```azurecli-interactive
    #!/bin/bash

    # Variables for common values used throughout hello script.
    rgName="myResourceGroup"
    location="eastus"

    # Create a resource group.
    az group create \
      --name $rgName \
      --location $location

    # Create virtual network 1.
    az network vnet create \
      --name myVnet1 \
      --resource-group $rgName \
      --location $location \
      --address-prefix 10.0.0.0/16

    # Create virtual network 2.
    az network vnet create \
      --name myVnet2 \
      --resource-group $rgName \
      --location $location \
      --address-prefix 10.1.0.0/16
    ```

2. <span data-ttu-id="93a61-189">建立對等互連 hello 兩個虛擬網路之間的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="93a61-189">Create a virtual network peering between hello two virtual networks.</span></span>
 
    ```azurecli-interactive
    # Get hello id for VNet1.
    vnet1Id=$(az network vnet show \
      --resource-group $rgName \
      --name myVnet1 \
      --query id --out tsv)

    # Get hello id for VNet2.
    vnet2Id=$(az network vnet show \
      --resource-group $rgName \
      --name myVnet2 \
      --query id \
      --out tsv)

    # Peer VNet1 tooVNet2.
    az network vnet peering create \
      --name myVnet1ToMyVnet2 \
      --resource-group $rgName \
      --vnet-name myVnet1 \
      --remote-vnet-id $vnet2Id \
      --allow-vnet-access

    # Peer VNet2 tooVNet1.
    az network vnet peering create \
      --name myVnet2ToMyVnet1 \
      --resource-group $rgName \
      --vnet-name myVnet2 \
      --remote-vnet-id $vnet1Id \
      --allow-vnet-access
    ```

3. <span data-ttu-id="93a61-190">Hello 指令碼執行之後，請檢閱每個虛擬網路的對等互連 hello。</span><span class="sxs-lookup"><span data-stu-id="93a61-190">After hello script executes, review hello peerings for each virtual network.</span></span> 

    ```azurecli-interactive
    az network vnet peering list \
      --resource-group myResourceGroup \
      --vnet-name myVnet1 \
      --output table
    ```
    
    <span data-ttu-id="93a61-191">Hello 之前再次執行命令，取代*myVnet1*與*myVnet2*。</span><span class="sxs-lookup"><span data-stu-id="93a61-191">Run hello previous command again, replacing *myVnet1* with *myVnet2*.</span></span> <span data-ttu-id="93a61-192">hello 輸出兩個命令顯示**Connected**在 hello **PeeringState**資料行。</span><span class="sxs-lookup"><span data-stu-id="93a61-192">hello output of both commands shows **Connected** in hello **PeeringState** column.</span></span>

     <span data-ttu-id="93a61-193">所建立的其中一個虛擬網路中任何 Azure 資源，現在都能 toocommunicate 彼此透過其 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="93a61-193">Any Azure resources you create in either virtual network are now able toocommunicate with each other through their IP addresses.</span></span> <span data-ttu-id="93a61-194">如果您使用預設 Azure 名稱解析為 hello 虛擬網路，hello hello 虛擬網路中沒有資源無法 tooresolve 名稱在 hello 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="93a61-194">If you're using default Azure name resolution for hello virtual networks, hello resources in hello virtual networks are not able tooresolve names across hello virtual networks.</span></span> <span data-ttu-id="93a61-195">如果您想 tooresolve 名稱多個虛擬網路中的對等互連，您必須建立您自己的 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="93a61-195">If you want tooresolve names across virtual networks in a peering, you must create your own DNS server.</span></span> <span data-ttu-id="93a61-196">深入了解如何註冊 tooset[使用您自己的 DNS 伺服器的名稱解析](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server)。</span><span class="sxs-lookup"><span data-stu-id="93a61-196">Learn how tooset up [Name resolution using your own DNS server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span></span>

4. <span data-ttu-id="93a61-197">**選擇性**： 未涵蓋在本教學課程中建立虛擬機器，雖然您可以在每個虛擬網路中建立虛擬機器，並從一個虛擬機器 toohello 其他 toovalidate 連線連接。</span><span class="sxs-lookup"><span data-stu-id="93a61-197">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine toohello other, toovalidate connectivity.</span></span>
5. <span data-ttu-id="93a61-198">**選擇性**: toodelete hello 您在本教學課程中建立的資源，步驟完成 hello[刪除資源](#delete-cli)本文中。</span><span class="sxs-lookup"><span data-stu-id="93a61-198">**Optional**: toodelete hello resources that you create in this tutorial, complete hello steps in [Delete resources](#delete-cli) in this article.</span></span>


## <span data-ttu-id="93a61-199"><a name="powershell"></a>建立對等互連 - PowerShell</span><span class="sxs-lookup"><span data-stu-id="93a61-199"><a name="powershell"></a>Create peering - PowerShell</span></span>

1. <span data-ttu-id="93a61-200">安裝 hello hello PowerShell 最新版本[AzureRm](https://www.powershellgallery.com/packages/AzureRM/)模組。</span><span class="sxs-lookup"><span data-stu-id="93a61-200">Install hello latest version of hello PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) module.</span></span> <span data-ttu-id="93a61-201">如果您是新 tooAzure PowerShell，請參閱[Azure PowerShell 概觀](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="93a61-201">If you're new tooAzure PowerShell, see [Azure PowerShell overview](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="93a61-202">toostart PowerShell 工作階段，跳過**啟動**，輸入**powershell**，然後按一下 **PowerShell**。</span><span class="sxs-lookup"><span data-stu-id="93a61-202">toostart a PowerShell session, go too**Start**, enter **powershell**, and then click **PowerShell**.</span></span>
3. <span data-ttu-id="93a61-203">在 PowerShell 中，登入 tooAzure 輸入 hello`login-azurermaccount`命令。</span><span class="sxs-lookup"><span data-stu-id="93a61-203">In PowerShell, log in tooAzure by entering hello `login-azurermaccount` command.</span></span> <span data-ttu-id="93a61-204">登入的 hello 帳戶必須具有 hello 必要的權限 toocreate 虛擬網路對等互連。</span><span class="sxs-lookup"><span data-stu-id="93a61-204">hello account you log in with must have hello necessary permissions toocreate a virtual network peering.</span></span> <span data-ttu-id="93a61-205">請參閱 hello[權限](#permissions)本文，如需詳細資訊一節。</span><span class="sxs-lookup"><span data-stu-id="93a61-205">See hello [Permissions](#permissions) section of this article for details.</span></span>
4. <span data-ttu-id="93a61-206">建立一個資源群組和兩個虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="93a61-206">Create a resource group and two virtual networks.</span></span> <span data-ttu-id="93a61-207">tooexecute hello 指令碼中，複製 hello 下列指令碼，將它貼到 PowerShell，然後按`Enter`囉 」 畫面上出現 hello 最後一行之後：</span><span class="sxs-lookup"><span data-stu-id="93a61-207">tooexecute hello script, copy hello following script, paste it into PowerShell, and then press `Enter` after hello last line appears on hello screen:</span></span>

    ```powershell
    # Variables for common values used throughout hello script.
    $rgName='myResourceGroup'
    $location='eastus'

    # Create a resource group.
    New-AzureRmResourceGroup `
      -Name $rgName `
      -Location $location

    # Create virtual network 1.
    $vnet1 = New-AzureRmVirtualNetwork `
      -ResourceGroupName $rgName `
      -Name 'myVnet1' `
      -AddressPrefix '10.0.0.0/16' `
      -Location $location

    # Create virtual network 2.
    $vnet2 = New-AzureRmVirtualNetwork `
      -ResourceGroupName $rgName `
      -Name 'myVnet2' `
      -AddressPrefix '10.1.0.0/16' `
      -Location $location
    ```

5. <span data-ttu-id="93a61-208">建立對等互連 hello 兩個虛擬網路之間的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="93a61-208">Create a virtual network peering between hello two virtual networks.</span></span> <span data-ttu-id="93a61-209">複製 hello 下列指令碼，在 tooPowerShell，貼上，然後按`Enter`囉 」 畫面上出現 hello 最後一行之後：</span><span class="sxs-lookup"><span data-stu-id="93a61-209">Copy hello following script, paste in tooPowerShell, and then press `Enter` after hello last line appears on hello screen:</span></span>
    ```powershell
    # Peer VNet1 tooVNet2.
    Add-AzureRmVirtualNetworkPeering `
      -Name 'myVnet1ToMyVnet2' `
      -VirtualNetwork $vnet1 `
      -RemoteVirtualNetworkId $vnet2.Id

    # Peer VNet2 tooVNet1.
    Add-AzureRmVirtualNetworkPeering `
      -Name 'myVnet2ToMyVnet1' `
      -VirtualNetwork $vnet2 `
      -RemoteVirtualNetworkId $vnet1.Id
    ```
6. <span data-ttu-id="93a61-210">tooreview hello 子網路的 hello 虛擬網路，複本 hello 下列命令，在 tooPowerShell，貼上，然後按`Enter`:</span><span class="sxs-lookup"><span data-stu-id="93a61-210">tooreview hello subnets for hello virtual network, copy hello following command, paste in tooPowerShell, and then press `Enter`:</span></span>

    ```powershell
    Get-AzureRmVirtualNetworkPeering `
      -ResourceGroupName myResourceGroup `
      -VirtualNetworkName myVnet1 `
      | Format-Table VirtualNetworkName, PeeringState
    ```

    <span data-ttu-id="93a61-211">Hello 之前再次執行命令，取代*myVnet1*與*myVnet2*。</span><span class="sxs-lookup"><span data-stu-id="93a61-211">Run hello previous command again, replacing *myVnet1* with *myVnet2*.</span></span> <span data-ttu-id="93a61-212">hello 輸出兩個命令顯示**Connected**在 hello **PeeringState**資料行。</span><span class="sxs-lookup"><span data-stu-id="93a61-212">hello output of both commands shows **Connected** in hello **PeeringState** column.</span></span>
7. <span data-ttu-id="93a61-213">**選擇性**： 未涵蓋在本教學課程中建立虛擬機器，雖然您可以在每個虛擬網路中建立虛擬機器，並從一個虛擬機器 toohello 其他 toovalidate 連線連接。</span><span class="sxs-lookup"><span data-stu-id="93a61-213">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine toohello other, toovalidate connectivity.</span></span>
8. <span data-ttu-id="93a61-214">**選擇性**: toodelete hello 您在本教學課程中建立的資源，步驟完成 hello[刪除資源](#delete-powershell)本文中。</span><span class="sxs-lookup"><span data-stu-id="93a61-214">**Optional**: toodelete hello resources that you create in this tutorial, complete hello steps in [Delete resources](#delete-powershell) in this article.</span></span>

<span data-ttu-id="93a61-215">所建立的其中一個虛擬網路中任何 Azure 資源，現在都能 toocommunicate 彼此透過其 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="93a61-215">Any Azure resources you create in either virtual network are now able toocommunicate with each other through their IP addresses.</span></span> <span data-ttu-id="93a61-216">如果您使用預設 Azure 名稱解析為 hello 虛擬網路，hello hello 虛擬網路中沒有資源無法 tooresolve 名稱在 hello 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="93a61-216">If you're using default Azure name resolution for hello virtual networks, hello resources in hello virtual networks are not able tooresolve names across hello virtual networks.</span></span> <span data-ttu-id="93a61-217">如果您想 tooresolve 名稱多個虛擬網路中的對等互連，您必須建立您自己的 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="93a61-217">If you want tooresolve names across virtual networks in a peering, you must create your own DNS server.</span></span> <span data-ttu-id="93a61-218">深入了解如何註冊 tooset[使用您自己的 DNS 伺服器的名稱解析](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server)。</span><span class="sxs-lookup"><span data-stu-id="93a61-218">Learn how tooset up [Name resolution using your own DNS server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span></span>

## <span data-ttu-id="93a61-219"><a name="template"></a>建立對等互連 - Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="93a61-219"><a name="template"></a>Create peering - Resource Manager template</span></span>

1. <span data-ttu-id="93a61-220">參考[建立虛擬網路對等互連](https://azure.microsoft.com/resources/templates/201-vnet-to-vnet-peering) Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="93a61-220">Reference [Create a virtual network peering](https://azure.microsoft.com/resources/templates/201-vnet-to-vnet-peering) Resource Manager template.</span></span> <span data-ttu-id="93a61-221">指示會提供搭配 hello 範本部署 hello 範本使用 hello Azure 入口網站、 PowerShell 或 hello Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="93a61-221">Instructions are provided with hello template for deploying hello template using hello Azure portal, PowerShell, or hello Azure CLI.</span></span> <span data-ttu-id="93a61-222">登入您選擇使用的帳戶具有 toodeploy hello 範本 toowhichever 工具 hello toocreate 必要的權限的虛擬網路對等互連。</span><span class="sxs-lookup"><span data-stu-id="93a61-222">Log in toowhichever tool you choose toodeploy hello template with using an account that has hello necessary permissions toocreate a virtual network peering.</span></span> <span data-ttu-id="93a61-223">請參閱 hello[權限](#permissions)本文，如需詳細資訊一節。</span><span class="sxs-lookup"><span data-stu-id="93a61-223">See hello [Permissions](#permissions) section of this article for details.</span></span>
2. <span data-ttu-id="93a61-224">**選擇性**： 未涵蓋在本教學課程中建立虛擬機器，雖然您可以在每個虛擬網路中建立虛擬機器，並從一個虛擬機器 toohello 其他 toovalidate 連線連接。</span><span class="sxs-lookup"><span data-stu-id="93a61-224">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine toohello other, toovalidate connectivity.</span></span>
3. <span data-ttu-id="93a61-225">**選擇性**: toodelete hello 您在本教學課程中建立的資源，hello 步驟完成 hello[刪除資源](#delete)> 一節的本文中，使用 hello Azure 入口網站、 PowerShell 或 hello Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="93a61-225">**Optional**: toodelete hello resources that you create in this tutorial, complete hello steps in hello [Delete resources](#delete) section of this article, using either hello Azure portal, PowerShell, or hello Azure CLI.</span></span>

## <span data-ttu-id="93a61-226"><a name="permissions"></a>權限</span><span class="sxs-lookup"><span data-stu-id="93a61-226"><a name="permissions"></a>Permissions</span></span>

<span data-ttu-id="93a61-227">您使用的虛擬網路對等互連 toocreate hello 帳戶都必須 hello 必要的角色或權限。</span><span class="sxs-lookup"><span data-stu-id="93a61-227">hello accounts you use toocreate a virtual network peering must have hello necessary role or permissions.</span></span> <span data-ttu-id="93a61-228">例如，如果您已對等互連名為 VNet1 和 VNet2 這兩個虛擬網路，您的帳戶必須指派下列最小的角色或權限，每個虛擬網路的 hello:</span><span class="sxs-lookup"><span data-stu-id="93a61-228">For example, if you were peering two virtual networks named VNet1 and VNet2, your account must be assigned hello following minimum role or permissions for each virtual network:</span></span>
    
|<span data-ttu-id="93a61-229">虛擬網路</span><span class="sxs-lookup"><span data-stu-id="93a61-229">Virtual network</span></span>|<span data-ttu-id="93a61-230">角色</span><span class="sxs-lookup"><span data-stu-id="93a61-230">Role</span></span>|<span data-ttu-id="93a61-231">權限</span><span class="sxs-lookup"><span data-stu-id="93a61-231">Permissions</span></span>|
|---|---|---|
|<span data-ttu-id="93a61-232">VNet1</span><span class="sxs-lookup"><span data-stu-id="93a61-232">VNet1</span></span>|[<span data-ttu-id="93a61-233">網路參與者</span><span class="sxs-lookup"><span data-stu-id="93a61-233">Network Contributor</span></span>](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|<span data-ttu-id="93a61-234">Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write</span><span class="sxs-lookup"><span data-stu-id="93a61-234">Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write</span></span>|
|<span data-ttu-id="93a61-235">VNet2</span><span class="sxs-lookup"><span data-stu-id="93a61-235">VNet2</span></span>|[<span data-ttu-id="93a61-236">網路參與者</span><span class="sxs-lookup"><span data-stu-id="93a61-236">Network Contributor</span></span>](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|<span data-ttu-id="93a61-237">Microsoft.Network/virtualNetworks/peer</span><span class="sxs-lookup"><span data-stu-id="93a61-237">Microsoft.Network/virtualNetworks/peer</span></span>|

<span data-ttu-id="93a61-238">深入了解[內建角色](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)並指派特定權限太[自訂角色](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json)（資源管理員）。</span><span class="sxs-lookup"><span data-stu-id="93a61-238">Learn more about [built-in roles](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) and assigning specific permissions too[custom roles](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (Resource Manager only).</span></span>

## <span data-ttu-id="93a61-239"><a name="delete"></a>刪除資源</span><span class="sxs-lookup"><span data-stu-id="93a61-239"><a name="delete"></a>Delete resources</span></span>
<span data-ttu-id="93a61-240">當您完成本教學課程時，您可能想 toodelete hello 資源，您建立 hello 教學課程中，因此您不必承受使用費用。</span><span class="sxs-lookup"><span data-stu-id="93a61-240">When you've finished this tutorial, you might want toodelete hello resources you created in hello tutorial, so you don't incur usage charges.</span></span> <span data-ttu-id="93a61-241">刪除資源群組時，也會刪除 hello 資源群組中的所有資源。</span><span class="sxs-lookup"><span data-stu-id="93a61-241">Deleting a resource group also deletes all resources that are in hello resource group.</span></span>

### <span data-ttu-id="93a61-242"><a name="delete-portal"></a>Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="93a61-242"><a name="delete-portal"></a>Azure portal</span></span>

1. <span data-ttu-id="93a61-243">在 [hello] 入口網站搜尋方塊中，輸入**myResourceGroup**。</span><span class="sxs-lookup"><span data-stu-id="93a61-243">In hello portal search box, enter **myResourceGroup**.</span></span> <span data-ttu-id="93a61-244">在 hello 搜尋結果中，按一下  **myResourceGroup**。</span><span class="sxs-lookup"><span data-stu-id="93a61-244">In hello search results, click **myResourceGroup**.</span></span>
2. <span data-ttu-id="93a61-245">在 hello **myResourceGroup**刀鋒視窗中，按一下 hello**刪除**圖示。</span><span class="sxs-lookup"><span data-stu-id="93a61-245">On hello **myResourceGroup** blade, click hello **Delete** icon.</span></span>
3. <span data-ttu-id="93a61-246">tooconfirm hello 刪除、 hello**類型 hello 資源群組名稱**方塊中，輸入**myResourceGroup**，然後按一下**刪除**。</span><span class="sxs-lookup"><span data-stu-id="93a61-246">tooconfirm hello deletion, in hello **TYPE hello RESOURCE GROUP NAME** box, enter **myResourceGroup**, and then click **Delete**.</span></span>

### <span data-ttu-id="93a61-247"><a name="delete-cli"></a>Azure CLI</span><span class="sxs-lookup"><span data-stu-id="93a61-247"><a name="delete-cli"></a>Azure CLI</span></span>

<span data-ttu-id="93a61-248">輸入下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="93a61-248">Enter hello following command:</span></span>

```azurecli-interactive
az group delete --name myResourceGroup --yes
```

### <span data-ttu-id="93a61-249"><a name="delete-powershell"></a>PowerShell</span><span class="sxs-lookup"><span data-stu-id="93a61-249"><a name="delete-powershell"></a>PowerShell</span></span>

<span data-ttu-id="93a61-250">輸入下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="93a61-250">Enter hello following command:</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -force
```

## <a name="next-steps"></a><span data-ttu-id="93a61-251">後續步驟</span><span class="sxs-lookup"><span data-stu-id="93a61-251">Next steps</span></span>

- <span data-ttu-id="93a61-252">請先徹底熟悉重要[虛擬網路對等互連的條件約束和行為](virtual-network-manage-peering.md#requirements-and-constraints)，再建立虛擬網路對等互連以供生產環境使用。</span><span class="sxs-lookup"><span data-stu-id="93a61-252">Thoroughly familiarize yourself with important [virtual network peering constraints and behaviors](virtual-network-manage-peering.md#requirements-and-constraints) before creating a virtual network peering for production use.</span></span>
- <span data-ttu-id="93a61-253">了解所有[虛擬網路對等互連設定](virtual-network-manage-peering.md#create-a-peering)。</span><span class="sxs-lookup"><span data-stu-id="93a61-253">Learn about all [virtual network peering settings](virtual-network-manage-peering.md#create-a-peering).</span></span>
- <span data-ttu-id="93a61-254">了解如何太[建立中樞和支點網路拓樸](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering)與虛擬網路對等互連。</span><span class="sxs-lookup"><span data-stu-id="93a61-254">Learn how too[create a hub and spoke network topology](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) with virtual network peering.</span></span>
