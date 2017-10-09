---
title: "aaaCreate 多個子網路的 Azure 虛擬網路 |Microsoft 文件"
description: "深入了解如何 toocreate 具有多個子網路，在 Azure 中的虛擬網路。"
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4ad679a4-a959-4e48-a317-d9f5655a442b
ms.service: virtual-network
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/26/2017
ms.author: jdial
ms.custom: 
ms.openlocfilehash: 0f56fa6ac24537d33b8e217f5b03f387826ab487
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-with-multiple-subnets"></a><span data-ttu-id="09697-103">建立有多個子網路的虛擬網路</span><span class="sxs-lookup"><span data-stu-id="09697-103">Create a virtual network with multiple subnets</span></span>

<span data-ttu-id="09697-104">在本教學課程，了解如何 toocreate 基本 Azure 虛擬網路具有不同公用和私用子網路。</span><span class="sxs-lookup"><span data-stu-id="09697-104">In this tutorial, learn how toocreate a basic Azure virtual network that has separate public and private subnets.</span></span> <span data-ttu-id="09697-105">您可以在子網路中建立各種 Azure 資源 (如虛擬機器、App Service 環境、虛擬機器擴展集、Azure HDInsight 及雲端服務)。</span><span class="sxs-lookup"><span data-stu-id="09697-105">You can create Azure resources, like Virtual machines, App Service environments, Virtual machine scale sets, Azure HDInsight, and Cloud services in a subnet.</span></span> <span data-ttu-id="09697-106">虛擬網路中的資源可以進行通訊與彼此、 與其他網路連線的 tooa 虛擬網路中的資源。</span><span class="sxs-lookup"><span data-stu-id="09697-106">Resources in virtual networks can communicate with each other and with resources in other networks connected tooa virtual network.</span></span>

