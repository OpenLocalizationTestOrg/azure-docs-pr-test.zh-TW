---
title: "aaaCreate Azure 虛擬網路對等式不同的部署模型的相同訂用帳戶 |Microsoft 文件"
description: "了解如何 toocreate 虛擬網路對等虛擬網路之間建立透過不同的 Azure 部署模型中存在 hello 相同 Azure 訂用帳戶。"
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
ms.openlocfilehash: 365156d651c9042ed52baeb15bf629fcc5329af8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-peering---different-deployment-models-same-subscription"></a><span data-ttu-id="4f9d6-103">建立虛擬網路對等互連 - 不同部署模型、相同訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="4f9d6-103">Create a virtual network peering - different deployment models, same subscription</span></span> 

<span data-ttu-id="4f9d6-104">在此教學課程中，您學會 toocreate 對等互連是透過不同的部署模型建立的虛擬網路之間的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-104">In this tutorial, you learn toocreate a virtual network peering between virtual networks created through different deployment models.</span></span> <span data-ttu-id="4f9d6-105">這兩個虛擬網路中存在 hello 相同訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-105">Both virtual networks exist in hello same subscription.</span></span> <span data-ttu-id="4f9d6-106">在不同的虛擬網路 toocommunicate 彼此具有對等兩個虛擬網路可讓資源 hello 相同的頻寬和延遲好像 hello 資源是在 hello 相同虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-106">Peering two virtual networks enables resources in different virtual networks toocommunicate with each other with hello same bandwidth and latency as though hello resources were in hello same virtual network.</span></span> <span data-ttu-id="4f9d6-107">深入了解[虛擬網路對等互連](virtual-network-peering-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-107">Learn more about [Virtual network peering](virtual-network-peering-overview.md).</span></span> 

<span data-ttu-id="4f9d6-108">hello 步驟 toocreate 虛擬網路對等互連會有所不同，hello 虛擬網路是否有相同，或不同的 hello、 訂用帳戶及其中[Azure 部署模型](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json)建立 hello 虛擬網路透過。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-108">hello steps toocreate a virtual network peering are different, depending on whether hello virtual networks are in hello same, or different, subscriptions, and which [Azure deployment model](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) hello virtual networks are created through.</span></span> <span data-ttu-id="4f9d6-109">了解 toocreate 的虛擬網路在其他情況下，即可從下表中的 hello hello 案例對等互連的方式：</span><span class="sxs-lookup"><span data-stu-id="4f9d6-109">Learn how toocreate a virtual network peering in other scenarios by clicking hello scenario from hello following table:</span></span>

