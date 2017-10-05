---
title: "建立 Azure 虛擬網路對等互連 - 不同部署模型 - 相同訂用帳戶 |Microsoft Docs"
description: "了解如何在透過不同 Azure 部署模型建立且存在於相同 Azure 訂用帳戶中的虛擬網路之間，建立虛擬網路對等互連。"
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
ms.openlocfilehash: 7d75d85863ce4b06ef1f552e0d583dec302f7ace
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/29/2017
---
# <a name="create-a-virtual-network-peering---different-deployment-models-same-subscription"></a><span data-ttu-id="32393-103">建立虛擬網路對等互連 - 不同部署模型、相同訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="32393-103">Create a virtual network peering - different deployment models, same subscription</span></span> 

<span data-ttu-id="32393-104">在本教學課程中，您會了解如何在透過不同部署模型建立的虛擬網路之間，建立虛擬網路對等互連。</span><span class="sxs-lookup"><span data-stu-id="32393-104">In this tutorial, you learn to create a virtual network peering between virtual networks created through different deployment models.</span></span> <span data-ttu-id="32393-105">這兩個虛擬網路均存在於相同的訂用帳戶中。</span><span class="sxs-lookup"><span data-stu-id="32393-105">Both virtual networks exist in the same subscription.</span></span> <span data-ttu-id="32393-106">對等互連兩個虛擬網路，可讓不同虛擬網路中的資源彼此通訊，且通訊時會有相同的頻寬和延遲，彷彿這些資源是位於相同的虛擬網路中。</span><span class="sxs-lookup"><span data-stu-id="32393-106">Peering two virtual networks enables resources in different virtual networks to communicate with each other with the same bandwidth and latency as though the resources were in the same virtual network.</span></span> <span data-ttu-id="32393-107">深入了解[虛擬網路對等互連](virtual-network-peering-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="32393-107">Learn more about [Virtual network peering](virtual-network-peering-overview.md).</span></span> 

<span data-ttu-id="32393-108">建立虛擬網路對等互連的步驟會因一些因素而有所不同，這取決於虛擬網路是位於相同還是不同的訂用帳戶中，以及是透過哪一個 [Azure 部署模型](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json)建立虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="32393-108">The steps to create a virtual network peering are different, depending on whether the virtual networks are in the same, or different, subscriptions, and which [Azure deployment model](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) the virtual networks are created through.</span></span> <span data-ttu-id="32393-109">請按一下下表中的案例，以了解如何在其他案例中建立虛擬網路對等互連：</span><span class="sxs-lookup"><span data-stu-id="32393-109">Learn how to create a virtual network peering in other scenarios by clicking the scenario from the following table:</span></span>

|<span data-ttu-id="32393-110">Azure 部署模型</span><span class="sxs-lookup"><span data-stu-id="32393-110">Azure deployment model</span></span>  | <span data-ttu-id="32393-111">Azure 訂閱</span><span class="sxs-lookup"><span data-stu-id="32393-111">Azure subscription</span></span>  |
|--------- |---------|
|[<span data-ttu-id="32393-112">兩者皆使用 Resource Manager</span><span class="sxs-lookup"><span data-stu-id="32393-112">Both Resource Manager</span></span>](virtual-network-create-peering.md) |<span data-ttu-id="32393-113">相同</span><span class="sxs-lookup"><span data-stu-id="32393-113">Same</span></span>|
|[<span data-ttu-id="32393-114">兩者皆使用 Resource Manager</span><span class="sxs-lookup"><span data-stu-id="32393-114">Both Resource Manager</span></span>](create-peering-different-subscriptions.md) |<span data-ttu-id="32393-115">不同</span><span class="sxs-lookup"><span data-stu-id="32393-115">Different</span></span>|
|[<span data-ttu-id="32393-116">一個使用 Resource Manager、一個使用傳統部署模型</span><span class="sxs-lookup"><span data-stu-id="32393-116">One Resource Manager, one classic</span></span>](create-peering-different-deployment-models-subscriptions.md) |<span data-ttu-id="32393-117">不同</span><span class="sxs-lookup"><span data-stu-id="32393-117">Different</span></span>|

<span data-ttu-id="32393-118">虛擬網路對等互連無法在透過傳統部署模型建立的兩個虛擬網路之間建立。</span><span class="sxs-lookup"><span data-stu-id="32393-118">A virtual network peering cannot be created between two virtual networks deployed through the classic deployment model.</span></span> <span data-ttu-id="32393-119">只能在存在於相同 Azure 區域中的兩個虛擬網路之間建立虛擬網路對等互連。</span><span class="sxs-lookup"><span data-stu-id="32393-119">A virtual network peering can only be created between two virtual networks that exist in the same Azure region.</span></span> <span data-ttu-id="32393-120">如果您需要將兩個都是透過傳統部署模型建立的虛擬網路連接，或是將存在於不同 Azure 區域中的虛擬網路連接，可以使用 Azure [VPN 閘道](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json)來連接這些虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="32393-120">If you need to connect virtual networks that were both created through the classic deployment model, or that exist in different Azure regions, you can use an Azure [VPN Gateway](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) to connect the virtual networks.</span></span> 

<span data-ttu-id="32393-121">您可以使用 [Azure 入口網站](#portal)、Azure [命令列介面](#cli) (CLI) 或 Azure [PowerShell](#powershell) 來建立虛擬網路對等互連。</span><span class="sxs-lookup"><span data-stu-id="32393-121">You can use the [Azure portal](#portal), the Azure [command-line interface](#cli) (CLI), or Azure [PowerShell](#powershell) to create a virtual network peering.</span></span> <span data-ttu-id="32393-122">按一下任何先前的工具連結，直接前往使用您所選工具建立虛擬網路對等互連的步驟。</span><span class="sxs-lookup"><span data-stu-id="32393-122">Click any of the previous tool links to go directly to the steps for creating a virtual network peering using your tool of choice.</span></span>

## <span data-ttu-id="32393-123"><a name="cli"></a>建立對等互連 - 入口網站</span><span class="sxs-lookup"><span data-stu-id="32393-123"><a name="cli"></a>Create peering - Portal</span></span>

1. <span data-ttu-id="32393-124">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="32393-124">Log in to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="32393-125">您登入時使用的帳戶必須擁有必要的權限，才能建立虛擬網路對等互連。</span><span class="sxs-lookup"><span data-stu-id="32393-125">The account you log in with must have the necessary permissions to create a virtual network peering.</span></span> <span data-ttu-id="32393-126">如需詳細資訊，請參閱本文的[權限](#permissions)一節。</span><span class="sxs-lookup"><span data-stu-id="32393-126">See the [Permissions](#permissions) section of this article for details.</span></span>
2. <span data-ttu-id="32393-127">依序按一下 [新增]、[網路] 及 [虛擬網路]。</span><span class="sxs-lookup"><span data-stu-id="32393-127">Click **+ New**, click **Networking**, then click **Virtual network**.</span></span>
3. <span data-ttu-id="32393-128">在 [建立虛擬網路] 刀鋒視窗上，輸入或選取下列設定的值，然後按一下 [建立]：</span><span class="sxs-lookup"><span data-stu-id="32393-128">In the **Create virtual network** blade, enter, or select values for the following settings, then click **Create**:</span></span>
    - <span data-ttu-id="32393-129">**名稱**：*myVnet1*</span><span class="sxs-lookup"><span data-stu-id="32393-129">**Name**: *myVnet1*</span></span>
    - <span data-ttu-id="32393-130">**位址空間**：*10.0.0.0/16*</span><span class="sxs-lookup"><span data-stu-id="32393-130">**Address space**: *10.0.0.0/16*</span></span>
    - <span data-ttu-id="32393-131">**子網路名稱**：*預設值*</span><span class="sxs-lookup"><span data-stu-id="32393-131">**Subnet name**: *default*</span></span>
    - <span data-ttu-id="32393-132">**子網路位址範圍**：*10.0.0.0/24*</span><span class="sxs-lookup"><span data-stu-id="32393-132">**Subnet address range**: *10.0.0.0/24*</span></span>
    - <span data-ttu-id="32393-133">**訂用帳戶**︰選取您的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="32393-133">**Subscription**: Select your subscription</span></span>
    - <span data-ttu-id="32393-134">**資源群組**：選取 [新建] 並輸入 *myResourceGroup*</span><span class="sxs-lookup"><span data-stu-id="32393-134">**Resource group**: Select **Create new** and enter *myResourceGroup*</span></span>
    - <span data-ttu-id="32393-135">**位置**：*美國東部*</span><span class="sxs-lookup"><span data-stu-id="32393-135">**Location**: *East US*</span></span>
4. <span data-ttu-id="32393-136">按一下 [+ 新增]。</span><span class="sxs-lookup"><span data-stu-id="32393-136">Click **+ New**.</span></span> <span data-ttu-id="32393-137">在 [搜尋 Marketplace] 方塊中，輸入*虛擬網路*。</span><span class="sxs-lookup"><span data-stu-id="32393-137">In the **Search the Marketplace** box, type *Virtual network*.</span></span> <span data-ttu-id="32393-138">當搜尋結果中出現虛擬網路時，按一下 [虛擬網路]。</span><span class="sxs-lookup"><span data-stu-id="32393-138">Click **Virtual network** when it appears in the search results.</span></span> 
5. <span data-ttu-id="32393-139">在 [虛擬網路] 刀鋒視窗中，於 [選取部署模型] 方塊中選取 [傳統]，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="32393-139">In the **Virtual network** blade, select **Classic** in the **Select a deployment model** box, and then click **Create**.</span></span>
6. <span data-ttu-id="32393-140">在 [建立虛擬網路] 刀鋒視窗上，輸入或選取下列設定的值，然後按一下 [建立]：</span><span class="sxs-lookup"><span data-stu-id="32393-140">In the **Create virtual network** blade, enter, or select values for the following settings, then click **Create**:</span></span>
    - <span data-ttu-id="32393-141">**名稱**： *myVnet2*</span><span class="sxs-lookup"><span data-stu-id="32393-141">**Name**: *myVnet2*</span></span>
    - <span data-ttu-id="32393-142">**位址空間**：*10.1.0.0/16*</span><span class="sxs-lookup"><span data-stu-id="32393-142">**Address space**: *10.1.0.0/16*</span></span>
    - <span data-ttu-id="32393-143">**子網路名稱**：*預設值*</span><span class="sxs-lookup"><span data-stu-id="32393-143">**Subnet name**: *default*</span></span>
    - <span data-ttu-id="32393-144">**子網路位址範圍**：*10.1.0.0/24*</span><span class="sxs-lookup"><span data-stu-id="32393-144">**Subnet address range**: *10.1.0.0/24*</span></span>
    - <span data-ttu-id="32393-145">**訂用帳戶**︰選取您的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="32393-145">**Subscription**: Select your subscription</span></span>
    - <span data-ttu-id="32393-146">**資源群組**：選取 [使用現有] 並選取 *myResourceGroup*</span><span class="sxs-lookup"><span data-stu-id="32393-146">**Resource group**: Select **Use existing** and select *myResourceGroup*</span></span>
    - <span data-ttu-id="32393-147">**位置**：*美國東部*</span><span class="sxs-lookup"><span data-stu-id="32393-147">**Location**: *East US*</span></span>
7. <span data-ttu-id="32393-148">在入口網站頂端的 [搜尋資源] 方塊中，輸入 *myResourceGroup*。</span><span class="sxs-lookup"><span data-stu-id="32393-148">In the **Search resources** box at the top of the portal, type *myResourceGroup*.</span></span> <span data-ttu-id="32393-149">當搜尋結果中出現 **MyResourceGroup** 時，按一下該項目。</span><span class="sxs-lookup"><span data-stu-id="32393-149">Click **myResourceGroup** when it appears in the search results.</span></span> <span data-ttu-id="32393-150">**myresourcegroup** 資源群組的刀鋒視窗隨即出現。</span><span class="sxs-lookup"><span data-stu-id="32393-150">A blade appears for the **myresourcegroup** resource group.</span></span> <span data-ttu-id="32393-151">資源群組包含在前述步驟中建立的兩個虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="32393-151">The resource group contains the two virtual networks created in previous steps.</span></span>
8. <span data-ttu-id="32393-152">按一下 [myVNet1]。</span><span class="sxs-lookup"><span data-stu-id="32393-152">Click **myVNet1**.</span></span>
9. <span data-ttu-id="32393-153">在顯示的 [myVnet1] 刀鋒視窗，從刀鋒視窗左側的垂直選項清單中按一下 [對等互連]。</span><span class="sxs-lookup"><span data-stu-id="32393-153">In the **myVnet1** blade that appears, click **Peerings** from the vertical list of options on the left side of the blade.</span></span>
10. <span data-ttu-id="32393-154">在顯示的 [myVnet1 - 對等互連] 刀鋒視窗中，按一下 [+ 新增]</span><span class="sxs-lookup"><span data-stu-id="32393-154">In the **myVnet1 - Peerings** blade that appeared, click **+ Add**</span></span>
11. <span data-ttu-id="32393-155">在顯示的 [新增對等互連] 刀鋒視窗中，輸入或選取下列選項，然後按一下 [確定]：</span><span class="sxs-lookup"><span data-stu-id="32393-155">In the **Add peering** blade that appears, enter, or select the following options, then click **OK**:</span></span>
     - <span data-ttu-id="32393-156">**名稱**：*myVnet1ToMyVnet2*</span><span class="sxs-lookup"><span data-stu-id="32393-156">**Name**: *myVnet1ToMyVnet2*</span></span>
     - <span data-ttu-id="32393-157">**虛擬網路部署模型**︰選取 [傳統]。</span><span class="sxs-lookup"><span data-stu-id="32393-157">**Virtual network deployment model**:  Select **Classic**.</span></span> 
     - <span data-ttu-id="32393-158">**訂用帳戶**︰選取您的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="32393-158">**Subscription**: Select your subscription</span></span>
     - <span data-ttu-id="32393-159">**虛擬網路**：按一下 [選擇虛擬網路]，然後按一下 [myVnet2]。</span><span class="sxs-lookup"><span data-stu-id="32393-159">**Virtual network**:  Click **Choose a virtual network**, then click **myVnet2**.</span></span>
     - <span data-ttu-id="32393-160">**允許虛擬網路存取**：確定已選取 [啟用]。</span><span class="sxs-lookup"><span data-stu-id="32393-160">**Allow virtual network access:** Ensure that **Enabled** is selected.</span></span>
    <span data-ttu-id="32393-161">本教學課程中不會使用其他設定。</span><span class="sxs-lookup"><span data-stu-id="32393-161">No other settings are used in this tutorial.</span></span> <span data-ttu-id="32393-162">若要了解所有對等互連設定，請閱讀[管理虛擬網路對等互連](virtual-network-manage-peering.md#create-a-peering)。</span><span class="sxs-lookup"><span data-stu-id="32393-162">To learn about all peering settings, read [Manage virtual network peerings](virtual-network-manage-peering.md#create-a-peering).</span></span>
12. <span data-ttu-id="32393-163">按一下上一個步驟中的 [確定] 後，[新增對等互連] 刀鋒視窗隨即關閉，而且您會再次看到 [myVnet1 - 對等互連] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="32393-163">After clicking **OK** in the previous step, the **Add peering** blade closes and you see the **myVnet1 - Peerings** blade again.</span></span> <span data-ttu-id="32393-164">幾秒之後，您建立的對等互連會出現在刀鋒視窗中。</span><span class="sxs-lookup"><span data-stu-id="32393-164">After a few seconds, the peering you created appears in the blade.</span></span> <span data-ttu-id="32393-165">您所建立之 **myVnet1ToMyVnet2** 對等互連的 [對等互連狀態] 資料行中會列出 [已連線]。</span><span class="sxs-lookup"><span data-stu-id="32393-165">**Connected** is listed in the **PEERING STATUS** column for the **myVnet1ToMyVnet2** peering you created.</span></span>

    <span data-ttu-id="32393-166">現在已建立對等互連。</span><span class="sxs-lookup"><span data-stu-id="32393-166">The peering is now established.</span></span> <span data-ttu-id="32393-167">您在任何一個虛擬網路中建立的任何 Azure 資源現在能夠透過其 IP 位址彼此通訊。</span><span class="sxs-lookup"><span data-stu-id="32393-167">Any Azure resources you create in either virtual network are now able to communicate with each other through their IP addresses.</span></span> <span data-ttu-id="32393-168">如果您使用虛擬網路的預設 Azure 名稱解析，則虛擬網路中的資源無法跨虛擬網路解析名稱。</span><span class="sxs-lookup"><span data-stu-id="32393-168">If you're using default Azure name resolution for the virtual networks, the resources in the virtual networks are not able to resolve names across the virtual networks.</span></span> <span data-ttu-id="32393-169">如果您想要跨對等互連中的虛擬網路解析名稱，您必須建立自己的 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="32393-169">If you want to resolve names across virtual networks in a peering, you must create your own DNS server.</span></span> <span data-ttu-id="32393-170">了解如何設定[使用自己的 DNS 伺服器進行名稱解析](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server)。</span><span class="sxs-lookup"><span data-stu-id="32393-170">Learn how to set up [Name resolution using your own DNS server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span></span>
13. <span data-ttu-id="32393-171">**選擇性**：雖然本教學課程未涵蓋建立虛擬機器，但您可以在每個虛擬網路中建立一部虛擬機器，並從一部虛擬機器連線至另一部來驗證連線。</span><span class="sxs-lookup"><span data-stu-id="32393-171">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine to the other, to validate connectivity.</span></span>
14. <span data-ttu-id="32393-172">**選擇性︰**若要刪除您在本教學課程中建立的資源，請完成本文之[刪除資源](#delete-portal)一節中的步驟。</span><span class="sxs-lookup"><span data-stu-id="32393-172">**Optional**: To delete the resources that you create in this tutorial, complete the steps in the [Delete resources](#delete-portal) section of this article.</span></span>

## <span data-ttu-id="32393-173"><a name="cli"></a>建立對等互連 - Azure CLI</span><span class="sxs-lookup"><span data-stu-id="32393-173"><a name="cli"></a>Create peering - Azure CLI</span></span>

1. <span data-ttu-id="32393-174">[安裝](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) Azure CLI 1.0 以建立虛擬網路 (傳統)。</span><span class="sxs-lookup"><span data-stu-id="32393-174">[Install](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) the Azure CLI 1.0 to create the virtual network (classic).</span></span>
2. <span data-ttu-id="32393-175">開啟命令工作階段，然後使用 `azure login` 命令來登入 Azure。</span><span class="sxs-lookup"><span data-stu-id="32393-175">Open a command session and log in to Azure using the `azure login` command.</span></span>
3. <span data-ttu-id="32393-176">輸入 `azure config mode asm` 命令來以「服務管理」模式執行 CLI。</span><span class="sxs-lookup"><span data-stu-id="32393-176">Run the CLI in Service Management mode by entering the `azure config mode asm` command.</span></span>
4. <span data-ttu-id="32393-177">輸入下列命令來建立虛擬網路 (傳統)：</span><span class="sxs-lookup"><span data-stu-id="32393-177">Enter the following command to create the virtual network (classic):</span></span>
 
    ```azurecli
    azure network vnet create --vnet myVnet2 --address-space 10.1.0.0 --cidr 16 --location "East US"
    ```

5. <span data-ttu-id="32393-178">建立資源群組和虛擬網路 (Resource Manager)。</span><span class="sxs-lookup"><span data-stu-id="32393-178">Create a resource group and a virtual network (Resource Manager).</span></span> <span data-ttu-id="32393-179">您可以使用 CLI 1.0 或 2.0 ([安裝](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json))。</span><span class="sxs-lookup"><span data-stu-id="32393-179">You can use either the CLI 1.0 or 2.0 ([install](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json)).</span></span> <span data-ttu-id="32393-180">本教學課程使用 CLI 2.0 來建立虛擬網路 (Resource Manager)，因為必須使用 2.0 來建立對等互連。</span><span class="sxs-lookup"><span data-stu-id="32393-180">In this tutorial, the CLI 2.0 is used to create the virtual network (Resource Manager), since 2.0 must be used to create the peering.</span></span> <span data-ttu-id="32393-181">請從已安裝 CLI 2.0.4 或更新版本的本機電腦，執行下列 Bash CLI 指令碼。</span><span class="sxs-lookup"><span data-stu-id="32393-181">Execute the following bash CLI script from your local machine with the CLI 2.0.4 or later installed.</span></span> <span data-ttu-id="32393-182">如需在 Windows 用戶端上執行 Bash CLI 指令碼的選項，請參閱[在 Windows 中執行 Azure CLI](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="32393-182">For options on running bash CLI scripts on Windows client, see [Running the Azure CLI in Windows](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="32393-183">您也可以使用 Azure Cloud Shell 來執行此指令碼。</span><span class="sxs-lookup"><span data-stu-id="32393-183">You can also run the script using the Azure Cloud Shell.</span></span> <span data-ttu-id="32393-184">Azure Cloud Shell 是免費的 Bash Shell，您可以直接在 Azure 入口網站內執行。</span><span class="sxs-lookup"><span data-stu-id="32393-184">The Azure Cloud Shell is a free Bash shell that you can run directly within the Azure portal.</span></span> <span data-ttu-id="32393-185">它具有預先安裝和設定的 Azure CLI，可與您的帳戶搭配使用。</span><span class="sxs-lookup"><span data-stu-id="32393-185">It has the Azure CLI preinstalled and configured to use with your account.</span></span> <span data-ttu-id="32393-186">按一下以下指令碼中的 [試試看] 按鈕，這會叫用可讓您登入 Azure 帳戶的 Cloud Shell。</span><span class="sxs-lookup"><span data-stu-id="32393-186">Click the **Try it** button in the script that follows, which invokes a Cloud Shell that logs you can log in to your Azure account with.</span></span> <span data-ttu-id="32393-187">若要執行此指令碼，請按一下 [複製] 按鈕並將內容貼到您的 Cloud Shell 中，然後按 `Enter`。</span><span class="sxs-lookup"><span data-stu-id="32393-187">To execute the script, click the **Copy** button and paste, the contents into your Cloud Shell, then press `Enter`.</span></span>

    ```azurecli-interactive
    #!/bin/bash

    # Create a resource group.
    az group create \
      --name myResourceGroup \
      --location eastus

    # Create the virtual network (Resource Manager).
    az network vnet create \
      --name myVnet1 \
      --resource-group myResourceGroup \
      --location eastus \
      --address-prefix 10.0.0.0/16
    ```

6. <span data-ttu-id="32393-188">在透過不同部署模型建立的兩個虛擬網路之間，建立虛擬網路對等互連。</span><span class="sxs-lookup"><span data-stu-id="32393-188">Create a virtual network peering between the two virtual networks created through the different deployment models.</span></span> <span data-ttu-id="32393-189">將下列指令碼複製到您電腦上的文字編輯器中。</span><span class="sxs-lookup"><span data-stu-id="32393-189">Copy the following script to a text editor on your PC.</span></span> <span data-ttu-id="32393-190">使用您的訂用帳戶 ID 來取代 `<subscription id>` 。</span><span class="sxs-lookup"><span data-stu-id="32393-190">Replace `<subscription id>` with your subscription Id.</span></span> <span data-ttu-id="32393-191">如果您不知道您的訂用帳戶 ID，請輸入 `az account show` 命令。</span><span class="sxs-lookup"><span data-stu-id="32393-191">If you don't know your subscription Id, enter the `az account show` command.</span></span> <span data-ttu-id="32393-192">輸出中的 **id** 值就是您的訂用帳戶 ID。</span><span class="sxs-lookup"><span data-stu-id="32393-192">The value for **id** in the output is your subscription Id.</span></span> <span data-ttu-id="32393-193">請將修改過的指令碼貼到您的 CLI 工作階段中，然後按 `Enter`。</span><span class="sxs-lookup"><span data-stu-id="32393-193">Paste the modified script in to your CLI session, and then press `Enter`.</span></span>

    ```azurecli-interactive
    # Get the id for VNet1.
    vnet1Id=$(az network vnet show \
      --resource-group myResourceGroup \
      --name myVnet1 \
      --query id --out tsv)

    # Peer VNet1 to VNet2.
    az network vnet peering create \
      --name myVnet1ToMyVnet2 \
      --resource-group myResourceGroup \
      --vnet-name myVnet1 \
      --remote-vnet-id /subscriptions/<subscription id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnet2 \
      --allow-vnet-access
    ```
7. <span data-ttu-id="32393-194">在指令碼執行之後，檢閱虛擬網路 (Resource Manager) 的對等互連。</span><span class="sxs-lookup"><span data-stu-id="32393-194">After the script executes, review the peering for the virtual network (Resource Manager).</span></span> <span data-ttu-id="32393-195">請複製下列命令並貼到您的 CLI 工作階段中，然後按 `Enter`：</span><span class="sxs-lookup"><span data-stu-id="32393-195">Copy the following command, paste it in your CLI session, and then press `Enter`:</span></span>

    ```azurecli-interactive
    az network vnet peering list \
      --resource-group myResourceGroup \
      --vnet-name myVnet1 \
      --output table
    ```
    
    <span data-ttu-id="32393-196">輸出會在 **PeeringState** 資料行中顯示 **Connected**。</span><span class="sxs-lookup"><span data-stu-id="32393-196">The output shows **Connected** in the **PeeringState** column.</span></span> 

    <span data-ttu-id="32393-197">您在任何一個虛擬網路中建立的任何 Azure 資源現在能夠透過其 IP 位址彼此通訊。</span><span class="sxs-lookup"><span data-stu-id="32393-197">Any Azure resources you create in either virtual network are now able to communicate with each other through their IP addresses.</span></span> <span data-ttu-id="32393-198">如果您使用虛擬網路的預設 Azure 名稱解析，則虛擬網路中的資源無法跨虛擬網路解析名稱。</span><span class="sxs-lookup"><span data-stu-id="32393-198">If you're using default Azure name resolution for the virtual networks, the resources in the virtual networks are not able to resolve names across the virtual networks.</span></span> <span data-ttu-id="32393-199">如果您想要跨對等互連中的虛擬網路解析名稱，您必須建立自己的 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="32393-199">If you want to resolve names across virtual networks in a peering, you must create your own DNS server.</span></span> <span data-ttu-id="32393-200">了解如何設定[使用自己的 DNS 伺服器進行名稱解析](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server)。</span><span class="sxs-lookup"><span data-stu-id="32393-200">Learn how to set up [Name resolution using your own DNS server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span></span>
8. <span data-ttu-id="32393-201">**選擇性**：雖然本教學課程未涵蓋建立虛擬機器，但您可以在每個虛擬網路中建立一部虛擬機器，並從一部虛擬機器連線至另一部來驗證連線。</span><span class="sxs-lookup"><span data-stu-id="32393-201">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine to the other, to validate connectivity.</span></span>
9. <span data-ttu-id="32393-202">**選擇性︰**若要刪除您在本教學課程中所建立的資源，請完成本文之[刪除資源](#delete-cli)中的步驟。</span><span class="sxs-lookup"><span data-stu-id="32393-202">**Optional**: To delete the resources that you create in this tutorial, complete the steps in [Delete resources](#delete-cli) in this article.</span></span>

## <span data-ttu-id="32393-203"><a name="powershell"></a>建立對等互連 - PowerShell</span><span class="sxs-lookup"><span data-stu-id="32393-203"><a name="powershell"></a>Create peering - PowerShell</span></span>

1. <span data-ttu-id="32393-204">安裝最新版的 PowerShell [Azure](https://www.powershellgallery.com/packages/Azure) 和 [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) 模組。</span><span class="sxs-lookup"><span data-stu-id="32393-204">Install the latest version of the PowerShell [Azure](https://www.powershellgallery.com/packages/Azure) and [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) modules.</span></span> <span data-ttu-id="32393-205">如果您不熟悉 Azure PowerShell，請參閱 [Azure PowerShell 概觀](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="32393-205">If you're new to Azure PowerShell, see [Azure PowerShell overview](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="32393-206">啟動 PowerShell 工作階段。</span><span class="sxs-lookup"><span data-stu-id="32393-206">Start a PowerShell session.</span></span>
3. <span data-ttu-id="32393-207">在 PowerShell 中，輸入 `Add-AzureAccount` 命令來登入 Azure。</span><span class="sxs-lookup"><span data-stu-id="32393-207">In PowerShell, log in to Azure by entering the `Add-AzureAccount` command.</span></span>
4. <span data-ttu-id="32393-208">若要使用 PowerShell 來建立虛擬網路 (傳統)，您必須建立一個新的或修改現有的網路組態檔。</span><span class="sxs-lookup"><span data-stu-id="32393-208">To create a virtual network (classic) with PowerShell, you must create a new, or modify an existing, network configuration file.</span></span> <span data-ttu-id="32393-209">了解如何[匯出、更新及匯入網路組態檔](virtual-networks-using-network-configuration-file.md)。</span><span class="sxs-lookup"><span data-stu-id="32393-209">Learn how to [export, update, and import network configuration files](virtual-networks-using-network-configuration-file.md).</span></span> <span data-ttu-id="32393-210">就本教學課程中使用的虛擬網路而言，此檔案應該包含下列 **VirtualNetworkSite** 元素：</span><span class="sxs-lookup"><span data-stu-id="32393-210">The file should include the following **VirtualNetworkSite** element for the virtual network used in this tutorial:</span></span>

    ```xml
    <VirtualNetworkSite name="myVnet2" Location="East US">
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
    > <span data-ttu-id="32393-211">匯入變更過的網路組態檔會導致您訂用帳戶中現有的虛擬網路 (傳統) 發生變更。</span><span class="sxs-lookup"><span data-stu-id="32393-211">Importing a changed network configuration file can cause changes to existing virtual networks (classic) in your subscription.</span></span> <span data-ttu-id="32393-212">請確定您只新增先前的虛擬網路，並且未變更或移除您訂用帳戶中任何現有的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="32393-212">Ensure you only add the previous virtual network and that you don't change or remove any existing virtual networks from your subscription.</span></span> 
5. <span data-ttu-id="32393-213">輸入 `login-azurermaccount` 命令來登入 Azure 以建立虛擬網路 (Resource Manager)。</span><span class="sxs-lookup"><span data-stu-id="32393-213">Log in to Azure to create the virtual network (Resource Manager) by entering the `login-azurermaccount` command.</span></span> <span data-ttu-id="32393-214">您登入時使用的帳戶必須擁有必要的權限，才能建立虛擬網路對等互連。</span><span class="sxs-lookup"><span data-stu-id="32393-214">The account you log in with must have the necessary permissions to create a virtual network peering.</span></span> <span data-ttu-id="32393-215">如需詳細資訊，請參閱本文的[權限](#permissions)一節。</span><span class="sxs-lookup"><span data-stu-id="32393-215">See the [Permissions](#permissions) section of this article for details.</span></span>
6. <span data-ttu-id="32393-216">建立資源群組和虛擬網路 (Resource Manager)。</span><span class="sxs-lookup"><span data-stu-id="32393-216">Create a resource group and a virtual network (Resource Manager).</span></span> <span data-ttu-id="32393-217">請複製指令碼並貼到 PowerShell 中，然後按 `Enter`。</span><span class="sxs-lookup"><span data-stu-id="32393-217">Copy the script, paste it into PowerShell, and then press `Enter`.</span></span>

    ```powershell
    # Create a resource group.
      New-AzureRmResourceGroup -Name myResourceGroup -Location eastus

    # Create the virtual network (Resource Manager).
      $vnet1 = New-AzureRmVirtualNetwork `
      -ResourceGroupName myResourceGroup `
      -Name 'myVnet1' `
      -AddressPrefix '10.0.0.0/16' `
      -Location eastus
    ```

7. <span data-ttu-id="32393-218">在透過不同部署模型建立的兩個虛擬網路之間，建立虛擬網路對等互連。</span><span class="sxs-lookup"><span data-stu-id="32393-218">Create a virtual network peering between the two virtual networks created through the different deployment models.</span></span> <span data-ttu-id="32393-219">將下列指令碼複製到您電腦上的文字編輯器中。</span><span class="sxs-lookup"><span data-stu-id="32393-219">Copy the following script to a text editor on your PC.</span></span> <span data-ttu-id="32393-220">使用您的訂用帳戶 ID 來取代 `<subscription id>` 。</span><span class="sxs-lookup"><span data-stu-id="32393-220">Replace `<subscription id>` with your subscription Id.</span></span> <span data-ttu-id="32393-221">如果您不知道您的訂用帳戶 ID，請輸入 `Get-AzureRmSubscription` 命令來檢視它。</span><span class="sxs-lookup"><span data-stu-id="32393-221">If you don't know your subscription Id, enter the `Get-AzureRmSubscription` command to view it.</span></span> <span data-ttu-id="32393-222">傳回之輸出中的 **Id** 值就是您的訂用帳戶 ID。</span><span class="sxs-lookup"><span data-stu-id="32393-222">The value for **Id** in the returned output is your subscription ID.</span></span> <span data-ttu-id="32393-223">若要執行指令碼，請從您的文字編輯器中複製修改過的指令碼，接著在 PowerShell 工作階段中按一下滑鼠右鍵，然後按 `Enter`。</span><span class="sxs-lookup"><span data-stu-id="32393-223">To execute the script, copy the modified script from your text editor, then right-click in your PowerShell session, and then press `Enter`.</span></span>

    ```powershell
    # Peer VNet1 to VNet2.
    Add-AzureRmVirtualNetworkPeering `
      -Name myVnet1ToMyVnet2 `
      -VirtualNetwork $vnet1 `
      -RemoteVirtualNetworkId /subscriptions/<subscription Id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnet2
    ```

8. <span data-ttu-id="32393-224">在指令碼執行之後，檢閱虛擬網路 (Resource Manager) 的對等互連。</span><span class="sxs-lookup"><span data-stu-id="32393-224">After the script executes, review the peering for the virtual network (Resource Manager).</span></span> <span data-ttu-id="32393-225">請複製下列命令並貼到您的 PowerShell 工作階段中，然後按 `Enter`：</span><span class="sxs-lookup"><span data-stu-id="32393-225">Copy the following command, paste it in your PowerShell session, and then press `Enter`:</span></span>

    ```powershell
    Get-AzureRmVirtualNetworkPeering `
      -ResourceGroupName myResourceGroup `
      -VirtualNetworkName myVnet1 `
      | Format-Table VirtualNetworkName, PeeringState
    ```

    <span data-ttu-id="32393-226">輸出會在 **PeeringState** 資料行中顯示 **Connected**。</span><span class="sxs-lookup"><span data-stu-id="32393-226">The output shows **Connected** in the **PeeringState** column.</span></span>

    <span data-ttu-id="32393-227">您在任何一個虛擬網路中建立的任何 Azure 資源現在能夠透過其 IP 位址彼此通訊。</span><span class="sxs-lookup"><span data-stu-id="32393-227">Any Azure resources you create in either virtual network are now able to communicate with each other through their IP addresses.</span></span> <span data-ttu-id="32393-228">如果您使用虛擬網路的預設 Azure 名稱解析，則虛擬網路中的資源無法跨虛擬網路解析名稱。</span><span class="sxs-lookup"><span data-stu-id="32393-228">If you're using default Azure name resolution for the virtual networks, the resources in the virtual networks are not able to resolve names across the virtual networks.</span></span> <span data-ttu-id="32393-229">如果您想要跨對等互連中的虛擬網路解析名稱，您必須建立自己的 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="32393-229">If you want to resolve names across virtual networks in a peering, you must create your own DNS server.</span></span> <span data-ttu-id="32393-230">了解如何設定[使用自己的 DNS 伺服器進行名稱解析](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server)。</span><span class="sxs-lookup"><span data-stu-id="32393-230">Learn how to set up [Name resolution using your own DNS server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span></span>

9. <span data-ttu-id="32393-231">**選擇性**：雖然本教學課程未涵蓋建立虛擬機器，但您可以在每個虛擬網路中建立一部虛擬機器，並從一部虛擬機器連線至另一部來驗證連線。</span><span class="sxs-lookup"><span data-stu-id="32393-231">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine to the other, to validate connectivity.</span></span>
10. <span data-ttu-id="32393-232">**選擇性︰**若要刪除您在本教學課程中所建立的資源，請完成本文之[刪除資源](#delete-powershell)中的步驟。</span><span class="sxs-lookup"><span data-stu-id="32393-232">**Optional**: To delete the resources that you create in this tutorial, complete the steps in [Delete resources](#delete-powershell) in this article.</span></span>
 
## <span data-ttu-id="32393-233"><a name="permissions"></a>權限</span><span class="sxs-lookup"><span data-stu-id="32393-233"><a name="permissions"></a>Permissions</span></span>

<span data-ttu-id="32393-234">您用於建立虛擬網路對等互連的帳戶必須具有必要的角色或權限。</span><span class="sxs-lookup"><span data-stu-id="32393-234">The accounts you use to create a virtual network peering must have the necessary role or permissions.</span></span> <span data-ttu-id="32393-235">例如，如果您是將名為 myVnet1 和 myVnet2 的兩個虛擬網路對等互連，您的帳戶就必須獲指派各個虛擬網路的下列最基本角色或權限：</span><span class="sxs-lookup"><span data-stu-id="32393-235">For example, if you were peering two virtual networks named myVnet1 and myVnet2, your account must be assigned the following minimum role or permissions for each virtual network:</span></span>
    
|<span data-ttu-id="32393-236">虛擬網路</span><span class="sxs-lookup"><span data-stu-id="32393-236">Virtual network</span></span>|<span data-ttu-id="32393-237">部署模型</span><span class="sxs-lookup"><span data-stu-id="32393-237">Deployment model</span></span>|<span data-ttu-id="32393-238">角色</span><span class="sxs-lookup"><span data-stu-id="32393-238">Role</span></span>|<span data-ttu-id="32393-239">權限</span><span class="sxs-lookup"><span data-stu-id="32393-239">Permissions</span></span>|
|---|---|---|---|
|<span data-ttu-id="32393-240">myVnet1</span><span class="sxs-lookup"><span data-stu-id="32393-240">myVnet1</span></span>|<span data-ttu-id="32393-241">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="32393-241">Resource Manager</span></span>|[<span data-ttu-id="32393-242">網路參與者</span><span class="sxs-lookup"><span data-stu-id="32393-242">Network Contributor</span></span>](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|<span data-ttu-id="32393-243">Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write</span><span class="sxs-lookup"><span data-stu-id="32393-243">Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write</span></span>|
| |<span data-ttu-id="32393-244">傳統</span><span class="sxs-lookup"><span data-stu-id="32393-244">Classic</span></span>|[<span data-ttu-id="32393-245">傳統網路參與者</span><span class="sxs-lookup"><span data-stu-id="32393-245">Classic Network Contributor</span></span>](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|<span data-ttu-id="32393-246">N/A</span><span class="sxs-lookup"><span data-stu-id="32393-246">N/A</span></span>|
|<span data-ttu-id="32393-247">myVnet2</span><span class="sxs-lookup"><span data-stu-id="32393-247">myVnet2</span></span>|<span data-ttu-id="32393-248">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="32393-248">Resource Manager</span></span>|[<span data-ttu-id="32393-249">網路參與者</span><span class="sxs-lookup"><span data-stu-id="32393-249">Network Contributor</span></span>](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|<span data-ttu-id="32393-250">Microsoft.Network/virtualNetworks/peer</span><span class="sxs-lookup"><span data-stu-id="32393-250">Microsoft.Network/virtualNetworks/peer</span></span>|
||<span data-ttu-id="32393-251">傳統</span><span class="sxs-lookup"><span data-stu-id="32393-251">Classic</span></span>|[<span data-ttu-id="32393-252">傳統網路參與者</span><span class="sxs-lookup"><span data-stu-id="32393-252">Classic Network Contributor</span></span>](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|<span data-ttu-id="32393-253">Microsoft.ClassicNetwork/virtualNetworks/peer</span><span class="sxs-lookup"><span data-stu-id="32393-253">Microsoft.ClassicNetwork/virtualNetworks/peer</span></span>|

<span data-ttu-id="32393-254">深入了解[內建角色](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)以及如何對[自訂角色](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json)指派特定權限 (僅限 Resource Manager)。</span><span class="sxs-lookup"><span data-stu-id="32393-254">Learn more about [built-in roles](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) and assigning specific permissions to [custom roles](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (Resource Manager only).</span></span>

## <span data-ttu-id="32393-255"><a name="delete"></a>刪除資源</span><span class="sxs-lookup"><span data-stu-id="32393-255"><a name="delete"></a>Delete resources</span></span>
<span data-ttu-id="32393-256">當您完成本教學課程時，您可能會想刪除您在教學課程中建立的資源，以免產生使用費。</span><span class="sxs-lookup"><span data-stu-id="32393-256">When you've finished this tutorial, you might want to delete the resources you created in the tutorial, so you don't incur usage charges.</span></span> <span data-ttu-id="32393-257">刪除資源群組同時會刪除其內含的所有資源。</span><span class="sxs-lookup"><span data-stu-id="32393-257">Deleting a resource group also deletes all resources that are in the resource group.</span></span>

### <span data-ttu-id="32393-258"><a name="delete-portal"></a>Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="32393-258"><a name="delete-portal"></a>Azure portal</span></span>

1. <span data-ttu-id="32393-259">在入口網站的搜尋方塊中，輸入 **myResourceGroup**。</span><span class="sxs-lookup"><span data-stu-id="32393-259">In the portal search box, enter **myResourceGroup**.</span></span> <span data-ttu-id="32393-260">在搜尋結果中按一下 [myResourceGroup]。</span><span class="sxs-lookup"><span data-stu-id="32393-260">In the search results, click **myResourceGroup**.</span></span>
2. <span data-ttu-id="32393-261">在 [myResourceGroup] 刀鋒視窗中，按一下 [刪除] 圖示。</span><span class="sxs-lookup"><span data-stu-id="32393-261">On the **myResourceGroup** blade, click the **Delete** icon.</span></span>
3. <span data-ttu-id="32393-262">若要確認刪除動作，請在 [輸入資源群組名稱] 方塊中輸入 **myResourceGroup**，然後按一下 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="32393-262">To confirm the deletion, in the **TYPE THE RESOURCE GROUP NAME** box, enter **myResourceGroup**, and then click **Delete**.</span></span>

### <span data-ttu-id="32393-263"><a name="delete-cli"></a>Azure CLI</span><span class="sxs-lookup"><span data-stu-id="32393-263"><a name="delete-cli"></a>Azure CLI</span></span>

1. <span data-ttu-id="32393-264">使用 Azure CLI 2.0 來以下列命令刪除虛擬網路 (Resource Manager)：</span><span class="sxs-lookup"><span data-stu-id="32393-264">Use the Azure CLI 2.0 to delete the virtual network (Resource Manager) with the following command:</span></span>

    ```azurecli-interactive
    az group delete --name myResourceGroup --yes
    ```

2. <span data-ttu-id="32393-265">使用 Azure CLI 1.0 來以下列命令刪除虛擬網路 (傳統)：</span><span class="sxs-lookup"><span data-stu-id="32393-265">Use the Azure CLI 1.0 to delete the virtual network (classic) with the following commands:</span></span>

    ```azurecli
    azure config mode asm

    azure network vnet delete --vnet myVnet2 --quiet
    ```

### <span data-ttu-id="32393-266"><a name="delete-powershell"></a>PowerShell</span><span class="sxs-lookup"><span data-stu-id="32393-266"><a name="delete-powershell"></a>PowerShell</span></span>

1. <span data-ttu-id="32393-267">輸入下列命令來刪除虛擬網路 (Resource Manager)：</span><span class="sxs-lookup"><span data-stu-id="32393-267">Enter the following command to delete the virtual network (Resource Manager):</span></span>

    ```powershell
    Remove-AzureRmResourceGroup -Name myResourceGroup -Force
    ```

2. <span data-ttu-id="32393-268">若要使用 PowerShell 來刪除虛擬網路 (傳統)，您必須修改現有的網路組態檔。</span><span class="sxs-lookup"><span data-stu-id="32393-268">To delete the virtual network (classic) with PowerShell, you must modify an existing network configuration file.</span></span> <span data-ttu-id="32393-269">了解如何[匯出、更新及匯入網路組態檔](virtual-networks-using-network-configuration-file.md)。</span><span class="sxs-lookup"><span data-stu-id="32393-269">Learn how to [export, update, and import network configuration files](virtual-networks-using-network-configuration-file.md).</span></span> <span data-ttu-id="32393-270">針對本教學課程中使用的虛擬網路，請移除下列 VirtualNetworkSite 元素：</span><span class="sxs-lookup"><span data-stu-id="32393-270">Remove the following VirtualNetworkSite element for the virtual network used in this tutorial:</span></span>

    ```xml
    <VirtualNetworkSite name="myVnet2" Location="East US">
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
    > <span data-ttu-id="32393-271">匯入變更過的網路組態檔會導致您訂用帳戶中現有的虛擬網路 (傳統) 發生變更。</span><span class="sxs-lookup"><span data-stu-id="32393-271">Importing a changed network configuration file can cause changes to existing virtual networks (classic) in your subscription.</span></span> <span data-ttu-id="32393-272">請確定您只移除先前的虛擬網路，並且未變更或移除您訂用帳戶中任何其他現有的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="32393-272">Ensure you only remove the previous virtual network and that you don't change or remove any other existing virtual networks from your subscription.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="32393-273">後續步驟</span><span class="sxs-lookup"><span data-stu-id="32393-273">Next steps</span></span>

- <span data-ttu-id="32393-274">請先徹底熟悉重要[虛擬網路對等互連的條件約束和行為](virtual-network-manage-peering.md#requirements-and-constraints)，再建立虛擬網路對等互連以供生產環境使用。</span><span class="sxs-lookup"><span data-stu-id="32393-274">Thoroughly familiarize yourself with important [virtual network peering constraints and behaviors](virtual-network-manage-peering.md#requirements-and-constraints) before creating a virtual network peering for production use.</span></span>
- <span data-ttu-id="32393-275">了解所有[虛擬網路對等互連設定](virtual-network-manage-peering.md#create-a-peering)。</span><span class="sxs-lookup"><span data-stu-id="32393-275">Learn about all [virtual network peering settings](virtual-network-manage-peering.md#create-a-peering).</span></span>
- <span data-ttu-id="32393-276">了解如何透過虛擬網路對等互連來[建立中樞和輪輻網路拓撲](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering)。</span><span class="sxs-lookup"><span data-stu-id="32393-276">Learn how to [create a hub and spoke network topology](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) with virtual network peering.</span></span>