<span data-ttu-id="09697-107">hello 以下各節包含的步驟，toocreate 虛擬網路使用 hello [Azure 入口網站](#portal)，hello Azure 命令列介面 ([Azure CLI](#azure-cli))， [Azure PowerShell](#powershell)，和[Azure Resource Manager 範本](#resource-manager-template)。</span><span class="sxs-lookup"><span data-stu-id="09697-107">hello following sections include steps that you can take toocreate a virtual network by using hello [Azure portal](#portal), hello Azure command-line interface ([Azure CLI](#azure-cli)), [Azure PowerShell](#powershell), and an [Azure Resource Manager template](#resource-manager-template).</span></span> <span data-ttu-id="09697-108">hello 結果為的 hello 相同，而不論您使用 toocreate hello 虛擬網路的工具。</span><span class="sxs-lookup"><span data-stu-id="09697-108">hello result is hello same, regardless of which tool you use toocreate hello virtual network.</span></span> <span data-ttu-id="09697-109">按一下任何一個工具連結 toogo toothat hello 教學課程。</span><span class="sxs-lookup"><span data-stu-id="09697-109">Click a tool link toogo toothat section of hello tutorial.</span></span> <span data-ttu-id="09697-110">深入了解所有[虛擬網路](virtual-network-manage-network.md)和[子網路](virtual-network-manage-subnet.md)設定。</span><span class="sxs-lookup"><span data-stu-id="09697-110">Learn more about all [virtual network](virtual-network-manage-network.md) and [subnet](virtual-network-manage-subnet.md) settings.</span></span>

<span data-ttu-id="09697-111">本文提供步驟 toocreate hello Resource Manager 部署模型，也就是 hello 部署模型，我們建議您建立新的虛擬網路時，使用透過虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="09697-111">This article provides steps toocreate a virtual network through hello Resource Manager deployment model, which is hello deployment model we recommend using when creating new virtual networks.</span></span> <span data-ttu-id="09697-112">如果您需要 toocreate 虛擬網路 （傳統），請參閱[建立虛擬網路 （傳統）](create-virtual-network-classic.md)。</span><span class="sxs-lookup"><span data-stu-id="09697-112">If you need toocreate a virtual network (classic), see [Create a virtual network (classic)](create-virtual-network-classic.md).</span></span> <span data-ttu-id="09697-113">如果您不熟悉 Azure 部署模型，請參閱[了解 Azure 部署模型](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="09697-113">If you're not familiar with Azure's deployment models, see [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>

## <span data-ttu-id="09697-114"><a name="portal"></a>Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="09697-114"><a name="portal"></a>Azure portal</span></span>

1. <span data-ttu-id="09697-115">在網際網路瀏覽器，移 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="09697-115">In an Internet browser, go toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="09697-116">使用您的 [Azure 帳戶](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account)登入。</span><span class="sxs-lookup"><span data-stu-id="09697-116">Log in using your [Azure account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="09697-117">如果您沒有 Azure 帳戶，您可以註冊 [免費試用](https://azure.microsoft.com/offers/ms-azr-0044p)。</span><span class="sxs-lookup"><span data-stu-id="09697-117">If you don't have an Azure account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
2. <span data-ttu-id="09697-118">在 hello 入口網站中，按一下  **+ 新增** > **網路** > **虛擬網路**。</span><span class="sxs-lookup"><span data-stu-id="09697-118">In hello portal, click **+New** > **Networking** > **Virtual network**.</span></span>
3. <span data-ttu-id="09697-119">在 hello**建立虛擬網路**刀鋒視窗中，輸入下列值的 hello，然後按一下**建立**:</span><span class="sxs-lookup"><span data-stu-id="09697-119">On hello **Create virtual network** blade, enter hello following values, and then click **Create**:</span></span>

    |<span data-ttu-id="09697-120">設定</span><span class="sxs-lookup"><span data-stu-id="09697-120">Setting</span></span>|<span data-ttu-id="09697-121">值</span><span class="sxs-lookup"><span data-stu-id="09697-121">Value</span></span>|
    |---|---|
    |<span data-ttu-id="09697-122">名稱</span><span class="sxs-lookup"><span data-stu-id="09697-122">Name</span></span>|<span data-ttu-id="09697-123">myVnet</span><span class="sxs-lookup"><span data-stu-id="09697-123">myVnet</span></span>|
    |<span data-ttu-id="09697-124">位址空間</span><span class="sxs-lookup"><span data-stu-id="09697-124">Address space</span></span>|<span data-ttu-id="09697-125">10.0.0.0/16</span><span class="sxs-lookup"><span data-stu-id="09697-125">10.0.0.0/16</span></span>|
    |<span data-ttu-id="09697-126">子網路名稱</span><span class="sxs-lookup"><span data-stu-id="09697-126">Subnet name</span></span>|<span data-ttu-id="09697-127">公開</span><span class="sxs-lookup"><span data-stu-id="09697-127">Public</span></span>|
    |<span data-ttu-id="09697-128">子網路位址範圍</span><span class="sxs-lookup"><span data-stu-id="09697-128">Subnet address range</span></span>|<span data-ttu-id="09697-129">10.0.0.0/24</span><span class="sxs-lookup"><span data-stu-id="09697-129">10.0.0.0/24</span></span>|
    |<span data-ttu-id="09697-130">資源群組</span><span class="sxs-lookup"><span data-stu-id="09697-130">Resource group</span></span>|<span data-ttu-id="09697-131">讓 [新建] 保持選取狀態，然後輸入 **myResourceGroup**。</span><span class="sxs-lookup"><span data-stu-id="09697-131">Leave **Create new** selected, and then enter **myResourceGroup**.</span></span>|
    |<span data-ttu-id="09697-132">訂用帳戶和位置</span><span class="sxs-lookup"><span data-stu-id="09697-132">Subscription and location</span></span>|<span data-ttu-id="09697-133">選取您的訂用帳戶和位置。</span><span class="sxs-lookup"><span data-stu-id="09697-133">Select your subscription and location.</span></span>

    <span data-ttu-id="09697-134">如果您是新 tooAzure，深入了解[資源群組](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group)，[訂閱](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription)，和[位置](https://azure.microsoft.com/regions)(也稱為 tooas*區域*)。</span><span class="sxs-lookup"><span data-stu-id="09697-134">If you're new tooAzure, learn more about [resource groups](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [subscriptions](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), and [locations](https://azure.microsoft.com/regions) (also referred tooas *regions*).</span></span>
4. <span data-ttu-id="09697-135">在 hello 入口網站中，您可以建立只有一個子網路時建立虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="09697-135">In hello portal, you can create only one subnet when you create a virtual network.</span></span> <span data-ttu-id="09697-136">在本教學課程中，您會建立第二個子網路之後建立 hello 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="09697-136">In this tutorial, you create a second subnet after you create hello virtual network.</span></span> <span data-ttu-id="09697-137">您稍後可能會建立可存取網際網路資源 hello**公用**子網路。</span><span class="sxs-lookup"><span data-stu-id="09697-137">You might later create Internet-accessible resources in hello **Public** subnet.</span></span> <span data-ttu-id="09697-138">您也可以建立不是可從在 hello hello 網際網路存取的資源**私人**子網路。</span><span class="sxs-lookup"><span data-stu-id="09697-138">You also might create resources that aren't accessible from hello Internet in hello **Private** subnet.</span></span> <span data-ttu-id="09697-139">toocreate hello 第二個中的子網路，hello**搜尋資源**hello hello 頁頂端的方塊中，輸入**myVnet**。</span><span class="sxs-lookup"><span data-stu-id="09697-139">toocreate hello second subnet, in hello **Search resources** box at hello top of hello page, enter **myVnet**.</span></span> <span data-ttu-id="09697-140">在 hello 搜尋結果中，按一下  **myVnet**。</span><span class="sxs-lookup"><span data-stu-id="09697-140">In hello search results, click **myVnet**.</span></span> <span data-ttu-id="09697-141">如果您有多個虛擬網路與 hello 您訂用帳戶中的相同名稱，請檢查 hello 列在每個虛擬網路的資源群組。</span><span class="sxs-lookup"><span data-stu-id="09697-141">If you have multiple virtual networks with hello same name in your subscription, check hello resource groups that are listed under each virtual network.</span></span> <span data-ttu-id="09697-142">請確定您按一下 hello **myVnet**搜尋具有 hello 資源群組的結果**myResourceGroup**。</span><span class="sxs-lookup"><span data-stu-id="09697-142">Ensure that you click hello **myVnet** search result that has hello resource group **myResourceGroup**.</span></span>
5. <span data-ttu-id="09697-143">在 hello **myVnet**刀鋒視窗底下**設定**，按一下**子網路**。</span><span class="sxs-lookup"><span data-stu-id="09697-143">On hello **myVnet** blade, under **SETTINGS**, click **Subnets**.</span></span>
6. <span data-ttu-id="09697-144">在 hello **myVnet-子網路**刀鋒視窗中，按一下  **+ 子網路**。</span><span class="sxs-lookup"><span data-stu-id="09697-144">On hello **myVnet - Subnets** blade, click **+Subnet**.</span></span>
7. <span data-ttu-id="09697-145">在 hello**加入子網路**刀鋒視窗中，針對**名稱**，輸入**私用**。</span><span class="sxs-lookup"><span data-stu-id="09697-145">On hello **Add subnet** blade, for **Name**, enter **Private**.</span></span> <span data-ttu-id="09697-146">對 [位址範圍] 輸入 **10.0.1.0/24**。</span><span class="sxs-lookup"><span data-stu-id="09697-146">For **Address range**, enter **10.0.1.0/24**.</span></span>  <span data-ttu-id="09697-147">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="09697-147">Click **OK**.</span></span>
8. <span data-ttu-id="09697-148">在 hello **myVnet-子網路**刀鋒視窗中，檢閱 hello 子網路。</span><span class="sxs-lookup"><span data-stu-id="09697-148">On hello **myVnet - Subnets** blade, review hello subnets.</span></span> <span data-ttu-id="09697-149">您可以看到 hello**公用**和**私人**您所建立的子網路。</span><span class="sxs-lookup"><span data-stu-id="09697-149">You can see hello **Public** and **Private** subnets that you created.</span></span>
9. <span data-ttu-id="09697-150">**選擇性：** toodelete hello 您在本教學課程中建立的資源，步驟完成 hello[刪除資源](#delete-portal)本文中。</span><span class="sxs-lookup"><span data-stu-id="09697-150">**Optional:** toodelete hello resources that you create in this tutorial, complete hello steps in [Delete resources](#delete-portal) in this article.</span></span>

## <a name="azure-cli"></a><span data-ttu-id="09697-151">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="09697-151">Azure CLI</span></span>

<span data-ttu-id="09697-152">Azure CLI 命令都 hello 相同，無論您從 Windows、 Linux 或 macOS 執行 hello 命令。</span><span class="sxs-lookup"><span data-stu-id="09697-152">Azure CLI commands are hello same, whether you execute hello commands from Windows, Linux, or macOS.</span></span> <span data-ttu-id="09697-153">不過，不同作業系統殼層的指令碼編寫會有差異。</span><span class="sxs-lookup"><span data-stu-id="09697-153">However, there are scripting differences between operating system shells.</span></span> <span data-ttu-id="09697-154">Bash 殼層中，執行 hello 步驟中的 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="09697-154">hello script in hello following steps executes in a Bash shell.</span></span> 

1. <span data-ttu-id="09697-155">[安裝和設定 hello Azure CLI](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="09697-155">[Install and configure hello Azure CLI](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="09697-156">確定您擁有 hello hello Azure CLI 安裝最新版本。</span><span class="sxs-lookup"><span data-stu-id="09697-156">Ensure you have hello most recent version of hello Azure CLI installed.</span></span> <span data-ttu-id="09697-157">CLI 命令的 tooget 說明輸入`az <command> --help`。</span><span class="sxs-lookup"><span data-stu-id="09697-157">tooget help for CLI commands, type `az <command> --help`.</span></span> <span data-ttu-id="09697-158">而不是安裝 hello CLI 和其必要元件，您可以使用 hello Azure 雲端殼層。</span><span class="sxs-lookup"><span data-stu-id="09697-158">Rather than installing hello CLI and its pre-requisites, you can use hello Azure Cloud Shell.</span></span> <span data-ttu-id="09697-159">hello Azure 雲端殼層是免費的 Bash 殼層，您可以直接在 hello Azure 入口網站中執行。</span><span class="sxs-lookup"><span data-stu-id="09697-159">hello Azure Cloud Shell is a free Bash shell that you can run directly within hello Azure portal.</span></span> <span data-ttu-id="09697-160">hello 雲端殼層有的 hello Azure CLI 預先安裝和設定 toouse 與您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="09697-160">hello Cloud Shell has hello Azure CLI preinstalled and configured toouse with your account.</span></span> <span data-ttu-id="09697-161">toouse hello 雲端 Shell 中，按一下 hello 雲端殼層 (**> _**) 在 hello hello 最上方的按鈕[入口網站](https://portal.azure.com)或直接按一下 hello*試試*hello 遵循的步驟中的按鈕。</span><span class="sxs-lookup"><span data-stu-id="09697-161">toouse hello Cloud Shell, click hello Cloud Shell (**>_**) button at hello top of hello [portal](https://portal.azure.com) or just click hello *Try it* button in hello steps that follow.</span></span> 
2. <span data-ttu-id="09697-162">如果在本機執行 hello CLI，請登入以 hello tooAzure`az login`命令。</span><span class="sxs-lookup"><span data-stu-id="09697-162">If running hello CLI locally, log in tooAzure with hello `az login` command.</span></span> <span data-ttu-id="09697-163">如果使用 hello 雲端殼層，您已登入。</span><span class="sxs-lookup"><span data-stu-id="09697-163">If using hello Cloud Shell, you're already logged in.</span></span>
3. <span data-ttu-id="09697-164">檢閱 hello 下列指令碼和其註解。</span><span class="sxs-lookup"><span data-stu-id="09697-164">Review hello following script and its comments.</span></span> <span data-ttu-id="09697-165">在瀏覽器中將 hello 指令碼複製並貼到您的 CLI 工作階段：</span><span class="sxs-lookup"><span data-stu-id="09697-165">In your browser, copy hello script and paste it into your CLI session:</span></span>

    ```azurecli-interactive
    #!/bin/bash
    
    # Create a resource group.
    az group create \
      --name myResourceGroup \
      --location eastus
    
    # Create a virtual network with one subnet named Public.
    az network vnet create \
      --name myVnet \
      --resource-group myResourceGroup \
      --subnet-name Public
    
    # Create an additional subnet named Private in hello virtual network.
    az network vnet subnet create \
      --name Private \
      --address-prefix 10.0.1.0/24 \
      --vnet-name myVnet \
      --resource-group myResourceGroup
    ```
    
4. <span data-ttu-id="09697-166">Hello 指令碼完成時執行，請檢閱 hello hello 虛擬網路的子網路。</span><span class="sxs-lookup"><span data-stu-id="09697-166">When hello script is finished running, review hello subnets for hello virtual network.</span></span> <span data-ttu-id="09697-167">複製下列命令，hello 並貼到您的 CLI 工作階段中：</span><span class="sxs-lookup"><span data-stu-id="09697-167">Copy hello following command, and then paste it into your CLI session:</span></span>

    ```azurecli
    az network vnet subnet list --resource-group myResourceGroup --vnet-name myVnet --output table
    ```

5. <span data-ttu-id="09697-168">**選擇性**: toodelete hello 您在本教學課程中建立的資源，步驟完成 hello[刪除資源](#delete-cli)本文中。</span><span class="sxs-lookup"><span data-stu-id="09697-168">**Optional**: toodelete hello resources that you create in this tutorial, complete hello steps in [Delete resources](#delete-cli) in this article.</span></span>

## <a name="powershell"></a><span data-ttu-id="09697-169">PowerShell</span><span class="sxs-lookup"><span data-stu-id="09697-169">PowerShell</span></span>

1. <span data-ttu-id="09697-170">安裝 hello hello PowerShell 最新版本[AzureRm](https://www.powershellgallery.com/packages/AzureRM/)模組。</span><span class="sxs-lookup"><span data-stu-id="09697-170">Install hello latest version of hello PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) module.</span></span> <span data-ttu-id="09697-171">如果您是新 tooAzure PowerShell，請參閱[Azure PowerShell 概觀](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="09697-171">If you're new tooAzure PowerShell, see [Azure PowerShell overview](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="09697-172">在 PowerShell 工作階段中，登入與 tooAzure 您[Azure 帳戶](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account)使用 hello`login-azurermaccount`命令。</span><span class="sxs-lookup"><span data-stu-id="09697-172">In a PowerShell session, log in tooAzure with your [Azure account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account) using hello `login-azurermaccount` command.</span></span>

3. <span data-ttu-id="09697-173">檢閱 hello 下列指令碼和其註解。</span><span class="sxs-lookup"><span data-stu-id="09697-173">Review hello following script and its comments.</span></span> <span data-ttu-id="09697-174">在瀏覽器中將 hello 指令碼複製並貼到您的 PowerShell 工作階段：</span><span class="sxs-lookup"><span data-stu-id="09697-174">In your browser, copy hello script and paste it into your PowerShell session:</span></span>

    ```powershell
    # Create a resource group.
    New-AzureRmResourceGroup `
      -Name myResourceGroup `
      -Location eastus
    
    # Create hello public and private subnets.
    $Subnet1 = New-AzureRmVirtualNetworkSubnetConfig `
      -Name Public `
      -AddressPrefix 10.0.0.0/24
    $Subnet2 = New-AzureRmVirtualNetworkSubnetConfig `
      -Name Private `
      -AddressPrefix 10.0.1.0/24
    
    # Create a virtual network.
    $Vnet=New-AzureRmVirtualNetwork `
      -ResourceGroupName myResourceGroup `
      -Location eastus `
      -Name myVnet `
      -AddressPrefix 10.0.0.0/16 `
      -Subnet $Subnet1,$Subnet2
    ```

4. <span data-ttu-id="09697-175">tooreview hello hello 虛擬網路子網路複製 hello 下列命令，並貼到您的 PowerShell 工作階段中：</span><span class="sxs-lookup"><span data-stu-id="09697-175">tooreview hello subnets for hello virtual network, copy hello following command, and then paste it into your PowerShell session:</span></span>

    ```powershell
    $Vnet.subnets | Format-Table Name, AddressPrefix
    ```

5. <span data-ttu-id="09697-176">**選擇性**: toodelete hello 您在本教學課程中建立的資源，步驟完成 hello[刪除資源](#delete-powershell)本文中。</span><span class="sxs-lookup"><span data-stu-id="09697-176">**Optional**: toodelete hello resources that you create in this tutorial, complete hello steps in [Delete resources](#delete-powershell) in this article.</span></span>

## <a name="resource-manager-template"></a><span data-ttu-id="09697-177">Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="09697-177">Resource Manager template</span></span>

<span data-ttu-id="09697-178">您可以使用 Azure Resource Manager 範本來部署虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="09697-178">You can deploy a virtual network by using an Azure Resource Manager template.</span></span> <span data-ttu-id="09697-179">toolearn 進一步了解範本，請參閱[什麼是資源管理員](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#template-deployment)。</span><span class="sxs-lookup"><span data-stu-id="09697-179">toolearn more about templates, see [What is Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#template-deployment).</span></span> <span data-ttu-id="09697-180">tooaccess hello 範本和 toolearn 有關它的參數，請參閱 hello[建立具有兩個子網路的虛擬網路](https://azure.microsoft.com/resources/templates/101-vnet-two-subnets/)範本。</span><span class="sxs-lookup"><span data-stu-id="09697-180">tooaccess hello template and toolearn about its parameters, see hello [Create a virtual network with two subnets](https://azure.microsoft.com/resources/templates/101-vnet-two-subnets/) template.</span></span> <span data-ttu-id="09697-181">您可以部署 hello 範本使用 hello[入口網站](#template-portal)， [Azure CLI](#template-cli)，或[PowerShell](#template-powershell)。</span><span class="sxs-lookup"><span data-stu-id="09697-181">You can deploy hello template by using hello [portal](#template-portal), [Azure CLI](#template-cli), or [PowerShell](#template-powershell).</span></span>

<span data-ttu-id="09697-182">**選擇性：** toodelete hello 您在本教學課程中建立的資源，步驟的任何小節中的完整 hello[刪除資源](#delete)本文中。</span><span class="sxs-lookup"><span data-stu-id="09697-182">**Optional:** toodelete hello resources that you create in this tutorial, complete hello steps in any subsections of [Delete resources](#delete) in this article.</span></span>

### <span data-ttu-id="09697-183"><a name="template-portal"></a>Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="09697-183"><a name="template-portal"></a>Azure portal</span></span>

1. <span data-ttu-id="09697-184">在瀏覽器中，開啟 hello[範本頁面](https://azure.microsoft.com/resources/templates/101-vnet-two-subnets)。</span><span class="sxs-lookup"><span data-stu-id="09697-184">In your browser, open hello [template page](https://azure.microsoft.com/resources/templates/101-vnet-two-subnets).</span></span>
2. <span data-ttu-id="09697-185">按一下 hello**部署 tooAzure**  按鈕。</span><span class="sxs-lookup"><span data-stu-id="09697-185">Click hello **Deploy tooAzure** button.</span></span> <span data-ttu-id="09697-186">如果您未登入 tooAzure，在出現的 hello Azure 入口網站的登入畫面上登入。</span><span class="sxs-lookup"><span data-stu-id="09697-186">If you're not already logged in tooAzure, log in on hello Azure portal login screen that appears.</span></span>
3. <span data-ttu-id="09697-187">使用登入 toohello 入口網站您[Azure 帳戶](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account)。</span><span class="sxs-lookup"><span data-stu-id="09697-187">Sign in toohello portal by using your [Azure account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="09697-188">如果您沒有 Azure 帳戶，您可以註冊 [免費試用](https://azure.microsoft.com/offers/ms-azr-0044p)。</span><span class="sxs-lookup"><span data-stu-id="09697-188">If you don't have an Azure account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
4. <span data-ttu-id="09697-189">輸入 hello 遵循 hello 參數的值：</span><span class="sxs-lookup"><span data-stu-id="09697-189">Enter hello following values for hello parameters:</span></span>

    |<span data-ttu-id="09697-190">參數</span><span class="sxs-lookup"><span data-stu-id="09697-190">Parameter</span></span>|<span data-ttu-id="09697-191">值</span><span class="sxs-lookup"><span data-stu-id="09697-191">Value</span></span>|
    |---|---|
    |<span data-ttu-id="09697-192">訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="09697-192">Subscription</span></span>|<span data-ttu-id="09697-193">選取您的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="09697-193">Select your subscription</span></span>|
    |<span data-ttu-id="09697-194">資源群組</span><span class="sxs-lookup"><span data-stu-id="09697-194">Resource group</span></span>|<span data-ttu-id="09697-195">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="09697-195">myResourceGroup</span></span>|
    |<span data-ttu-id="09697-196">位置</span><span class="sxs-lookup"><span data-stu-id="09697-196">Location</span></span>|<span data-ttu-id="09697-197">選取位置</span><span class="sxs-lookup"><span data-stu-id="09697-197">Select a location</span></span>|
    |<span data-ttu-id="09697-198">Vnet 名稱</span><span class="sxs-lookup"><span data-stu-id="09697-198">Vnet Name</span></span>|<span data-ttu-id="09697-199">myVnet</span><span class="sxs-lookup"><span data-stu-id="09697-199">myVnet</span></span>|
    |<span data-ttu-id="09697-200">Vnet 位址首碼</span><span class="sxs-lookup"><span data-stu-id="09697-200">Vnet Address Prefix</span></span>|<span data-ttu-id="09697-201">10.0.0.0/16</span><span class="sxs-lookup"><span data-stu-id="09697-201">10.0.0.0/16</span></span>|
    |<span data-ttu-id="09697-202">Subnet1Prefix</span><span class="sxs-lookup"><span data-stu-id="09697-202">Subnet1Prefix</span></span>|<span data-ttu-id="09697-203">10.0.0.0/24</span><span class="sxs-lookup"><span data-stu-id="09697-203">10.0.0.0/24</span></span>|
    |<span data-ttu-id="09697-204">Subnet1Name</span><span class="sxs-lookup"><span data-stu-id="09697-204">Subnet1Name</span></span>|<span data-ttu-id="09697-205">公開</span><span class="sxs-lookup"><span data-stu-id="09697-205">Public</span></span>|
    |<span data-ttu-id="09697-206">Subnet2Prefix</span><span class="sxs-lookup"><span data-stu-id="09697-206">Subnet2Prefix</span></span>|<span data-ttu-id="09697-207">10.0.1.0/24</span><span class="sxs-lookup"><span data-stu-id="09697-207">10.0.1.0/24</span></span>|
    |<span data-ttu-id="09697-208">Subnet2Name</span><span class="sxs-lookup"><span data-stu-id="09697-208">Subnet2Name</span></span>|<span data-ttu-id="09697-209">私人</span><span class="sxs-lookup"><span data-stu-id="09697-209">Private</span></span>|

5. <span data-ttu-id="09697-210">同意 toohello 條款和條件，然後再按 **購買**toodeploy hello 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="09697-210">Agree toohello terms and conditions, and then click **Purchase** toodeploy hello virtual network.</span></span>

### <span data-ttu-id="09697-211"><a name="template-cli"></a>Azure CLI</span><span class="sxs-lookup"><span data-stu-id="09697-211"><a name="template-cli"></a>Azure CLI</span></span>

1. <span data-ttu-id="09697-212">[安裝和設定 hello Azure CLI](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="09697-212">[Install and configure hello Azure CLI](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="09697-213">確定您擁有 hello hello Azure CLI 安裝最新版本。</span><span class="sxs-lookup"><span data-stu-id="09697-213">Ensure you have hello most recent version of hello Azure CLI installed.</span></span> <span data-ttu-id="09697-214">CLI 命令的 tooget 說明輸入`az <command> --help`。</span><span class="sxs-lookup"><span data-stu-id="09697-214">tooget help for CLI commands, type `az <command> --help`.</span></span> <span data-ttu-id="09697-215">而不是安裝 hello CLI 和其必要元件，您可以使用 hello Azure 雲端殼層。</span><span class="sxs-lookup"><span data-stu-id="09697-215">Rather than installing hello CLI and its pre-requisites, you can use hello Azure Cloud Shell.</span></span> <span data-ttu-id="09697-216">hello Azure 雲端殼層是免費的 Bash 殼層，您可以直接在 hello Azure 入口網站中執行。</span><span class="sxs-lookup"><span data-stu-id="09697-216">hello Azure Cloud Shell is a free Bash shell that you can run directly within hello Azure portal.</span></span> <span data-ttu-id="09697-217">hello 雲端殼層有的 hello Azure CLI 預先安裝和設定 toouse 與您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="09697-217">hello Cloud Shell has hello Azure CLI preinstalled and configured toouse with your account.</span></span> <span data-ttu-id="09697-218">toouse hello 雲端 Shell 中，按一下 hello 雲端殼層**> _**按鈕上方的 hello hello[入口網站](https://portal.azure.com)，或直接按一下 hello**試試**hello 遵循的步驟中的按鈕。</span><span class="sxs-lookup"><span data-stu-id="09697-218">toouse hello Cloud Shell, click hello Cloud Shell **>_** button at hello top of hello [portal](https://portal.azure.com), or just click hello **Try it** button in hello steps that follow.</span></span> 
2. <span data-ttu-id="09697-219">如果在本機執行 hello CLI，請登入以 hello tooAzure`az login`命令。</span><span class="sxs-lookup"><span data-stu-id="09697-219">If running hello CLI locally, log in tooAzure with hello `az login` command.</span></span> <span data-ttu-id="09697-220">如果使用 hello 雲端殼層，您已登入。</span><span class="sxs-lookup"><span data-stu-id="09697-220">If using hello Cloud Shell, you're already logged in.</span></span>
3. <span data-ttu-id="09697-221">toocreate hello 虛擬網路的資源群組中，複製 hello 下列命令，並將它貼到您的 CLI 工作階段：</span><span class="sxs-lookup"><span data-stu-id="09697-221">toocreate a resource group for hello virtual network, copy hello following command and paste it into your CLI session:</span></span>

    ```azurecli-interactive
    az group create --name myResourceGroup --location eastus
    ```
    
4. <span data-ttu-id="09697-222">您可以使用下列參數選項的 hello 的其中一個部署 hello 範本：</span><span class="sxs-lookup"><span data-stu-id="09697-222">You can deploy hello template by using one of hello following parameters options:</span></span>
    - <span data-ttu-id="09697-223">**預設參數值**。</span><span class="sxs-lookup"><span data-stu-id="09697-223">**Default parameter values**.</span></span> <span data-ttu-id="09697-224">輸入下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="09697-224">Enter hello following command:</span></span>
    
        ```azurecli-interactive
        az group deployment create --resource-group myResourceGroup --name VnetTutorial --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vnet-two-subnets/azuredeploy.json`
        ```
    - <span data-ttu-id="09697-225">**自訂參數值**。</span><span class="sxs-lookup"><span data-stu-id="09697-225">**Custom parameter values**.</span></span> <span data-ttu-id="09697-226">下載並修改 hello 範本，再部署 hello 範本。</span><span class="sxs-lookup"><span data-stu-id="09697-226">Download and modify hello template before you deploy hello template.</span></span> <span data-ttu-id="09697-227">您也可以部署 hello 範本在 hello 命令列使用參數，或部署 hello 範本與個別參數檔案。</span><span class="sxs-lookup"><span data-stu-id="09697-227">You also can deploy hello template by using parameters at hello command line, or deploy hello template with a separate parameters file.</span></span> <span data-ttu-id="09697-228">toodownload hello 範本和參數檔案，按一下 hello**瀏覽 GitHub 上**按鈕 hello[建立具有兩個子網路的虛擬網路](https://azure.microsoft.com/resources/templates/101-vnet-two-subnets/)範本頁面。</span><span class="sxs-lookup"><span data-stu-id="09697-228">toodownload hello template and parameters files, click hello **Browse on GitHub** button on hello [Create a virtual network with two subnets](https://azure.microsoft.com/resources/templates/101-vnet-two-subnets/) template page.</span></span> <span data-ttu-id="09697-229">在 GitHub 中，按一下 hello **azuredeploy.parameters.json**或**azuredeploy.json**檔案。</span><span class="sxs-lookup"><span data-stu-id="09697-229">In GitHub, click hello **azuredeploy.parameters.json** or **azuredeploy.json** file.</span></span> <span data-ttu-id="09697-230">然後，按一下 hello **Raw**按鈕 toodisplay hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="09697-230">Then, click hello **Raw** button toodisplay hello file.</span></span> <span data-ttu-id="09697-231">在瀏覽器中，複製 hello hello 檔案內容。</span><span class="sxs-lookup"><span data-stu-id="09697-231">In your browser, copy hello contents of hello file.</span></span> <span data-ttu-id="09697-232">儲存您的電腦上的 hello 內容 tooa 檔案。</span><span class="sxs-lookup"><span data-stu-id="09697-232">Save hello contents tooa file on your computer.</span></span> <span data-ttu-id="09697-233">您可以修改 hello 範本中的 hello 參數值，或使用不同的參數檔案部署 hello 範本。</span><span class="sxs-lookup"><span data-stu-id="09697-233">You can modify hello parameter values in hello template, or deploy hello template with a separate parameters file.</span></span>  

    <span data-ttu-id="09697-234">toolearn 深入了解如何使用這些方法，toodeploy 範本鍵入`az group deployment create --help`。</span><span class="sxs-lookup"><span data-stu-id="09697-234">toolearn more about how toodeploy templates by using these methods, type `az group deployment create --help`.</span></span>

### <span data-ttu-id="09697-235"><a name="template-powershell"></a>PowerShell</span><span class="sxs-lookup"><span data-stu-id="09697-235"><a name="template-powershell"></a>PowerShell</span></span>

1. <span data-ttu-id="09697-236">安裝 hello hello PowerShell 最新版本[AzureRm](https://www.powershellgallery.com/packages/AzureRM/)模組。</span><span class="sxs-lookup"><span data-stu-id="09697-236">Install hello latest version of hello PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) module.</span></span> <span data-ttu-id="09697-237">如果您是新 tooAzure PowerShell，請參閱[Azure PowerShell 概觀](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="09697-237">If you're new tooAzure PowerShell, see [Azure PowerShell overview](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="09697-238">在 PowerShell 工作階段中使用 toosign 您[Azure 帳戶](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account)，輸入`login-azurermaccount`。</span><span class="sxs-lookup"><span data-stu-id="09697-238">In a PowerShell session, toosign in with your [Azure account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account), enter `login-azurermaccount`.</span></span>
3. <span data-ttu-id="09697-239">toocreate 資源群組 hello 虛擬網路，請輸入下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="09697-239">toocreate a resource group for hello virtual network, enter hello following command:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location eastus
    ```
    
4. <span data-ttu-id="09697-240">您可以使用下列參數選項的 hello 的其中一個部署 hello 範本：</span><span class="sxs-lookup"><span data-stu-id="09697-240">You can deploy hello template by using one of hello following parameters options:</span></span>
    - <span data-ttu-id="09697-241">**預設參數值**。</span><span class="sxs-lookup"><span data-stu-id="09697-241">**Default parameter values**.</span></span> <span data-ttu-id="09697-242">輸入下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="09697-242">Enter hello following command:</span></span>
    
        ```powershell
        New-AzureRmResourceGroupDeployment -Name VnetTutorial -ResourceGroupName myResourceGroup -TemplateUri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vnet-two-subnets/azuredeploy.json
        ```
        
    - <span data-ttu-id="09697-243">**自訂參數值**。</span><span class="sxs-lookup"><span data-stu-id="09697-243">**Custom parameter values**.</span></span> <span data-ttu-id="09697-244">下載並修改 hello 範本，再部署。</span><span class="sxs-lookup"><span data-stu-id="09697-244">Download and modify hello template before you deploy it.</span></span> <span data-ttu-id="09697-245">您也可以部署 hello 範本在 hello 命令列使用參數，或部署 hello 範本與個別參數檔案。</span><span class="sxs-lookup"><span data-stu-id="09697-245">You also can deploy hello template by using parameters at hello command line, or deploy hello template with a separate parameters file.</span></span> <span data-ttu-id="09697-246">toodownload hello 範本和參數檔案，按一下 hello**瀏覽 GitHub 上**按鈕 hello[建立具有兩個子網路的虛擬網路](https://azure.microsoft.com/resources/templates/101-vnet-two-subnets/)範本頁面。</span><span class="sxs-lookup"><span data-stu-id="09697-246">toodownload hello template and parameters files, click hello **Browse on GitHub** button on hello [Create a virtual network with two subnets](https://azure.microsoft.com/resources/templates/101-vnet-two-subnets/) template page.</span></span> <span data-ttu-id="09697-247">在 GitHub 中，按一下 hello **azuredeploy.parameters.json**或**azuredeploy.json**檔案。</span><span class="sxs-lookup"><span data-stu-id="09697-247">In GitHub, click hello **azuredeploy.parameters.json**  or **azuredeploy.json** file.</span></span> <span data-ttu-id="09697-248">然後，按一下 hello **Raw**按鈕 toodisplay hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="09697-248">Then, click hello **Raw** button toodisplay hello file.</span></span> <span data-ttu-id="09697-249">在瀏覽器中，複製 hello hello 檔案內容。</span><span class="sxs-lookup"><span data-stu-id="09697-249">In your browser, copy hello contents of hello file.</span></span> <span data-ttu-id="09697-250">儲存您的電腦上的 hello 內容 tooa 檔案。</span><span class="sxs-lookup"><span data-stu-id="09697-250">Save hello contents tooa file on your computer.</span></span> <span data-ttu-id="09697-251">您可以修改 hello 範本中的 hello 參數值，或使用不同的參數檔案部署 hello 範本。</span><span class="sxs-lookup"><span data-stu-id="09697-251">You can modify hello parameter values in hello template, or deploy hello template with a separate parameters file.</span></span>  

    <span data-ttu-id="09697-252">toolearn 深入了解如何使用這些方法，toodeploy 範本鍵入`Get-Help New-AzureRmResourceGroupDeployment`。</span><span class="sxs-lookup"><span data-stu-id="09697-252">toolearn more about how toodeploy templates by using these methods, type `Get-Help New-AzureRmResourceGroupDeployment`.</span></span> 

## <span data-ttu-id="09697-253"><a name="delete"></a>刪除資源</span><span class="sxs-lookup"><span data-stu-id="09697-253"><a name="delete"></a>Delete resources</span></span>

<span data-ttu-id="09697-254">當您完成本教學課程中時，您可能想 toodelete hello 資源，您所建立，如此您就不會產生使用費用。</span><span class="sxs-lookup"><span data-stu-id="09697-254">When you finish this tutorial, you might want toodelete hello resources that you created, so that you don't incur usage charges.</span></span> <span data-ttu-id="09697-255">刪除資源群組時，也會刪除 hello 資源群組中的所有資源。</span><span class="sxs-lookup"><span data-stu-id="09697-255">Deleting a resource group also deletes all resources that are in hello resource group.</span></span>

### <span data-ttu-id="09697-256"><a name="delete-portal"></a>Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="09697-256"><a name="delete-portal"></a>Azure portal</span></span>

1. <span data-ttu-id="09697-257">在 [hello] 入口網站搜尋方塊中，輸入**myResourceGroup**。</span><span class="sxs-lookup"><span data-stu-id="09697-257">In hello portal search box, enter **myResourceGroup**.</span></span> <span data-ttu-id="09697-258">在 hello 搜尋結果中，按一下  **myResourceGroup**。</span><span class="sxs-lookup"><span data-stu-id="09697-258">In hello search results, click **myResourceGroup**.</span></span>
2. <span data-ttu-id="09697-259">在 hello **myResourceGroup**刀鋒視窗中，按一下 hello**刪除**圖示。</span><span class="sxs-lookup"><span data-stu-id="09697-259">On hello **myResourceGroup** blade, click hello **Delete** icon.</span></span>
3. <span data-ttu-id="09697-260">tooconfirm hello 刪除、 hello**類型 hello 資源群組名稱**方塊中，輸入**myResourceGroup**，然後按一下**刪除**。</span><span class="sxs-lookup"><span data-stu-id="09697-260">tooconfirm hello deletion, in hello **TYPE hello RESOURCE GROUP NAME** box, enter **myResourceGroup**, and then click **Delete**.</span></span>

### <span data-ttu-id="09697-261"><a name="delete-cli"></a>Azure CLI</span><span class="sxs-lookup"><span data-stu-id="09697-261"><a name="delete-cli"></a>Azure CLI</span></span>

<span data-ttu-id="09697-262">CLI 工作階段中，輸入下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="09697-262">In a CLI session, enter hello following command:</span></span>

```azurecli-interactive
az group delete --name myResourceGroup --yes
```

### <span data-ttu-id="09697-263"><a name="delete-powershell"></a>PowerShell</span><span class="sxs-lookup"><span data-stu-id="09697-263"><a name="delete-powershell"></a>PowerShell</span></span>

<span data-ttu-id="09697-264">在 PowerShell 工作階段中，輸入下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="09697-264">In a PowerShell session, enter hello following command:</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="next-steps"></a><span data-ttu-id="09697-265">後續步驟</span><span class="sxs-lookup"><span data-stu-id="09697-265">Next steps</span></span>

- <span data-ttu-id="09697-266">toolearn 有關所有虛擬網路和子網路設定，請參閱[管理虛擬網路](virtual-network-manage-network.md#view-vnet)和[管理虛擬網路子網路](virtual-network-manage-subnet.md#create-subnet)。</span><span class="sxs-lookup"><span data-stu-id="09697-266">toolearn about all virtual network and subnet settings, see [Manage virtual networks](virtual-network-manage-network.md#view-vnet) and [Manage virtual network subnets](virtual-network-manage-subnet.md#create-subnet).</span></span> <span data-ttu-id="09697-267">您必須使用實際執行環境 toomeet 不同需求中的虛擬網路和子網路的各種選項。</span><span class="sxs-lookup"><span data-stu-id="09697-267">You have various options for using virtual networks and subnets in a production environment toomeet different requirements.</span></span>
- <span data-ttu-id="09697-268">輸入和輸出 toofilter 子網路的流量，建立和套用[網路安全性群組](virtual-networks-nsg.md)toosubnets。</span><span class="sxs-lookup"><span data-stu-id="09697-268">toofilter inbound and outbound subnet traffic, create and apply [network security groups](virtual-networks-nsg.md) toosubnets.</span></span>
- <span data-ttu-id="09697-269">建立[Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-network%2ftoc.json)或[Linux](../virtual-machines/linux/quick-create-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json)虛擬機器，然後將它連線 tooan 現有的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="09697-269">Create a [Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-network%2ftoc.json) or a [Linux](../virtual-machines/linux/quick-create-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) virtual machine, and then connect it tooan existing virtual network.</span></span>
- <span data-ttu-id="09697-270">tooconnect 兩個虛擬網路在 hello 相同的 Azure 位置中建立[虛擬網路對等互連](virtual-network-peering-overview.md)hello 虛擬網路之間。</span><span class="sxs-lookup"><span data-stu-id="09697-270">tooconnect two virtual networks in hello same Azure location, create a  [virtual network peering](virtual-network-peering-overview.md) between hello virtual networks.</span></span>
- <span data-ttu-id="09697-271">使用 hello 虛擬網路 tooan 在內部部署網路連線[VPN 閘道](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json)或[Azure ExpressRoute](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md?toc=%2fazure%2fvirtual-network%2ftoc.json)循環。</span><span class="sxs-lookup"><span data-stu-id="09697-271">Connect hello virtual network tooan on-premises network by using a [VPN Gateway](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) or [Azure ExpressRoute](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md?toc=%2fazure%2fvirtual-network%2ftoc.json) circuit.</span></span>