|<span data-ttu-id="4f9d6-110">Azure 部署模型</span><span class="sxs-lookup"><span data-stu-id="4f9d6-110">Azure deployment model</span></span>  | <span data-ttu-id="4f9d6-111">Azure 訂閱</span><span class="sxs-lookup"><span data-stu-id="4f9d6-111">Azure subscription</span></span>  |
|--------- |---------|
|[<span data-ttu-id="4f9d6-112">兩者皆使用 Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4f9d6-112">Both Resource Manager</span></span>](virtual-network-create-peering.md) |<span data-ttu-id="4f9d6-113">相同</span><span class="sxs-lookup"><span data-stu-id="4f9d6-113">Same</span></span>|
|[<span data-ttu-id="4f9d6-114">兩者皆使用 Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4f9d6-114">Both Resource Manager</span></span>](create-peering-different-subscriptions.md) |<span data-ttu-id="4f9d6-115">不同</span><span class="sxs-lookup"><span data-stu-id="4f9d6-115">Different</span></span>|
|[<span data-ttu-id="4f9d6-116">一個使用 Resource Manager、一個使用傳統部署模型</span><span class="sxs-lookup"><span data-stu-id="4f9d6-116">One Resource Manager, one classic</span></span>](create-peering-different-deployment-models-subscriptions.md) |<span data-ttu-id="4f9d6-117">不同</span><span class="sxs-lookup"><span data-stu-id="4f9d6-117">Different</span></span>|

<span data-ttu-id="4f9d6-118">無法透過 hello 傳統部署模型所部署的兩個虛擬網路之間建立的虛擬網路對等互連。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-118">A virtual network peering cannot be created between two virtual networks deployed through hello classic deployment model.</span></span> <span data-ttu-id="4f9d6-119">虛擬網路對等互連只能建立兩個存在於 hello 相同的虛擬網路之間的 Azure 區域。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-119">A virtual network peering can only be created between two virtual networks that exist in hello same Azure region.</span></span> <span data-ttu-id="4f9d6-120">如果您需要同時建立透過 hello 傳統部署模型，或存在於不同的 Azure 地區 tooconnect 虛擬網路，您可以使用 Azure [VPN 閘道](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json)tooconnect hello 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-120">If you need tooconnect virtual networks that were both created through hello classic deployment model, or that exist in different Azure regions, you can use an Azure [VPN Gateway](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) tooconnect hello virtual networks.</span></span> 

<span data-ttu-id="4f9d6-121">您可以使用 hello [Azure 入口網站](#portal)，hello Azure[命令列介面](#cli)(CLI)，或 Azure [PowerShell](#powershell) toocreate 虛擬網路對等互連。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-121">You can use hello [Azure portal](#portal), hello Azure [command-line interface](#cli) (CLI), or Azure [PowerShell](#powershell) toocreate a virtual network peering.</span></span> <span data-ttu-id="4f9d6-122">直接 toohello 一個步驟建立的虛擬網路對等互連使用您選擇的工具，請按一下任何先前工具連結 toogo hello。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-122">Click any of hello previous tool links toogo directly toohello steps for creating a virtual network peering using your tool of choice.</span></span>

## <span data-ttu-id="4f9d6-123"><a name="cli"></a>建立對等互連 - 入口網站</span><span class="sxs-lookup"><span data-stu-id="4f9d6-123"><a name="cli"></a>Create peering - Portal</span></span>

1. <span data-ttu-id="4f9d6-124">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-124">Log in toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="4f9d6-125">登入的 hello 帳戶必須具有 hello 必要的權限 toocreate 虛擬網路對等互連。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-125">hello account you log in with must have hello necessary permissions toocreate a virtual network peering.</span></span> <span data-ttu-id="4f9d6-126">請參閱 hello[權限](#permissions)本文，如需詳細資訊一節。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-126">See hello [Permissions](#permissions) section of this article for details.</span></span>
2. <span data-ttu-id="4f9d6-127">依序按一下 [新增]、[網路] 及 [虛擬網路]。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-127">Click **+ New**, click **Networking**, then click **Virtual network**.</span></span>
3. <span data-ttu-id="4f9d6-128">在 hello**建立虛擬網路**刀鋒視窗中，輸入，或選取值 hello 下列設定，然後按一下 **建立**:</span><span class="sxs-lookup"><span data-stu-id="4f9d6-128">In hello **Create virtual network** blade, enter, or select values for hello following settings, then click **Create**:</span></span>
    - <span data-ttu-id="4f9d6-129">**名稱**：*myVnet1*</span><span class="sxs-lookup"><span data-stu-id="4f9d6-129">**Name**: *myVnet1*</span></span>
    - <span data-ttu-id="4f9d6-130">**位址空間**：*10.0.0.0/16*</span><span class="sxs-lookup"><span data-stu-id="4f9d6-130">**Address space**: *10.0.0.0/16*</span></span>
    - <span data-ttu-id="4f9d6-131">**子網路名稱**：*預設值*</span><span class="sxs-lookup"><span data-stu-id="4f9d6-131">**Subnet name**: *default*</span></span>
    - <span data-ttu-id="4f9d6-132">**子網路位址範圍**：*10.0.0.0/24*</span><span class="sxs-lookup"><span data-stu-id="4f9d6-132">**Subnet address range**: *10.0.0.0/24*</span></span>
    - <span data-ttu-id="4f9d6-133">**訂用帳戶**︰選取您的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="4f9d6-133">**Subscription**: Select your subscription</span></span>
    - <span data-ttu-id="4f9d6-134">**資源群組**：選取 [新建] 並輸入 *myResourceGroup*</span><span class="sxs-lookup"><span data-stu-id="4f9d6-134">**Resource group**: Select **Create new** and enter *myResourceGroup*</span></span>
    - <span data-ttu-id="4f9d6-135">**位置**：*美國東部*</span><span class="sxs-lookup"><span data-stu-id="4f9d6-135">**Location**: *East US*</span></span>
4. <span data-ttu-id="4f9d6-136">按一下 [+ 新增]。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-136">Click **+ New**.</span></span> <span data-ttu-id="4f9d6-137">在 hello**搜尋 hello Marketplace**方塊中，輸入*虛擬網路*。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-137">In hello **Search hello Marketplace** box, type *Virtual network*.</span></span> <span data-ttu-id="4f9d6-138">按一下**虛擬網路**hello 搜尋結果中出現。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-138">Click **Virtual network** when it appears in hello search results.</span></span> 
5. <span data-ttu-id="4f9d6-139">在 hello**虛擬網路**刀鋒視窗中，選取**傳統**在 hello**選取部署模型**方塊，然後再按一下**建立**。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-139">In hello **Virtual network** blade, select **Classic** in hello **Select a deployment model** box, and then click **Create**.</span></span>
6. <span data-ttu-id="4f9d6-140">在 hello**建立虛擬網路**刀鋒視窗中，輸入，或選取值 hello 下列設定，然後按一下 **建立**:</span><span class="sxs-lookup"><span data-stu-id="4f9d6-140">In hello **Create virtual network** blade, enter, or select values for hello following settings, then click **Create**:</span></span>
    - <span data-ttu-id="4f9d6-141">**名稱**： *myVnet2*</span><span class="sxs-lookup"><span data-stu-id="4f9d6-141">**Name**: *myVnet2*</span></span>
    - <span data-ttu-id="4f9d6-142">**位址空間**：*10.1.0.0/16*</span><span class="sxs-lookup"><span data-stu-id="4f9d6-142">**Address space**: *10.1.0.0/16*</span></span>
    - <span data-ttu-id="4f9d6-143">**子網路名稱**：*預設值*</span><span class="sxs-lookup"><span data-stu-id="4f9d6-143">**Subnet name**: *default*</span></span>
    - <span data-ttu-id="4f9d6-144">**子網路位址範圍**：*10.1.0.0/24*</span><span class="sxs-lookup"><span data-stu-id="4f9d6-144">**Subnet address range**: *10.1.0.0/24*</span></span>
    - <span data-ttu-id="4f9d6-145">**訂用帳戶**︰選取您的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="4f9d6-145">**Subscription**: Select your subscription</span></span>
    - <span data-ttu-id="4f9d6-146">**資源群組**：選取 [使用現有] 並選取 *myResourceGroup*</span><span class="sxs-lookup"><span data-stu-id="4f9d6-146">**Resource group**: Select **Use existing** and select *myResourceGroup*</span></span>
    - <span data-ttu-id="4f9d6-147">**位置**：*美國東部*</span><span class="sxs-lookup"><span data-stu-id="4f9d6-147">**Location**: *East US*</span></span>
7. <span data-ttu-id="4f9d6-148">在 hello**搜尋資源**方塊上方的 hello 入口網站中，型別 hello *myResourceGroup*。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-148">In hello **Search resources** box at hello top of hello portal, type *myResourceGroup*.</span></span> <span data-ttu-id="4f9d6-149">按一下**myResourceGroup** hello 搜尋結果中出現。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-149">Click **myResourceGroup** when it appears in hello search results.</span></span> <span data-ttu-id="4f9d6-150">刀鋒視窗會顯示 hello **myresourcegroup**資源群組。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-150">A blade appears for hello **myresourcegroup** resource group.</span></span> <span data-ttu-id="4f9d6-151">hello 資源群組包含兩個 hello 前述步驟中建立虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-151">hello resource group contains hello two virtual networks created in previous steps.</span></span>
8. <span data-ttu-id="4f9d6-152">按一下 [myVNet1]。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-152">Click **myVNet1**.</span></span>
9. <span data-ttu-id="4f9d6-153">在 [hello **myVnet1**刀鋒視窗中，按一下**對等互連**從 hello 垂直 hello 左邊的 hello] 刀鋒視窗上的選項清單。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-153">In hello **myVnet1** blade that appears, click **Peerings** from hello vertical list of options on hello left side of hello blade.</span></span>
10. <span data-ttu-id="4f9d6-154">在 hello **myVnet1-對等互連**刀鋒視窗中出現，按一下**+ 新增**</span><span class="sxs-lookup"><span data-stu-id="4f9d6-154">In hello **myVnet1 - Peerings** blade that appeared, click **+ Add**</span></span>
11. <span data-ttu-id="4f9d6-155">在 hello**新增對等互連**刀鋒視窗中，輸入，或選取 hello 下列選項，然後按一下 **確定**:</span><span class="sxs-lookup"><span data-stu-id="4f9d6-155">In hello **Add peering** blade that appears, enter, or select hello following options, then click **OK**:</span></span>
     - <span data-ttu-id="4f9d6-156">**名稱**：*myVnet1ToMyVnet2*</span><span class="sxs-lookup"><span data-stu-id="4f9d6-156">**Name**: *myVnet1ToMyVnet2*</span></span>
     - <span data-ttu-id="4f9d6-157">**虛擬網路部署模型**︰選取 [傳統]。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-157">**Virtual network deployment model**:  Select **Classic**.</span></span> 
     - <span data-ttu-id="4f9d6-158">**訂用帳戶**︰選取您的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="4f9d6-158">**Subscription**: Select your subscription</span></span>
     - <span data-ttu-id="4f9d6-159">**虛擬網路**：按一下 [選擇虛擬網路]，然後按一下 [myVnet2]。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-159">**Virtual network**:  Click **Choose a virtual network**, then click **myVnet2**.</span></span>
     - <span data-ttu-id="4f9d6-160">**允許虛擬網路存取**：確定已選取 [啟用]。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-160">**Allow virtual network access:** Ensure that **Enabled** is selected.</span></span>
    <span data-ttu-id="4f9d6-161">本教學課程中不會使用其他設定。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-161">No other settings are used in this tutorial.</span></span> <span data-ttu-id="4f9d6-162">讀取所有的對等設定的相關 toolearn[管理虛擬網路對等互連](virtual-network-manage-peering.md#create-a-peering)。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-162">toolearn about all peering settings, read [Manage virtual network peerings](virtual-network-manage-peering.md#create-a-peering).</span></span>
12. <span data-ttu-id="4f9d6-163">按一下後**[確定]** hello 先前步驟中，在 hello**新增對等互連**刀鋒視窗會關閉，而且您會看見 hello **myVnet1-對等互連**刀鋒視窗一次。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-163">After clicking **OK** in hello previous step, hello **Add peering** blade closes and you see hello **myVnet1 - Peerings** blade again.</span></span> <span data-ttu-id="4f9d6-164">幾秒之後，對等互連您所建立的 hello 會出現在 [hello] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-164">After a few seconds, hello peering you created appears in hello blade.</span></span> <span data-ttu-id="4f9d6-165">**連接**會列在 hello**對等互連狀態**hello 的資料行**myVnet1ToMyVnet2**對等互連您建立。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-165">**Connected** is listed in hello **PEERING STATUS** column for hello **myVnet1ToMyVnet2** peering you created.</span></span>

    <span data-ttu-id="4f9d6-166">現在建立 hello 對等互連。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-166">hello peering is now established.</span></span> <span data-ttu-id="4f9d6-167">所建立的其中一個虛擬網路中任何 Azure 資源，現在都能 toocommunicate 彼此透過其 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-167">Any Azure resources you create in either virtual network are now able toocommunicate with each other through their IP addresses.</span></span> <span data-ttu-id="4f9d6-168">如果您使用預設 Azure 名稱解析為 hello 虛擬網路，hello hello 虛擬網路中沒有資源無法 tooresolve 名稱在 hello 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-168">If you're using default Azure name resolution for hello virtual networks, hello resources in hello virtual networks are not able tooresolve names across hello virtual networks.</span></span> <span data-ttu-id="4f9d6-169">如果您想 tooresolve 名稱多個虛擬網路中的對等互連，您必須建立您自己的 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-169">If you want tooresolve names across virtual networks in a peering, you must create your own DNS server.</span></span> <span data-ttu-id="4f9d6-170">深入了解如何註冊 tooset[使用您自己的 DNS 伺服器的名稱解析](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server)。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-170">Learn how tooset up [Name resolution using your own DNS server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span></span>
13. <span data-ttu-id="4f9d6-171">**選擇性**： 未涵蓋在本教學課程中建立虛擬機器，雖然您可以在每個虛擬網路中建立虛擬機器，並從一個虛擬機器 toohello 其他 toovalidate 連線連接。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-171">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine toohello other, toovalidate connectivity.</span></span>
14. <span data-ttu-id="4f9d6-172">**選擇性**: toodelete hello 您在本教學課程中建立的資源，hello 步驟完成 hello[刪除資源](#delete-portal)本文一節。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-172">**Optional**: toodelete hello resources that you create in this tutorial, complete hello steps in hello [Delete resources](#delete-portal) section of this article.</span></span>

## <span data-ttu-id="4f9d6-173"><a name="cli"></a>建立對等互連 - Azure CLI</span><span class="sxs-lookup"><span data-stu-id="4f9d6-173"><a name="cli"></a>Create peering - Azure CLI</span></span>

1. <span data-ttu-id="4f9d6-174">[安裝](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json)hello Azure CLI 1.0 toocreate hello 虛擬網路 （傳統）。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-174">[Install](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) hello Azure CLI 1.0 toocreate hello virtual network (classic).</span></span>
2. <span data-ttu-id="4f9d6-175">開啟 命令工作階段並登入使用 hello tooAzure`azure login`命令。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-175">Open a command session and log in tooAzure using hello `azure login` command.</span></span>
3. <span data-ttu-id="4f9d6-176">服務管理模式中執行 hello CLI，方式是輸入 hello`azure config mode asm`命令。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-176">Run hello CLI in Service Management mode by entering hello `azure config mode asm` command.</span></span>
4. <span data-ttu-id="4f9d6-177">輸入下列命令 toocreate hello 虛擬網路 （傳統） 的 hello:</span><span class="sxs-lookup"><span data-stu-id="4f9d6-177">Enter hello following command toocreate hello virtual network (classic):</span></span>
 
    ```azurecli
    azure network vnet create --vnet myVnet2 --address-space 10.1.0.0 --cidr 16 --location "East US"
    ```

5. <span data-ttu-id="4f9d6-178">建立資源群組和虛擬網路 (Resource Manager)。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-178">Create a resource group and a virtual network (Resource Manager).</span></span> <span data-ttu-id="4f9d6-179">您可以使用 hello CLI 1.0 或 2.0 ([安裝](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json))。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-179">You can use either hello CLI 1.0 or 2.0 ([install](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json)).</span></span> <span data-ttu-id="4f9d6-180">在本教學課程，hello CLI 2.0 都是使用的 toocreate hello 虛擬網路 （資源管理員），因為 2.0 必須為使用的 toocreate hello 對等互連。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-180">In this tutorial, hello CLI 2.0 is used toocreate hello virtual network (Resource Manager), since 2.0 must be used toocreate hello peering.</span></span> <span data-ttu-id="4f9d6-181">執行的 hello 下列撞 CLI 指令碼，從本機電腦與 hello CLI 2.0.4 安裝或更新版本。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-181">Execute hello following bash CLI script from your local machine with hello CLI 2.0.4 or later installed.</span></span> <span data-ttu-id="4f9d6-182">如選項上執行被 Windows 用戶端上的 CLI 指令碼，請參閱 < [Windows 中執行 hello Azure CLI](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-182">For options on running bash CLI scripts on Windows client, see [Running hello Azure CLI in Windows](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="4f9d6-183">您也可以執行使用 hello Azure 雲端殼層 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-183">You can also run hello script using hello Azure Cloud Shell.</span></span> <span data-ttu-id="4f9d6-184">hello Azure 雲端殼層是免費的 Bash 殼層，您可以直接在 hello Azure 入口網站中執行。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-184">hello Azure Cloud Shell is a free Bash shell that you can run directly within hello Azure portal.</span></span> <span data-ttu-id="4f9d6-185">它有的 hello Azure CLI 預先安裝和設定 toouse 與您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-185">It has hello Azure CLI preinstalled and configured toouse with your account.</span></span> <span data-ttu-id="4f9d6-186">按一下 hello**試試**按鈕，如下所示，記錄您的雲端殼層會叫用來登入 tooyour hello 指令碼中使用的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-186">Click hello **Try it** button in hello script that follows, which invokes a Cloud Shell that logs you can log in tooyour Azure account with.</span></span> <span data-ttu-id="4f9d6-187">tooexecute hello 指令碼中，按一下 hello**複製**按鈕和 貼上，hello 內容到您的雲端殼層，然後按`Enter`。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-187">tooexecute hello script, click hello **Copy** button and paste, hello contents into your Cloud Shell, then press `Enter`.</span></span>

    ```azurecli-interactive
    #!/bin/bash

    # Create a resource group.
    az group create \
      --name myResourceGroup \
      --location eastus

    # Create hello virtual network (Resource Manager).
    az network vnet create \
      --name myVnet1 \
      --resource-group myResourceGroup \
      --location eastus \
      --address-prefix 10.0.0.0/16
    ```

6. <span data-ttu-id="4f9d6-188">建立虛擬網路之間 hello 兩個虛擬網路透過 hello 不同的部署模型建立對等互連。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-188">Create a virtual network peering between hello two virtual networks created through hello different deployment models.</span></span> <span data-ttu-id="4f9d6-189">複製下列指令碼 tooa 文字編輯器在您的電腦上的 hello。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-189">Copy hello following script tooa text editor on your PC.</span></span> <span data-ttu-id="4f9d6-190">使用您的訂用帳戶 ID 來取代 `<subscription id>` 。如果您不知道您的訂用帳戶 Id，請輸入 hello`az account show`命令。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-190">Replace `<subscription id>` with your subscription Id. If you don't know your subscription Id, enter hello `az account show` command.</span></span> <span data-ttu-id="4f9d6-191">hello 值**識別碼**在 hello 的輸出會是您的訂用帳戶 id。Tooyour CLI 工作階段中，貼上 hello 修改指令碼，然後按下`Enter`。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-191">hello value for **id** in hello output is your subscription Id. Paste hello modified script in tooyour CLI session, and then press `Enter`.</span></span>

    ```azurecli-interactive
    # Get hello id for VNet1.
    vnet1Id=$(az network vnet show \
      --resource-group myResourceGroup \
      --name myVnet1 \
      --query id --out tsv)

    # Peer VNet1 tooVNet2.
    az network vnet peering create \
      --name myVnet1ToMyVnet2 \
      --resource-group myResourceGroup \
      --vnet-name myVnet1 \
      --remote-vnet-id /subscriptions/<subscription id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnet2 \
      --allow-vnet-access
    ```
7. <span data-ttu-id="4f9d6-192">Hello 指令碼執行之後，請檢閱 hello 對等互連 hello 虛擬網路 （資源管理員）。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-192">After hello script executes, review hello peering for hello virtual network (Resource Manager).</span></span> <span data-ttu-id="4f9d6-193">複製 hello 下列命令，將它貼入您的 CLI 工作階段中，然後按`Enter`:</span><span class="sxs-lookup"><span data-stu-id="4f9d6-193">Copy hello following command, paste it in your CLI session, and then press `Enter`:</span></span>

    ```azurecli-interactive
    az network vnet peering list \
      --resource-group myResourceGroup \
      --vnet-name myVnet1 \
      --output table
    ```
    
    <span data-ttu-id="4f9d6-194">輸出中顯示 hello **Connected**在 hello **PeeringState**資料行。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-194">hello output shows **Connected** in hello **PeeringState** column.</span></span> 

    <span data-ttu-id="4f9d6-195">所建立的其中一個虛擬網路中任何 Azure 資源，現在都能 toocommunicate 彼此透過其 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-195">Any Azure resources you create in either virtual network are now able toocommunicate with each other through their IP addresses.</span></span> <span data-ttu-id="4f9d6-196">如果您使用預設 Azure 名稱解析為 hello 虛擬網路，hello hello 虛擬網路中沒有資源無法 tooresolve 名稱在 hello 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-196">If you're using default Azure name resolution for hello virtual networks, hello resources in hello virtual networks are not able tooresolve names across hello virtual networks.</span></span> <span data-ttu-id="4f9d6-197">如果您想 tooresolve 名稱多個虛擬網路中的對等互連，您必須建立您自己的 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-197">If you want tooresolve names across virtual networks in a peering, you must create your own DNS server.</span></span> <span data-ttu-id="4f9d6-198">深入了解如何註冊 tooset[使用您自己的 DNS 伺服器的名稱解析](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server)。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-198">Learn how tooset up [Name resolution using your own DNS server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span></span>
8. <span data-ttu-id="4f9d6-199">**選擇性**： 未涵蓋在本教學課程中建立虛擬機器，雖然您可以在每個虛擬網路中建立虛擬機器，並從一個虛擬機器 toohello 其他 toovalidate 連線連接。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-199">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine toohello other, toovalidate connectivity.</span></span>
9. <span data-ttu-id="4f9d6-200">**選擇性**: toodelete hello 您在本教學課程中建立的資源，步驟完成 hello[刪除資源](#delete-cli)本文中。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-200">**Optional**: toodelete hello resources that you create in this tutorial, complete hello steps in [Delete resources](#delete-cli) in this article.</span></span>

## <span data-ttu-id="4f9d6-201"><a name="powershell"></a>建立對等互連 - PowerShell</span><span class="sxs-lookup"><span data-stu-id="4f9d6-201"><a name="powershell"></a>Create peering - PowerShell</span></span>

1. <span data-ttu-id="4f9d6-202">安裝 hello hello PowerShell 最新版本[Azure](https://www.powershellgallery.com/packages/Azure)和[AzureRm](https://www.powershellgallery.com/packages/AzureRM/)模組。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-202">Install hello latest version of hello PowerShell [Azure](https://www.powershellgallery.com/packages/Azure) and [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) modules.</span></span> <span data-ttu-id="4f9d6-203">如果您是新 tooAzure PowerShell，請參閱[Azure PowerShell 概觀](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-203">If you're new tooAzure PowerShell, see [Azure PowerShell overview](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="4f9d6-204">啟動 PowerShell 工作階段。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-204">Start a PowerShell session.</span></span>
3. <span data-ttu-id="4f9d6-205">在 PowerShell 中，登入 tooAzure 輸入 hello`Add-AzureAccount`命令。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-205">In PowerShell, log in tooAzure by entering hello `Add-AzureAccount` command.</span></span>
4. <span data-ttu-id="4f9d6-206">toocreate 具有 PowerShell （傳統） 的虛擬網路，您必須建立新的或修改現有的網路組態檔。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-206">toocreate a virtual network (classic) with PowerShell, you must create a new, or modify an existing, network configuration file.</span></span> <span data-ttu-id="4f9d6-207">了解如何太[匯出、 更新和匯入網路組態檔](virtual-networks-using-network-configuration-file.md)。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-207">Learn how too[export, update, and import network configuration files](virtual-networks-using-network-configuration-file.md).</span></span> <span data-ttu-id="4f9d6-208">hello 檔案應該包含 hello 下列**VirtualNetworkSite** hello 這個教學課程中使用的虛擬網路的項目：</span><span class="sxs-lookup"><span data-stu-id="4f9d6-208">hello file should include hello following **VirtualNetworkSite** element for hello virtual network used in this tutorial:</span></span>

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
    > <span data-ttu-id="4f9d6-209">匯入已變更的網路組態檔，可能會導致變更 tooexisting （傳統） 您的訂用帳戶中的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-209">Importing a changed network configuration file can cause changes tooexisting virtual networks (classic) in your subscription.</span></span> <span data-ttu-id="4f9d6-210">確定您只有新增 hello 的上一個虛擬網路，且您不變更或移除任何現有的虛擬網路從您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-210">Ensure you only add hello previous virtual network and that you don't change or remove any existing virtual networks from your subscription.</span></span> 
5. <span data-ttu-id="4f9d6-211">登入 tooAzure toocreate hello 虛擬網路 （資源管理員） 中，輸入 hello`login-azurermaccount`命令。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-211">Log in tooAzure toocreate hello virtual network (Resource Manager) by entering hello `login-azurermaccount` command.</span></span> <span data-ttu-id="4f9d6-212">登入的 hello 帳戶必須具有 hello 必要的權限 toocreate 虛擬網路對等互連。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-212">hello account you log in with must have hello necessary permissions toocreate a virtual network peering.</span></span> <span data-ttu-id="4f9d6-213">請參閱 hello[權限](#permissions)本文，如需詳細資訊一節。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-213">See hello [Permissions](#permissions) section of this article for details.</span></span>
6. <span data-ttu-id="4f9d6-214">建立資源群組和虛擬網路 (Resource Manager)。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-214">Create a resource group and a virtual network (Resource Manager).</span></span> <span data-ttu-id="4f9d6-215">複製 hello 指令碼，將它貼到 PowerShell，然後按`Enter`。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-215">Copy hello script, paste it into PowerShell, and then press `Enter`.</span></span>

    ```powershell
    # Create a resource group.
      New-AzureRmResourceGroup -Name myResourceGroup -Location eastus

    # Create hello virtual network (Resource Manager).
      $vnet1 = New-AzureRmVirtualNetwork `
      -ResourceGroupName myResourceGroup `
      -Name 'myVnet1' `
      -AddressPrefix '10.0.0.0/16' `
      -Location eastus
    ```

7. <span data-ttu-id="4f9d6-216">建立虛擬網路之間 hello 兩個虛擬網路透過 hello 不同的部署模型建立對等互連。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-216">Create a virtual network peering between hello two virtual networks created through hello different deployment models.</span></span> <span data-ttu-id="4f9d6-217">複製下列指令碼 tooa 文字編輯器在您的電腦上的 hello。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-217">Copy hello following script tooa text editor on your PC.</span></span> <span data-ttu-id="4f9d6-218">使用您的訂用帳戶 ID 來取代 `<subscription id>` 。如果您不知道您的訂用帳戶 Id，請輸入 hello`Get-AzureRmSubscription`命令 tooview 它。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-218">Replace `<subscription id>` with your subscription Id. If you don't know your subscription Id, enter hello `Get-AzureRmSubscription` command tooview it.</span></span> <span data-ttu-id="4f9d6-219">hello 值**識別碼**hello 傳回輸出是您的訂用帳戶 id。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-219">hello value for **Id** in hello returned output is your subscription ID.</span></span> <span data-ttu-id="4f9d6-220">tooexecute hello 指令碼中，複製 hello 修改指令碼從您的文字編輯器，然後以滑鼠右鍵按一下您的 PowerShell 工作階段，然後按`Enter`。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-220">tooexecute hello script, copy hello modified script from your text editor, then right-click in your PowerShell session, and then press `Enter`.</span></span>

    ```powershell
    # Peer VNet1 tooVNet2.
    Add-AzureRmVirtualNetworkPeering `
      -Name myVnet1ToMyVnet2 `
      -VirtualNetwork $vnet1 `
      -RemoteVirtualNetworkId /subscriptions/<subscription Id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnet2
    ```

8. <span data-ttu-id="4f9d6-221">Hello 指令碼執行之後，請檢閱 hello 對等互連 hello 虛擬網路 （資源管理員）。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-221">After hello script executes, review hello peering for hello virtual network (Resource Manager).</span></span> <span data-ttu-id="4f9d6-222">複製 hello 下列命令，將它貼入您的 PowerShell 工作階段中，然後按`Enter`:</span><span class="sxs-lookup"><span data-stu-id="4f9d6-222">Copy hello following command, paste it in your PowerShell session, and then press `Enter`:</span></span>

    ```powershell
    Get-AzureRmVirtualNetworkPeering `
      -ResourceGroupName myResourceGroup `
      -VirtualNetworkName myVnet1 `
      | Format-Table VirtualNetworkName, PeeringState
    ```

    <span data-ttu-id="4f9d6-223">輸出中顯示 hello **Connected**在 hello **PeeringState**資料行。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-223">hello output shows **Connected** in hello **PeeringState** column.</span></span>

    <span data-ttu-id="4f9d6-224">所建立的其中一個虛擬網路中任何 Azure 資源，現在都能 toocommunicate 彼此透過其 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-224">Any Azure resources you create in either virtual network are now able toocommunicate with each other through their IP addresses.</span></span> <span data-ttu-id="4f9d6-225">如果您使用預設 Azure 名稱解析為 hello 虛擬網路，hello hello 虛擬網路中沒有資源無法 tooresolve 名稱在 hello 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-225">If you're using default Azure name resolution for hello virtual networks, hello resources in hello virtual networks are not able tooresolve names across hello virtual networks.</span></span> <span data-ttu-id="4f9d6-226">如果您想 tooresolve 名稱多個虛擬網路中的對等互連，您必須建立您自己的 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-226">If you want tooresolve names across virtual networks in a peering, you must create your own DNS server.</span></span> <span data-ttu-id="4f9d6-227">深入了解如何註冊 tooset[使用您自己的 DNS 伺服器的名稱解析](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server)。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-227">Learn how tooset up [Name resolution using your own DNS server](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).</span></span>

9. <span data-ttu-id="4f9d6-228">**選擇性**： 未涵蓋在本教學課程中建立虛擬機器，雖然您可以在每個虛擬網路中建立虛擬機器，並從一個虛擬機器 toohello 其他 toovalidate 連線連接。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-228">**Optional**: Though creating virtual machines is not covered in this tutorial, you can create a virtual machine in each virtual network and connect from one virtual machine toohello other, toovalidate connectivity.</span></span>
10. <span data-ttu-id="4f9d6-229">**選擇性**: toodelete hello 您在本教學課程中建立的資源，步驟完成 hello[刪除資源](#delete-powershell)本文中。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-229">**Optional**: toodelete hello resources that you create in this tutorial, complete hello steps in [Delete resources](#delete-powershell) in this article.</span></span>
 
## <span data-ttu-id="4f9d6-230"><a name="permissions"></a>權限</span><span class="sxs-lookup"><span data-stu-id="4f9d6-230"><a name="permissions"></a>Permissions</span></span>

<span data-ttu-id="4f9d6-231">您使用的虛擬網路對等互連 toocreate hello 帳戶都必須 hello 必要的角色或權限。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-231">hello accounts you use toocreate a virtual network peering must have hello necessary role or permissions.</span></span> <span data-ttu-id="4f9d6-232">例如，如果您已對等互連名為 myVnet1 和 myVnet2 的兩個虛擬網路，您的帳戶必須指派下列最小的角色或權限，每個虛擬網路的 hello:</span><span class="sxs-lookup"><span data-stu-id="4f9d6-232">For example, if you were peering two virtual networks named myVnet1 and myVnet2, your account must be assigned hello following minimum role or permissions for each virtual network:</span></span>
    
|<span data-ttu-id="4f9d6-233">虛擬網路</span><span class="sxs-lookup"><span data-stu-id="4f9d6-233">Virtual network</span></span>|<span data-ttu-id="4f9d6-234">部署模型</span><span class="sxs-lookup"><span data-stu-id="4f9d6-234">Deployment model</span></span>|<span data-ttu-id="4f9d6-235">角色</span><span class="sxs-lookup"><span data-stu-id="4f9d6-235">Role</span></span>|<span data-ttu-id="4f9d6-236">權限</span><span class="sxs-lookup"><span data-stu-id="4f9d6-236">Permissions</span></span>|
|---|---|---|---|
|<span data-ttu-id="4f9d6-237">myVnet1</span><span class="sxs-lookup"><span data-stu-id="4f9d6-237">myVnet1</span></span>|<span data-ttu-id="4f9d6-238">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4f9d6-238">Resource Manager</span></span>|[<span data-ttu-id="4f9d6-239">網路參與者</span><span class="sxs-lookup"><span data-stu-id="4f9d6-239">Network Contributor</span></span>](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|<span data-ttu-id="4f9d6-240">Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write</span><span class="sxs-lookup"><span data-stu-id="4f9d6-240">Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write</span></span>|
| |<span data-ttu-id="4f9d6-241">傳統</span><span class="sxs-lookup"><span data-stu-id="4f9d6-241">Classic</span></span>|[<span data-ttu-id="4f9d6-242">傳統網路參與者</span><span class="sxs-lookup"><span data-stu-id="4f9d6-242">Classic Network Contributor</span></span>](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|<span data-ttu-id="4f9d6-243">N/A</span><span class="sxs-lookup"><span data-stu-id="4f9d6-243">N/A</span></span>|
|<span data-ttu-id="4f9d6-244">myVnet2</span><span class="sxs-lookup"><span data-stu-id="4f9d6-244">myVnet2</span></span>|<span data-ttu-id="4f9d6-245">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4f9d6-245">Resource Manager</span></span>|[<span data-ttu-id="4f9d6-246">網路參與者</span><span class="sxs-lookup"><span data-stu-id="4f9d6-246">Network Contributor</span></span>](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|<span data-ttu-id="4f9d6-247">Microsoft.Network/virtualNetworks/peer</span><span class="sxs-lookup"><span data-stu-id="4f9d6-247">Microsoft.Network/virtualNetworks/peer</span></span>|
||<span data-ttu-id="4f9d6-248">傳統</span><span class="sxs-lookup"><span data-stu-id="4f9d6-248">Classic</span></span>|[<span data-ttu-id="4f9d6-249">傳統網路參與者</span><span class="sxs-lookup"><span data-stu-id="4f9d6-249">Classic Network Contributor</span></span>](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|<span data-ttu-id="4f9d6-250">Microsoft.ClassicNetwork/virtualNetworks/peer</span><span class="sxs-lookup"><span data-stu-id="4f9d6-250">Microsoft.ClassicNetwork/virtualNetworks/peer</span></span>|

<span data-ttu-id="4f9d6-251">深入了解[內建角色](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)並指派特定權限太[自訂角色](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json)（資源管理員）。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-251">Learn more about [built-in roles](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) and assigning specific permissions too[custom roles](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (Resource Manager only).</span></span>

## <span data-ttu-id="4f9d6-252"><a name="delete"></a>刪除資源</span><span class="sxs-lookup"><span data-stu-id="4f9d6-252"><a name="delete"></a>Delete resources</span></span>
<span data-ttu-id="4f9d6-253">當您完成本教學課程時，您可能想 toodelete hello 資源，您建立 hello 教學課程中，因此您不必承受使用費用。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-253">When you've finished this tutorial, you might want toodelete hello resources you created in hello tutorial, so you don't incur usage charges.</span></span> <span data-ttu-id="4f9d6-254">刪除資源群組時，也會刪除 hello 資源群組中的所有資源。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-254">Deleting a resource group also deletes all resources that are in hello resource group.</span></span>

### <span data-ttu-id="4f9d6-255"><a name="delete-portal"></a>Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="4f9d6-255"><a name="delete-portal"></a>Azure portal</span></span>

1. <span data-ttu-id="4f9d6-256">在 [hello] 入口網站搜尋方塊中，輸入**myResourceGroup**。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-256">In hello portal search box, enter **myResourceGroup**.</span></span> <span data-ttu-id="4f9d6-257">在 hello 搜尋結果中，按一下  **myResourceGroup**。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-257">In hello search results, click **myResourceGroup**.</span></span>
2. <span data-ttu-id="4f9d6-258">在 hello **myResourceGroup**刀鋒視窗中，按一下 hello**刪除**圖示。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-258">On hello **myResourceGroup** blade, click hello **Delete** icon.</span></span>
3. <span data-ttu-id="4f9d6-259">tooconfirm hello 刪除、 hello**類型 hello 資源群組名稱**方塊中，輸入**myResourceGroup**，然後按一下**刪除**。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-259">tooconfirm hello deletion, in hello **TYPE hello RESOURCE GROUP NAME** box, enter **myResourceGroup**, and then click **Delete**.</span></span>

### <span data-ttu-id="4f9d6-260"><a name="delete-cli"></a>Azure CLI</span><span class="sxs-lookup"><span data-stu-id="4f9d6-260"><a name="delete-cli"></a>Azure CLI</span></span>

1. <span data-ttu-id="4f9d6-261">使用下列命令的 hello hello Azure CLI 2.0 toodelete hello 虛擬網路 （資源管理員）：</span><span class="sxs-lookup"><span data-stu-id="4f9d6-261">Use hello Azure CLI 2.0 toodelete hello virtual network (Resource Manager) with hello following command:</span></span>

    ```azurecli-interactive
    az group delete --name myResourceGroup --yes
    ```

2. <span data-ttu-id="4f9d6-262">使用下列命令的 hello hello Azure CLI 1.0 toodelete hello 虛擬網路 （傳統）：</span><span class="sxs-lookup"><span data-stu-id="4f9d6-262">Use hello Azure CLI 1.0 toodelete hello virtual network (classic) with hello following commands:</span></span>

    ```azurecli
    azure config mode asm

    azure network vnet delete --vnet myVnet2 --quiet
    ```

### <span data-ttu-id="4f9d6-263"><a name="delete-powershell"></a>PowerShell</span><span class="sxs-lookup"><span data-stu-id="4f9d6-263"><a name="delete-powershell"></a>PowerShell</span></span>

1. <span data-ttu-id="4f9d6-264">輸入下列命令 toodelete hello 虛擬網路 （資源管理員） 的 hello:</span><span class="sxs-lookup"><span data-stu-id="4f9d6-264">Enter hello following command toodelete hello virtual network (Resource Manager):</span></span>

    ```powershell
    Remove-AzureRmResourceGroup -Name myResourceGroup -Force
    ```

2. <span data-ttu-id="4f9d6-265">toodelete hello 虛擬網路 （傳統） 使用 PowerShell，您必須修改現有的網路組態檔。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-265">toodelete hello virtual network (classic) with PowerShell, you must modify an existing network configuration file.</span></span> <span data-ttu-id="4f9d6-266">了解如何太[匯出、 更新和匯入網路組態檔](virtual-networks-using-network-configuration-file.md)。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-266">Learn how too[export, update, and import network configuration files](virtual-networks-using-network-configuration-file.md).</span></span> <span data-ttu-id="4f9d6-267">移除下列 hello 這個教學課程中使用的虛擬網路的 VirtualNetworkSite 元素 hello:</span><span class="sxs-lookup"><span data-stu-id="4f9d6-267">Remove hello following VirtualNetworkSite element for hello virtual network used in this tutorial:</span></span>

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
    > <span data-ttu-id="4f9d6-268">匯入已變更的網路組態檔，可能會導致變更 tooexisting （傳統） 您的訂用帳戶中的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-268">Importing a changed network configuration file can cause changes tooexisting virtual networks (classic) in your subscription.</span></span> <span data-ttu-id="4f9d6-269">請務必僅卸除 hello 的上一個虛擬網路，且您不變更或移除您的訂用帳戶中的任何其他現有的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-269">Ensure you only remove hello previous virtual network and that you don't change or remove any other existing virtual networks from your subscription.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="4f9d6-270">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4f9d6-270">Next steps</span></span>

- <span data-ttu-id="4f9d6-271">請先徹底熟悉重要[虛擬網路對等互連的條件約束和行為](virtual-network-manage-peering.md#requirements-and-constraints)，再建立虛擬網路對等互連以供生產環境使用。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-271">Thoroughly familiarize yourself with important [virtual network peering constraints and behaviors](virtual-network-manage-peering.md#requirements-and-constraints) before creating a virtual network peering for production use.</span></span>
- <span data-ttu-id="4f9d6-272">了解所有[虛擬網路對等互連設定](virtual-network-manage-peering.md#create-a-peering)。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-272">Learn about all [virtual network peering settings](virtual-network-manage-peering.md#create-a-peering).</span></span>
- <span data-ttu-id="4f9d6-273">了解如何太[建立中樞和支點網路拓樸](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering)與虛擬網路對等互連。</span><span class="sxs-lookup"><span data-stu-id="4f9d6-273">Learn how too[create a hub and spoke network topology](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) with virtual network peering.</span></span>
