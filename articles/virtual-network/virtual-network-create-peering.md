---
title: "建立 Azure 虛擬網路對等互連 - Resource Manager - 相同訂用帳戶 | Microsoft Docs"
description: "了解如何在透過 Resource Manager 建立且存在於相同 Azure 訂用帳戶的虛擬網路之間，建立虛擬網路對等互連。"
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
ms.openlocfilehash: a32a6b33e04c603325ab3612f61e5852682eac7d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-virtual-network-peering---resource-manager-same-subscription"></a><span data-ttu-id="d1971-103">建立虛擬網路對等互連 - Resource Manager，相同訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="d1971-103">Create a virtual network peering - Resource Manager, same subscription</span></span>

<span data-ttu-id="d1971-104">在本教學課程中，您會了解如何在透過 Resource Manager 建立的虛擬網路之間，建立虛擬網路對等互連。</span><span class="sxs-lookup"><span data-stu-id="d1971-104">In this tutorial, you learn to create a virtual network peering between virtual networks created through Resource Manager.</span></span> <span data-ttu-id="d1971-105">這兩個虛擬網路均存在於相同的訂用帳戶中。</span><span class="sxs-lookup"><span data-stu-id="d1971-105">Both virtual networks exist in the same subscription.</span></span> <span data-ttu-id="d1971-106">對等互連兩個虛擬網路，可讓不同虛擬網路中的資源彼此通訊，且通訊時會有相同的頻寬和延遲，彷彿這些資源是位於相同的虛擬網路中。</span><span class="sxs-lookup"><span data-stu-id="d1971-106">Peering two virtual networks enables resources in different virtual networks to communicate with each other with the same bandwidth and latency as though the resources were in the same virtual network.</span></span> <span data-ttu-id="d1971-107">深入了解[虛擬網路對等互連](virtual-network-peering-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="d1971-107">Learn more about [Virtual network peering](virtual-network-peering-overview.md).</span></span> 

<span data-ttu-id="d1971-108">建立虛擬網路對等互連的步驟會因一些因素而有所不同，這取決於虛擬網路是位於相同還是不同的訂用帳戶中，以及是透過哪一個 [Azure 部署模型](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json)建立虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="d1971-108">The steps to create a virtual network peering are different, depending on whether the virtual networks are in the same, or different, subscriptions, and which [Azure deployment model](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) the virtual networks are created through.</span></span> <span data-ttu-id="d1971-109">請按一下下表中的案例，以了解如何在其他案例中建立虛擬網路對等互連：</span><span class="sxs-lookup"><span data-stu-id="d1971-109">Learn how to create a virtual network peering in other scenarios by clicking the scenario from the following table:</span></span>

|<span data-ttu-id="d1971-110">Azure 部署模型</span><span class="sxs-lookup"><span data-stu-id="d1971-110">Azure deployment model</span></span>  | <span data-ttu-id="d1971-111">Azure 訂閱</span><span class="sxs-lookup"><span data-stu-id="d1971-111">Azure subscription</span></span>  |
|--------- |---------|
|[<span data-ttu-id="d1971-112">兩者皆使用 Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d1971-112">Both Resource Manager</span></span>](create-peering-different-subscriptions.md) |<span data-ttu-id="d1971-113">不同</span><span class="sxs-lookup"><span data-stu-id="d1971-113">Different</span></span>|
|[<span data-ttu-id="d1971-114">一個使用 Resource Manager、一個使用傳統部署模型</span><span class="sxs-lookup"><span data-stu-id="d1971-114">One Resource Manager, one classic</span></span>](create-peering-different-deployment-models.md) |<span data-ttu-id="d1971-115">相同</span><span class="sxs-lookup"><span data-stu-id="d1971-115">Same</span></span>|
|[<span data-ttu-id="d1971-116">一個使用 Resource Manager、一個使用傳統部署模型</span><span class="sxs-lookup"><span data-stu-id="d1971-116">One Resource Manager, one classic</span></span>](create-peering-different-deployment-models-subscriptions.md) |<span data-ttu-id="d1971-117">不同</span><span class="sxs-lookup"><span data-stu-id="d1971-117">Different</span></span>|

<span data-ttu-id="d1971-118">虛擬網路對等互連無法在透過傳統部署模型建立的兩個虛擬網路之間建立。</span><span class="sxs-lookup"><span data-stu-id="d1971-118">A virtual network peering cannot be created between two virtual networks deployed through the classic deployment model.</span></span> <span data-ttu-id="d1971-119">只能在存在於相同 Azure 區域中的兩個虛擬網路之間建立虛擬網路對等互連。</span><span class="sxs-lookup"><span data-stu-id="d1971-119">A virtual network peering can only be created between two virtual networks that exist in the same Azure region.</span></span> <span data-ttu-id="d1971-120">如果您需要將兩個都是透過傳統部署模型建立的虛擬網路連接，或是將存在於不同 Azure 區域中的虛擬網路連接，可以使用 Azure [VPN 閘道](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json)來連接這些虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="d1971-120">If you need to connect virtual networks that were both created through the classic deployment model, or that exist in different Azure regions, you can use an Azure [VPN Gateway](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) to connect the virtual networks.</span></span> 

<span data-ttu-id="d1971-121">您可以使用 [Azure 入口網站](#portal)、Azure [命令列介面](#cli) (CLI)、Azure [PowerShell](#powershell) 或 [Azure Resource Manager 範本](#template)，來建立虛擬網路對等互連。</span><span class="sxs-lookup"><span data-stu-id="d1971-121">You can use the [Azure portal](#portal), the Azure [command-line interface](#cli) (CLI), Azure [PowerShell](#powershell), or an [Azure Resource Manager template](#template) to create a virtual network peering.</span></span> <span data-ttu-id="d1971-122">按一下任何先前的工具連結，直接前往使用您所選工具建立虛擬網路對等互連的步驟。</span><span class="sxs-lookup"><span data-stu-id="d1971-122">Click any of the previous tool links to go directly to the steps for creating a virtual network peering using your tool of choice.</span></span>

## <span data-ttu-id="d1971-123"><a name="portal"></a>建立對等互連 - Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="d1971-123"><a name="portal"></a>Create peering - Azure portal</span></span>

1. <span data-ttu-id="d1971-124">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="d1971-124">Log in to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="d1971-125">您登入時使用的帳戶必須擁有必要的權限，才能建立虛擬網路對等互連。</span><span class="sxs-lookup"><span data-stu-id="d1971-125">The account you log in with must have the necessary permissions to create a virtual network peering.</span></span> <span data-ttu-id="d1971-126">如需詳細資訊，請參閱本文的[權限](#permissions)一節。</span><span class="sxs-lookup"><span data-stu-id="d1971-126">See the [Permissions](#permissions) section of this article for details.</span></span>
2. <span data-ttu-id="d1971-127">依序按一下 [新增]、[網路] 及 [虛擬網路]。</span><span class="sxs-lookup"><span data-stu-id="d1971-127">Click **+ New**, click **Networking**, then click **Virtual network**.</span></span>
3. <span data-ttu-id="d1971-128">在 [建立虛擬網路] 刀鋒視窗上，輸入或選取下列設定的值，然後按一下 [建立]：</span><span class="sxs-lookup"><span data-stu-id="d1971-128">In the **Create virtual network** blade, enter, or select values for the following settings, then click **Create**:</span></span>
    - <span data-ttu-id="d1971-129">**名稱**：*myVnet1*</span><span class="sxs-lookup"><span data-stu-id="d1971-129">**Name**: *myVnet1*</span></span>
    - <span data-ttu-id="d1971-130">**位址空間**：*10.0.0.0/16*</span><span class="sxs-lookup"><span data-stu-id="d1971-130">**Address space**: *10.0.0.0/16*</span></span>
    - <span data-ttu-id="d1971-131">**子網路名稱**：*預設值*</span><span class="sxs-lookup"><span data-stu-id="d1971-131">**Subnet name**: *default*</span></span>
    - <span data-ttu-id="d1971-132">**子網路位址範圍**：*10.0.0.0/24*</span><span class="sxs-lookup"><span data-stu-id="d1971-132">**Subnet address range**: *10.0.0.0/24*</span></span>
    - <span data-ttu-id="d1971-133">**訂用帳戶**︰選取您的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="d1971-133">**Subscription**: Select your subscription</span></span>
    - <span data-ttu-id="d1971-134">**資源群組**：選取 [新建] 並輸入 *myResourceGroup*</span><span class="sxs-lookup"><span data-stu-id="d1971-134">**Resource group**: Select **Create new** and enter *myResourceGroup*</span></span>
    - <span data-ttu-id="d1971-135">**位置**：*美國東部*</span><span class="sxs-lookup"><span data-stu-id="d1971-135">**Location**: *East US*</span></span>
4. <span data-ttu-id="d1971-136">再次完成步驟 2-3 並在步驟 3 中指定下列值：</span><span class="sxs-lookup"><span data-stu-id="d1971-136">Complete steps 2-3 again specifying the following values in step 3:</span></span>
    - <span data-ttu-id="d1971-137">**名稱**： *myVnet2*</span><span class="sxs-lookup"><span data-stu-id="d1971-137">**Name**: *myVnet2*</span></span>
    - <span data-ttu-id="d1971-138">**位址空間**：*10.1.0.0/16*</span><span class="sxs-lookup"><span data-stu-id="d1971-138">**Address space**: *10.1.0.0/16*</span></span>
    - <span data-ttu-id="d1971-139">**子網路名稱**：*預設值*</span><span class="sxs-lookup"><span data-stu-id="d1971-139">**Subnet name**: *default*</span></span>
    - <span data-ttu-id="d1971-140">**子網路位址範圍**：*10.1.0.0/24*</span><span class="sxs-lookup"><span data-stu-id="d1971-140">**Subnet address range**: *10.1.0.0/24*</span></span>
    - <span data-ttu-id="d1971-141">**訂用帳戶**︰選取您的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="d1971-141">**Subscription**: Select your subscription</span></span>
    - <span data-ttu-id="d1971-142">**資源群組**：選取 [使用現有] 並選取 *myResourceGroup*</span><span class="sxs-lookup"><span data-stu-id="d1971-142">**Resource group**: Select **Use existing** and select *myResourceGroup*</span></span>
    - <span data-ttu-id="d1971-143">**位置**：*美國東部*</span><span class="sxs-lookup"><span data-stu-id="d1971-143">**Location**: *East US*</span></span>
5. <span data-ttu-id="d1971-144">在入口網站頂端的 [搜尋資源] 方塊中，輸入 *myResourceGroup*。</span><span class="sxs-lookup"><span data-stu-id="d1971-144">In the **Search resources** box at the top of the portal, type *myResourceGroup*.</span></span> <span data-ttu-id="d1971-145">當搜尋結果中出現 **MyResourceGroup** 時，按一下該項目。</span><span class="sxs-lookup"><span data-stu-id="d1971-145">Click **myResourceGroup** when it appears in the search results.</span></span> <span data-ttu-id="d1971-146">**myresourcegroup** 資源群組的刀鋒視窗隨即出現。</span><span class="sxs-lookup"><span data-stu-id="d1971-146">A blade appears for the **myresourcegroup** resource group.</span></span> <span data-ttu-id="d1971-147">資源群組包含在前述步驟中建立的兩個虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="d1971-147">The resource group contains the two virtual networks created in previous steps.</span></span>
6. <span data-ttu-id="d1971-148">按一下 [myVNet1]。</span><span class="sxs-lookup"><span data-stu-id="d1971-148">Click **myVNet1**.</span></span>
7. <span data-ttu-id="d1971-149">在顯示的 [myVnet1] 刀鋒視窗，從刀鋒視窗左側的垂直選項清單中按一下 [對等互連]。</span><span class="sxs-lookup"><span data-stu-id="d1971-149">In the **myVnet1** blade that appears, click **Peerings** from the vertical list of options on the left side of the blade.</span></span>
8. <span data-ttu-id="d1971-150">在顯示的 [myVnet1 - 對等互連] 刀鋒視窗中，按一下 [+ 新增]</span><span class="sxs-lookup"><span data-stu-id="d1971-150">In the **myVnet1 - Peerings** blade that appeared, click **+ Add**</span></span>
9. <span data-ttu-id="d1971-151">在顯示的 [新增對等互連] 刀鋒視窗中，輸入或選取下列選項，然後按一下 [確定]：</span><span class="sxs-lookup"><span data-stu-id="d1971-151">In the **Add peering** blade that appears, enter, or select the following options, then click **OK**:</span></span>
     - <span data-ttu-id="d1971-152">**名稱**：*myVnet1ToMyVnet2*</span><span class="sxs-lookup"><span data-stu-id="d1971-152">**Name**: *myVnet1ToMyVnet2*</span></span>
     - <span data-ttu-id="d1971-153">**虛擬網路部署模型**：選取 [Resource Manager]。</span><span class="sxs-lookup"><span data-stu-id="d1971-153">**Virtual network deployment model**:  Select **Resource Manager**.</span></span> 
     - <span data-ttu-id="d1971-154">**訂用帳戶**︰選取您的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="d1971-154">**Subscription**: Select your subscription</span></span>
     - <span data-ttu-id="d1971-155">**虛擬網路**：按一下 [選擇虛擬網路]，然後按一下 [myVnet2]。</span><span class="sxs-lookup"><span data-stu-id="d1971-155">**Virtual network**:  Click **Choose a virtual network**, then click **myVnet2**.</span></span>
     - <span data-ttu-id="d1971-156">**允許虛擬網路存取**：確定已選取 [啟用]。</span><span class="sxs-lookup"><span data-stu-id="d1971-156">**Allow virtual network access:** Ensure that **Enabled** is selected.</span></span>
    <span data-ttu-id="d1971-157">本教學課程中不會使用其他設定。</span><span class="sxs-lookup"><span data-stu-id="d1971-157">No other settings are used in this tutorial.</span></span> <span data-ttu-id="d1971-158">若要了解所有對等互連設定，請閱讀[管理虛擬網路對等互連](virtual-network-manage-peering.md#create-a-peering)。</span><span class="sxs-lookup"><span data-stu-id="d1971-158">To learn about all peering settings, read [Manage virtual network peerings](virtual-network-manage-peering.md#create-a-peering).</span></span>
10. <span data-ttu-id="d1971-159">按一下上一個步驟中的 [確定] 後，[新增對等互連] 刀鋒視窗隨即關閉，而且您會再次看到 [myVnet1 - 對等互連] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="d1971-159">After clicking **OK** in the previous step, the **Add peering** blade closes and you see the **myVnet1 - Peerings** blade again.</span></span> <span data-ttu-id="d1971-160">幾秒之後，您建立的對等互連會出現在刀鋒視窗中。</span><span class="sxs-lookup"><span data-stu-id="d1971-160">After a few seconds, the peering you created appears in the blade.</span></span> <span data-ttu-id="d1971-161">您建立之 **myVnet1ToMyVnet2** 對等互連的 [對等互連狀態] 資料行中列出 [已起始]。</span><span class="sxs-lookup"><span data-stu-id="d1971-161">**Initiated** is listed in the **PEERING STATUS** column for the **myVnet1ToMyVnet2** peering you created.</span></span> <span data-ttu-id="d1971-162">您已將 Vnet1 對等互連到 Vnet2，但現在必須將 myVnet2 對等互連到 myVnet1。</span><span class="sxs-lookup"><span data-stu-id="d1971-162">You've peered Vnet1 to Vnet2, but now you must peer myVnet2 to myVnet1.</span></span> <span data-ttu-id="d1971-163">必須以建立雙線的對等互連，虛擬網路中的資源才能彼此通訊。</span><span class="sxs-lookup"><span data-stu-id="d1971-163">The peering must be created in both directions to enable resources in the virtual networks to communicate with each other.</span></span>
11. <span data-ttu-id="d1971-164">針對 myVnet2 再次完成步驟 5-10。</span><span class="sxs-lookup"><span data-stu-id="d1971-164">Complete steps 5-10 again for myVnet2.</span></span>  <span data-ttu-id="d1971-165">將對等互連命名為 *myVnet2ToMyVnet1*。</span><span class="sxs-lookup"><span data-stu-id="d1971-165">Name the peering *myVnet2ToMyVnet1*.</span></span>
12. <span data-ttu-id="d1971-166">按一下 [確定] 來建立 MyVnet2 的對等互連幾秒之後，您剛建立之 **myVnet2ToMyVnet1** 對等互連的 [對等互連狀態] 資料行中會列出 [已連線]。</span><span class="sxs-lookup"><span data-stu-id="d1971-166">A few seconds after clicking **OK** to create the peering for MyVnet2, the **myVnet2ToMyVnet1** peering you just created is listed with **Connected** in the **PEERING STATUS** column.</span></span>
13. <span data-ttu-id="d1971-167">針對 MyVnet1 再次完成步驟 5-7。</span><span class="sxs-lookup"><span data-stu-id="d1971-167">Complete steps 5-7 again for MyVnet1.</span></span> <span data-ttu-id="d1971-168">**myVnet1ToVNet2** 對等互連的 [對等互連狀態] 現在也是 [已連線]。</span><span class="sxs-lookup"><span data-stu-id="d1971-168">The **PEERING STATUS** for the **myVnet1ToVNet2** peering is now also **Connected**.</span></span> <span data-ttu-id="d1971-169">您在對等互連中兩個虛擬網路的 [對等互連狀態] 資料行中看到 [已連線] 之後，對等互連變已建立成功。</span><span class="sxs-lookup"><span data-stu-id="d1971-169">The peering is successfully established after you see **Connected** in the **PEERING STATUS** column for both virtual networks in the peering.</span></span>
14. <span data-ttu-id="d1971-170">**選擇性**：雖然本教學課程未涵蓋建立虛擬機器，但您可以在每個虛擬網路中建立一部虛擬機器，並從一部虛擬機器連線至另一部來驗證連線。</span><span class="sxs-lookup"><span data-stu-id="d1971-170">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine to the other, to validate connectivity.</span></span>
15. <span data-ttu-id="d1971-171">**選擇性︰**若要刪除您在本教學課程中建立的資源，請完成本文之[刪除資源](#delete-portal)一節中的步驟。</span><span class="sxs-lookup"><span data-stu-id="d1971-171">**Optional**: To delete the resources that you create in this tutorial, complete the steps in the [Delete resources](#delete-portal) section of this article.</span></span>

<span data-ttu-id="d1971-172">您在任何一個虛擬網路中建立的任何 Azure 資源現在能夠透過其 IP 位址彼此通訊。</span><span class="sxs-lookup"><span data-stu-id="d1971-172">Any Azure resources you create in either virtual network are now able to communicate with each other through their IP addresses.</span></span> <span data-ttu-id="d1971-173">如果您使用虛擬網路的預設 Azure 名稱解析，則虛擬網路中的資源無法跨虛擬網路解析名稱。</span><span class="sxs-lookup"><span data-stu-id="d1971-173">If you're using default Azure name resolution for the virtual networks, the resources in the virtual networks are not able to resolve names across the virtual networks.</span></span> <span data-ttu-id="d1971-174">如果您想要跨對等互連中的虛擬網路解析名稱，您必須建立自己的 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="d1971-174">If you want to resolve names across virtual networks in a peering, you must create your own DNS server.</span></span> <span data-ttu-id="d1971-175">了解如何設定[使用自己的 DNS 伺服器進行名稱解析](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server)。</span><span class="sxs-lookup"><span data-stu-id="d1971-175">Learn how to set up [Name resolution using your own DNS server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span></span>

## <span data-ttu-id="d1971-176"><a name="cli"></a>建立對等互連 - Azure CLI</span><span class="sxs-lookup"><span data-stu-id="d1971-176"><a name="cli"></a>Create peering - Azure CLI</span></span>

<span data-ttu-id="d1971-177">下列指令碼：</span><span class="sxs-lookup"><span data-stu-id="d1971-177">The following script:</span></span>

- <span data-ttu-id="d1971-178">需要 Azure CLI 2.0.4 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="d1971-178">Requires the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="d1971-179">若要尋找版本，請執行 `az --version` 命令。</span><span class="sxs-lookup"><span data-stu-id="d1971-179">To find the version, run the `az --version` command.</span></span> <span data-ttu-id="d1971-180">如果您需要升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="d1971-180">If you need to upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
- <span data-ttu-id="d1971-181">適用於 Bash 殼層。</span><span class="sxs-lookup"><span data-stu-id="d1971-181">Works in a Bash shell.</span></span> <span data-ttu-id="d1971-182">如需在 Windows 用戶端上執行 Azure CLI 指令碼的選項，請參閱[在 Windows 中執行 Azure CLI](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="d1971-182">For options on running Azure CLI scripts on Windows client, see [Running the Azure CLI in Windows](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> 

<span data-ttu-id="d1971-183">您可以不安裝 CLI 及其相依項目，而是改用 Azure Cloud Shell。</span><span class="sxs-lookup"><span data-stu-id="d1971-183">Instead of installing the CLI and its dependencies, you can use the Azure Cloud Shell.</span></span> <span data-ttu-id="d1971-184">Azure Cloud Shell 是免費的 Bash Shell，您可以直接在 Azure 入口網站內執行。</span><span class="sxs-lookup"><span data-stu-id="d1971-184">The Azure Cloud Shell is a free Bash shell that you can run directly within the Azure portal.</span></span> <span data-ttu-id="d1971-185">它具有預先安裝和設定的 Azure CLI，可與您的帳戶搭配使用。</span><span class="sxs-lookup"><span data-stu-id="d1971-185">It has the Azure CLI preinstalled and configured to use with your account.</span></span> <span data-ttu-id="d1971-186">按一下以下指令碼中的 [試試看] 按鈕，這會叫用可讓您登入 Azure 帳戶的 Cloud Shell。</span><span class="sxs-lookup"><span data-stu-id="d1971-186">Click the **Try it** button in the script that follows, which invokes a Cloud Shell that logs you can log in to your Azure account with.</span></span> <span data-ttu-id="d1971-187">若要執行指令碼，請按一下 [Copy] \(複製\) 按鈕，然後將內容貼到您的 Cloud Shell。</span><span class="sxs-lookup"><span data-stu-id="d1971-187">To execute the script, click the **Copy** button and paste the contents into your Cloud Shell.</span></span>

1. <span data-ttu-id="d1971-188">建立一個資源群組和兩個虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="d1971-188">Create a resource group and two virtual networks.</span></span>

    ```azurecli-interactive
    #!/bin/bash

    # Variables for common values used throughout the script.
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

2. <span data-ttu-id="d1971-189">在兩個虛擬網路之間建立虛擬網路對等互連。</span><span class="sxs-lookup"><span data-stu-id="d1971-189">Create a virtual network peering between the two virtual networks.</span></span>
 
    ```azurecli-interactive
    # Get the id for VNet1.
    vnet1Id=$(az network vnet show \
      --resource-group $rgName \
      --name myVnet1 \
      --query id --out tsv)

    # Get the id for VNet2.
    vnet2Id=$(az network vnet show \
      --resource-group $rgName \
      --name myVnet2 \
      --query id \
      --out tsv)

    # Peer VNet1 to VNet2.
    az network vnet peering create \
      --name myVnet1ToMyVnet2 \
      --resource-group $rgName \
      --vnet-name myVnet1 \
      --remote-vnet-id $vnet2Id \
      --allow-vnet-access

    # Peer VNet2 to VNet1.
    az network vnet peering create \
      --name myVnet2ToMyVnet1 \
      --resource-group $rgName \
      --vnet-name myVnet2 \
      --remote-vnet-id $vnet1Id \
      --allow-vnet-access
    ```

3. <span data-ttu-id="d1971-190">在指令碼執行後，檢閱每個虛擬網路的對等互連。</span><span class="sxs-lookup"><span data-stu-id="d1971-190">After the script executes, review the peerings for each virtual network.</span></span> 

    ```azurecli-interactive
    az network vnet peering list \
      --resource-group myResourceGroup \
      --vnet-name myVnet1 \
      --output table
    ```
    
    <span data-ttu-id="d1971-191">再次執行前一個命令，以 *myVnet2* 取代 *myVnet1*。</span><span class="sxs-lookup"><span data-stu-id="d1971-191">Run the previous command again, replacing *myVnet1* with *myVnet2*.</span></span> <span data-ttu-id="d1971-192">兩個命令的輸出會在 [對等互連] 資料行中顯示 [已連線]。</span><span class="sxs-lookup"><span data-stu-id="d1971-192">The output of both commands shows **Connected** in the **PeeringState** column.</span></span>

     <span data-ttu-id="d1971-193">您在任何一個虛擬網路中建立的任何 Azure 資源現在能夠透過其 IP 位址彼此通訊。</span><span class="sxs-lookup"><span data-stu-id="d1971-193">Any Azure resources you create in either virtual network are now able to communicate with each other through their IP addresses.</span></span> <span data-ttu-id="d1971-194">如果您使用虛擬網路的預設 Azure 名稱解析，則虛擬網路中的資源無法跨虛擬網路解析名稱。</span><span class="sxs-lookup"><span data-stu-id="d1971-194">If you're using default Azure name resolution for the virtual networks, the resources in the virtual networks are not able to resolve names across the virtual networks.</span></span> <span data-ttu-id="d1971-195">如果您想要跨對等互連中的虛擬網路解析名稱，您必須建立自己的 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="d1971-195">If you want to resolve names across virtual networks in a peering, you must create your own DNS server.</span></span> <span data-ttu-id="d1971-196">了解如何設定[使用自己的 DNS 伺服器進行名稱解析](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server)。</span><span class="sxs-lookup"><span data-stu-id="d1971-196">Learn how to set up [Name resolution using your own DNS server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span></span>

4. <span data-ttu-id="d1971-197">**選擇性**：雖然本教學課程未涵蓋建立虛擬機器，但您可以在每個虛擬網路中建立一部虛擬機器，並從一部虛擬機器連線至另一部來驗證連線。</span><span class="sxs-lookup"><span data-stu-id="d1971-197">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine to the other, to validate connectivity.</span></span>
5. <span data-ttu-id="d1971-198">**選擇性︰**若要刪除您在本教學課程中所建立的資源，請完成本文之[刪除資源](#delete-cli)中的步驟。</span><span class="sxs-lookup"><span data-stu-id="d1971-198">**Optional**: To delete the resources that you create in this tutorial, complete the steps in [Delete resources](#delete-cli) in this article.</span></span>


## <span data-ttu-id="d1971-199"><a name="powershell"></a>建立對等互連 - PowerShell</span><span class="sxs-lookup"><span data-stu-id="d1971-199"><a name="powershell"></a>Create peering - PowerShell</span></span>

1. <span data-ttu-id="d1971-200">安裝最新版的 PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) 模組。</span><span class="sxs-lookup"><span data-stu-id="d1971-200">Install the latest version of the PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) module.</span></span> <span data-ttu-id="d1971-201">如果您不熟悉 Azure PowerShell，請參閱 [Azure PowerShell 概觀](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="d1971-201">If you're new to Azure PowerShell, see [Azure PowerShell overview](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="d1971-202">若要啟動 PowerShell 工作階段，請移至 [開始]，輸入 **powershell**，然後按一下 [PowerShell]。</span><span class="sxs-lookup"><span data-stu-id="d1971-202">To start a PowerShell session, go to **Start**, enter **powershell**, and then click **PowerShell**.</span></span>
3. <span data-ttu-id="d1971-203">在 PowerShell 中，輸入 `login-azurermaccount` 命令來登入 Azure。</span><span class="sxs-lookup"><span data-stu-id="d1971-203">In PowerShell, log in to Azure by entering the `login-azurermaccount` command.</span></span> <span data-ttu-id="d1971-204">您登入時使用的帳戶必須擁有必要的權限，才能建立虛擬網路對等互連。</span><span class="sxs-lookup"><span data-stu-id="d1971-204">The account you log in with must have the necessary permissions to create a virtual network peering.</span></span> <span data-ttu-id="d1971-205">如需詳細資訊，請參閱本文的[權限](#permissions)一節。</span><span class="sxs-lookup"><span data-stu-id="d1971-205">See the [Permissions](#permissions) section of this article for details.</span></span>
4. <span data-ttu-id="d1971-206">建立一個資源群組和兩個虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="d1971-206">Create a resource group and two virtual networks.</span></span> <span data-ttu-id="d1971-207">若要執行指令碼，請複製下列指令碼、將它貼到 PowerShell，然後當螢幕上出現最後一行之後按 `Enter`：</span><span class="sxs-lookup"><span data-stu-id="d1971-207">To execute the script, copy the following script, paste it into PowerShell, and then press `Enter` after the last line appears on the screen:</span></span>

    ```powershell
    # Variables for common values used throughout the script.
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

5. <span data-ttu-id="d1971-208">在兩個虛擬網路之間建立虛擬網路對等互連。</span><span class="sxs-lookup"><span data-stu-id="d1971-208">Create a virtual network peering between the two virtual networks.</span></span> <span data-ttu-id="d1971-209">請複製下列指令碼、將它貼到 PowerShell，然後當螢幕上出現最後一行之後按 `Enter`：</span><span class="sxs-lookup"><span data-stu-id="d1971-209">Copy the following script, paste in to PowerShell, and then press `Enter` after the last line appears on the screen:</span></span>
    ```powershell
    # Peer VNet1 to VNet2.
    Add-AzureRmVirtualNetworkPeering `
      -Name 'myVnet1ToMyVnet2' `
      -VirtualNetwork $vnet1 `
      -RemoteVirtualNetworkId $vnet2.Id

    # Peer VNet2 to VNet1.
    Add-AzureRmVirtualNetworkPeering `
      -Name 'myVnet2ToMyVnet1' `
      -VirtualNetwork $vnet2 `
      -RemoteVirtualNetworkId $vnet1.Id
    ```
6. <span data-ttu-id="d1971-210">若要檢閱虛擬網路的子網路，請複製下列命令、貼到 PowerShell 視窗，然後按 `Enter`：</span><span class="sxs-lookup"><span data-stu-id="d1971-210">To review the subnets for the virtual network, copy the following command, paste in to PowerShell, and then press `Enter`:</span></span>

    ```powershell
    Get-AzureRmVirtualNetworkPeering `
      -ResourceGroupName myResourceGroup `
      -VirtualNetworkName myVnet1 `
      | Format-Table VirtualNetworkName, PeeringState
    ```

    <span data-ttu-id="d1971-211">再次執行前一個命令，以 *myVnet2* 取代 *myVnet1*。</span><span class="sxs-lookup"><span data-stu-id="d1971-211">Run the previous command again, replacing *myVnet1* with *myVnet2*.</span></span> <span data-ttu-id="d1971-212">兩個命令的輸出會在 [對等互連] 資料行中顯示 [已連線]。</span><span class="sxs-lookup"><span data-stu-id="d1971-212">The output of both commands shows **Connected** in the **PeeringState** column.</span></span>
7. <span data-ttu-id="d1971-213">**選擇性**：雖然本教學課程未涵蓋建立虛擬機器，但您可以在每個虛擬網路中建立一部虛擬機器，並從一部虛擬機器連線至另一部來驗證連線。</span><span class="sxs-lookup"><span data-stu-id="d1971-213">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine to the other, to validate connectivity.</span></span>
8. <span data-ttu-id="d1971-214">**選擇性︰**若要刪除您在本教學課程中所建立的資源，請完成本文之[刪除資源](#delete-powershell)中的步驟。</span><span class="sxs-lookup"><span data-stu-id="d1971-214">**Optional**: To delete the resources that you create in this tutorial, complete the steps in [Delete resources](#delete-powershell) in this article.</span></span>

<span data-ttu-id="d1971-215">您在任何一個虛擬網路中建立的任何 Azure 資源現在能夠透過其 IP 位址彼此通訊。</span><span class="sxs-lookup"><span data-stu-id="d1971-215">Any Azure resources you create in either virtual network are now able to communicate with each other through their IP addresses.</span></span> <span data-ttu-id="d1971-216">如果您使用虛擬網路的預設 Azure 名稱解析，則虛擬網路中的資源無法跨虛擬網路解析名稱。</span><span class="sxs-lookup"><span data-stu-id="d1971-216">If you're using default Azure name resolution for the virtual networks, the resources in the virtual networks are not able to resolve names across the virtual networks.</span></span> <span data-ttu-id="d1971-217">如果您想要跨對等互連中的虛擬網路解析名稱，您必須建立自己的 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="d1971-217">If you want to resolve names across virtual networks in a peering, you must create your own DNS server.</span></span> <span data-ttu-id="d1971-218">了解如何設定[使用自己的 DNS 伺服器進行名稱解析](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server)。</span><span class="sxs-lookup"><span data-stu-id="d1971-218">Learn how to set up [Name resolution using your own DNS server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span></span>

## <span data-ttu-id="d1971-219"><a name="template"></a>建立對等互連 - Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="d1971-219"><a name="template"></a>Create peering - Resource Manager template</span></span>

1. <span data-ttu-id="d1971-220">參考[建立虛擬網路對等互連](https://azure.microsoft.com/resources/templates/201-vnet-to-vnet-peering) Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="d1971-220">Reference [Create a virtual network peering](https://azure.microsoft.com/resources/templates/201-vnet-to-vnet-peering) Resource Manager template.</span></span> <span data-ttu-id="d1971-221">範本會提供使用 Azure 入口網站、PowerShell 或 Azure CLI 來部署範本的指示。</span><span class="sxs-lookup"><span data-stu-id="d1971-221">Instructions are provided with the template for deploying the template using the Azure portal, PowerShell, or the Azure CLI.</span></span> <span data-ttu-id="d1971-222">登入您選擇的工具，以使用具備建立虛擬網路對等互連之必要權限的帳戶來部署範本。</span><span class="sxs-lookup"><span data-stu-id="d1971-222">Log in to whichever tool you choose to deploy the template with using an account that has the necessary permissions to create a virtual network peering.</span></span> <span data-ttu-id="d1971-223">如需詳細資訊，請參閱本文的[權限](#permissions)一節。</span><span class="sxs-lookup"><span data-stu-id="d1971-223">See the [Permissions](#permissions) section of this article for details.</span></span>
2. <span data-ttu-id="d1971-224">**選擇性**：雖然本教學課程未涵蓋建立虛擬機器，但您可以在每個虛擬網路中建立一部虛擬機器，並從一部虛擬機器連線至另一部來驗證連線。</span><span class="sxs-lookup"><span data-stu-id="d1971-224">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine to the other, to validate connectivity.</span></span>
3. <span data-ttu-id="d1971-225">**選擇性︰**若要刪除您在本教學課程中建立的資源，請使用 Azure 入口網站、PowerShell 或 Azure CLI 來完成本文之[刪除資源](#delete)一節中的步驟。</span><span class="sxs-lookup"><span data-stu-id="d1971-225">**Optional**: To delete the resources that you create in this tutorial, complete the steps in the [Delete resources](#delete) section of this article, using either the Azure portal, PowerShell, or the Azure CLI.</span></span>

## <span data-ttu-id="d1971-226"><a name="permissions"></a>權限</span><span class="sxs-lookup"><span data-stu-id="d1971-226"><a name="permissions"></a>Permissions</span></span>

<span data-ttu-id="d1971-227">您用於建立虛擬網路對等互連的帳戶必須具有必要的角色或權限。</span><span class="sxs-lookup"><span data-stu-id="d1971-227">The accounts you use to create a virtual network peering must have the necessary role or permissions.</span></span> <span data-ttu-id="d1971-228">例如，如果您要將兩個虛擬網路 (分別名為 VNet1 和 VNet2) 對等互連，您的帳戶必須針對每個虛擬網路獲得下列最基本的角色或權限：</span><span class="sxs-lookup"><span data-stu-id="d1971-228">For example, if you were peering two virtual networks named VNet1 and VNet2, your account must be assigned the following minimum role or permissions for each virtual network:</span></span>
    
|<span data-ttu-id="d1971-229">虛擬網路</span><span class="sxs-lookup"><span data-stu-id="d1971-229">Virtual network</span></span>|<span data-ttu-id="d1971-230">角色</span><span class="sxs-lookup"><span data-stu-id="d1971-230">Role</span></span>|<span data-ttu-id="d1971-231">權限</span><span class="sxs-lookup"><span data-stu-id="d1971-231">Permissions</span></span>|
|---|---|---|
|<span data-ttu-id="d1971-232">VNet1</span><span class="sxs-lookup"><span data-stu-id="d1971-232">VNet1</span></span>|[<span data-ttu-id="d1971-233">網路參與者</span><span class="sxs-lookup"><span data-stu-id="d1971-233">Network Contributor</span></span>](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|<span data-ttu-id="d1971-234">Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write</span><span class="sxs-lookup"><span data-stu-id="d1971-234">Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write</span></span>|
|<span data-ttu-id="d1971-235">VNet2</span><span class="sxs-lookup"><span data-stu-id="d1971-235">VNet2</span></span>|[<span data-ttu-id="d1971-236">網路參與者</span><span class="sxs-lookup"><span data-stu-id="d1971-236">Network Contributor</span></span>](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|<span data-ttu-id="d1971-237">Microsoft.Network/virtualNetworks/peer</span><span class="sxs-lookup"><span data-stu-id="d1971-237">Microsoft.Network/virtualNetworks/peer</span></span>|

<span data-ttu-id="d1971-238">深入了解[內建角色](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)以及如何對[自訂角色](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json)指派特定權限 (僅限 Resource Manager)。</span><span class="sxs-lookup"><span data-stu-id="d1971-238">Learn more about [built-in roles](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) and assigning specific permissions to [custom roles](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (Resource Manager only).</span></span>

## <span data-ttu-id="d1971-239"><a name="delete"></a>刪除資源</span><span class="sxs-lookup"><span data-stu-id="d1971-239"><a name="delete"></a>Delete resources</span></span>
<span data-ttu-id="d1971-240">當您完成本教學課程時，您可能會想刪除您在教學課程中建立的資源，以免產生使用費。</span><span class="sxs-lookup"><span data-stu-id="d1971-240">When you've finished this tutorial, you might want to delete the resources you created in the tutorial, so you don't incur usage charges.</span></span> <span data-ttu-id="d1971-241">刪除資源群組同時會刪除其內含的所有資源。</span><span class="sxs-lookup"><span data-stu-id="d1971-241">Deleting a resource group also deletes all resources that are in the resource group.</span></span>

### <span data-ttu-id="d1971-242"><a name="delete-portal"></a>Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="d1971-242"><a name="delete-portal"></a>Azure portal</span></span>

1. <span data-ttu-id="d1971-243">在入口網站的搜尋方塊中，輸入 **myResourceGroup**。</span><span class="sxs-lookup"><span data-stu-id="d1971-243">In the portal search box, enter **myResourceGroup**.</span></span> <span data-ttu-id="d1971-244">在搜尋結果中按一下 [myResourceGroup]。</span><span class="sxs-lookup"><span data-stu-id="d1971-244">In the search results, click **myResourceGroup**.</span></span>
2. <span data-ttu-id="d1971-245">在 [myResourceGroup] 刀鋒視窗中，按一下 [刪除] 圖示。</span><span class="sxs-lookup"><span data-stu-id="d1971-245">On the **myResourceGroup** blade, click the **Delete** icon.</span></span>
3. <span data-ttu-id="d1971-246">若要確認刪除動作，請在 [輸入資源群組名稱] 方塊中輸入 **myResourceGroup**，然後按一下 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="d1971-246">To confirm the deletion, in the **TYPE THE RESOURCE GROUP NAME** box, enter **myResourceGroup**, and then click **Delete**.</span></span>

### <span data-ttu-id="d1971-247"><a name="delete-cli"></a>Azure CLI</span><span class="sxs-lookup"><span data-stu-id="d1971-247"><a name="delete-cli"></a>Azure CLI</span></span>

<span data-ttu-id="d1971-248">輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="d1971-248">Enter the following command:</span></span>

```azurecli-interactive
az group delete --name myResourceGroup --yes
```

### <span data-ttu-id="d1971-249"><a name="delete-powershell"></a>PowerShell</span><span class="sxs-lookup"><span data-stu-id="d1971-249"><a name="delete-powershell"></a>PowerShell</span></span>

<span data-ttu-id="d1971-250">輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="d1971-250">Enter the following command:</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -force
```

## <a name="next-steps"></a><span data-ttu-id="d1971-251">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d1971-251">Next steps</span></span>

- <span data-ttu-id="d1971-252">請先徹底熟悉重要[虛擬網路對等互連的條件約束和行為](virtual-network-manage-peering.md#requirements-and-constraints)，再建立虛擬網路對等互連以供生產環境使用。</span><span class="sxs-lookup"><span data-stu-id="d1971-252">Thoroughly familiarize yourself with important [virtual network peering constraints and behaviors](virtual-network-manage-peering.md#requirements-and-constraints) before creating a virtual network peering for production use.</span></span>
- <span data-ttu-id="d1971-253">了解所有[虛擬網路對等互連設定](virtual-network-manage-peering.md#create-a-peering)。</span><span class="sxs-lookup"><span data-stu-id="d1971-253">Learn about all [virtual network peering settings](virtual-network-manage-peering.md#create-a-peering).</span></span>
- <span data-ttu-id="d1971-254">了解如何透過虛擬網路對等互連來[建立中樞和輪輻網路拓撲](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering)。</span><span class="sxs-lookup"><span data-stu-id="d1971-254">Learn how to [create a hub and spoke network topology](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) with virtual network peering.</span></span>
