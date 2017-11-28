---
title: "Azure 虛擬網路 （傳統） 含有多個子網路 aaaCreate |Microsoft 文件"
description: "深入了解如何 toocreate 在 Azure 中的多個子網路的虛擬網路 （傳統）。"
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: jdial
ms.custom: 
ms.openlocfilehash: cc7b9ad08d5c26dba09584762bedf614d2847032
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-classic-with-multiple-subnets"></a><span data-ttu-id="b8732-103">建立有多個子網路的虛擬網路 (傳統)</span><span class="sxs-lookup"><span data-stu-id="b8732-103">Create a virtual network (classic) with multiple subnets</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b8732-104">Azure 有二種建立和處理資源的[不同部署模型](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json)：Resource Manager 和傳統模型。</span><span class="sxs-lookup"><span data-stu-id="b8732-104">Azure has two [different deployment models](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) for creating and working with resources: Resource Manager and classic.</span></span> <span data-ttu-id="b8732-105">本文說明如何使用 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="b8732-105">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="b8732-106">Microsoft 建議您建立最新的虛擬網路透過 hello[資源管理員](virtual-networks-create-vnet-arm-pportal.md)部署模型。</span><span class="sxs-lookup"><span data-stu-id="b8732-106">Microsoft recommends creating most new virtual networks through hello [Resource Manager](virtual-networks-create-vnet-arm-pportal.md) deployment model.</span></span>

<span data-ttu-id="b8732-107">在本教學課程，了解如何 toocreate 基本的 Azure 虛擬網路 （傳統） 具有不同公用和私用子網路。</span><span class="sxs-lookup"><span data-stu-id="b8732-107">In this tutorial, learn how toocreate a basic Azure virtual network (classic) that has separate public and private subnets.</span></span> <span data-ttu-id="b8732-108">您可以在子網路中建立 Azure 資源，像是虛擬網路、雲端服務。</span><span class="sxs-lookup"><span data-stu-id="b8732-108">You can create Azure resources, like Virtual machines and Cloud services in a subnet.</span></span> <span data-ttu-id="b8732-109">建立虛擬網路 （傳統） 中的資源可以通訊，以及與其他網路連線的 tooa 虛擬網路中的資源。</span><span class="sxs-lookup"><span data-stu-id="b8732-109">Resources created in virtual networks (classic) can communicate with each other, and with resources in other networks connected tooa virtual network.</span></span>

<span data-ttu-id="b8732-110">深入了解所有[虛擬網路](virtual-network-manage-network.md)和[子網路](virtual-network-manage-subnet.md)設定。</span><span class="sxs-lookup"><span data-stu-id="b8732-110">Learn more about all [virtual network](virtual-network-manage-network.md) and [subnet](virtual-network-manage-subnet.md) settings.</span></span>

> [!WARNING]
> <span data-ttu-id="b8732-111">當[訂用帳戶停用](../billing/billing-subscription-become-disable.md?toc=%2fazure%2fvirtual-network%2ftoc.json#you-reached-your-spending-limit)時，Azure 會立即刪除虛擬網路 (傳統)。</span><span class="sxs-lookup"><span data-stu-id="b8732-111">Virtual networks (classic) are immediately deleted by Azure when a [subscription is disabled](../billing/billing-subscription-become-disable.md?toc=%2fazure%2fvirtual-network%2ftoc.json#you-reached-your-spending-limit).</span></span> <span data-ttu-id="b8732-112">不論資源是否存在 hello 虛擬網路中也會刪除虛擬網路 （傳統）。</span><span class="sxs-lookup"><span data-stu-id="b8732-112">Virtual networks (classic) are deleted regardless of whether resources exist in hello virtual network.</span></span> <span data-ttu-id="b8732-113">如果您稍後再重新啟用 hello 訂用帳戶，就必須重新建立 hello 虛擬網路中存在的資源。</span><span class="sxs-lookup"><span data-stu-id="b8732-113">If you later re-enable hello subscription, resources that existed in hello virtual network must be recreated.</span></span>

<span data-ttu-id="b8732-114">您可以建立虛擬網路 （傳統） 使用 hello [Azure 入口網站](#portal)，hello [Azure 命令列介面 (CLI) 1.0](#azure-cli)，或[PowerShell](#powershell)。</span><span class="sxs-lookup"><span data-stu-id="b8732-114">You can create a virtual network (classic) by using hello [Azure portal](#portal), hello [Azure command-line interface (CLI) 1.0](#azure-cli), or [PowerShell](#powershell).</span></span>

## <a name="portal"></a><span data-ttu-id="b8732-115">入口網站</span><span class="sxs-lookup"><span data-stu-id="b8732-115">Portal</span></span>

1. <span data-ttu-id="b8732-116">在網際網路瀏覽器，移 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="b8732-116">In an Internet browser, go toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="b8732-117">使用您的 [Azure 帳戶](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account)登入。</span><span class="sxs-lookup"><span data-stu-id="b8732-117">Log in using your [Azure account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account).</span></span> <span data-ttu-id="b8732-118">如果您沒有 Azure 帳戶，您可以註冊 [免費試用](https://azure.microsoft.com/offers/ms-azr-0044p)。</span><span class="sxs-lookup"><span data-stu-id="b8732-118">If you don't have an Azure account, you can sign up for a [free trial](https://azure.microsoft.com/offers/ms-azr-0044p).</span></span>
2. <span data-ttu-id="b8732-119">按一下**+ 新增**hello 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="b8732-119">Click **+New** in hello portal.</span></span>
3. <span data-ttu-id="b8732-120">輸入*虛擬網路*在 hello**搜尋 hello Marketplace**方塊上方的 hello hello**新增**刀鋒視窗中出現。</span><span class="sxs-lookup"><span data-stu-id="b8732-120">Enter *Virtual network* in hello **Search hello Marketplace** box at hello top of hello **New** blade that appears.</span></span>  <span data-ttu-id="b8732-121">按一下**虛擬網路**hello 搜尋結果中出現。</span><span class="sxs-lookup"><span data-stu-id="b8732-121">Click **Virtual network** when it appears in hello search results.</span></span>
4. <span data-ttu-id="b8732-122">選取**傳統**在 hello**選取部署模型**方塊中 hello**虛擬網路**刀鋒視窗中出現，然後按一下**建立**。</span><span class="sxs-lookup"><span data-stu-id="b8732-122">Select **Classic** in hello **Select a deployment model** box in hello **Virtual Network** blade that appears, then click **Create**.</span></span> 
5. <span data-ttu-id="b8732-123">輸入 hello 遵循 hello 值**建立虛擬網路 （傳統）**刀鋒視窗，然後按一下**建立**:</span><span class="sxs-lookup"><span data-stu-id="b8732-123">Enter hello following values on hello **Create virtual network (classic)** blade and then click **Create**:</span></span>

    |<span data-ttu-id="b8732-124">設定</span><span class="sxs-lookup"><span data-stu-id="b8732-124">Setting</span></span>|<span data-ttu-id="b8732-125">值</span><span class="sxs-lookup"><span data-stu-id="b8732-125">Value</span></span>|
    |---|---|
    |<span data-ttu-id="b8732-126">名稱</span><span class="sxs-lookup"><span data-stu-id="b8732-126">Name</span></span>|<span data-ttu-id="b8732-127">myVnet</span><span class="sxs-lookup"><span data-stu-id="b8732-127">myVnet</span></span>|
    |<span data-ttu-id="b8732-128">位址空間</span><span class="sxs-lookup"><span data-stu-id="b8732-128">Address space</span></span>|<span data-ttu-id="b8732-129">10.0.0.0/16</span><span class="sxs-lookup"><span data-stu-id="b8732-129">10.0.0.0/16</span></span>|
    |<span data-ttu-id="b8732-130">子網路名稱</span><span class="sxs-lookup"><span data-stu-id="b8732-130">Subnet name</span></span>|<span data-ttu-id="b8732-131">公開</span><span class="sxs-lookup"><span data-stu-id="b8732-131">Public</span></span>|
    |<span data-ttu-id="b8732-132">子網路位址範圍</span><span class="sxs-lookup"><span data-stu-id="b8732-132">Subnet address range</span></span>|<span data-ttu-id="b8732-133">10.0.0.0/24</span><span class="sxs-lookup"><span data-stu-id="b8732-133">10.0.0.0/24</span></span>|
    |<span data-ttu-id="b8732-134">資源群組</span><span class="sxs-lookup"><span data-stu-id="b8732-134">Resource group</span></span>|<span data-ttu-id="b8732-135">讓 [新建] 保持選取狀態，然後輸入 **myResourceGroup**。</span><span class="sxs-lookup"><span data-stu-id="b8732-135">Leave **Create new** selected, and then enter **myResourceGroup**.</span></span>|
    |<span data-ttu-id="b8732-136">訂用帳戶和位置</span><span class="sxs-lookup"><span data-stu-id="b8732-136">Subscription and location</span></span>|<span data-ttu-id="b8732-137">選取您的訂用帳戶和位置。</span><span class="sxs-lookup"><span data-stu-id="b8732-137">Select your subscription and location.</span></span>

    <span data-ttu-id="b8732-138">如果您是新 tooAzure，深入了解[資源群組](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group)，[訂閱](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription)，和[位置](https://azure.microsoft.com/regions)(也稱為 tooas*區域*)。</span><span class="sxs-lookup"><span data-stu-id="b8732-138">If you're new tooAzure, learn more about [resource groups](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [subscriptions](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), and [locations](https://azure.microsoft.com/regions) (also referred tooas *regions*).</span></span>
4. <span data-ttu-id="b8732-139">在 hello 入口網站中，您可以建立只有一個子網路時建立虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="b8732-139">In hello portal, you can create only one subnet when you create a virtual network.</span></span> <span data-ttu-id="b8732-140">在本教學課程中，您會建立第二個子網路之後建立 hello 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="b8732-140">In this tutorial, you create a second subnet after you create hello virtual network.</span></span> <span data-ttu-id="b8732-141">您稍後可能會建立可存取網際網路資源 hello**公用**子網路。</span><span class="sxs-lookup"><span data-stu-id="b8732-141">You might later create Internet-accessible resources in hello **Public** subnet.</span></span> <span data-ttu-id="b8732-142">您也可以建立不是可從在 hello hello 網際網路存取的資源**私人**子網路。</span><span class="sxs-lookup"><span data-stu-id="b8732-142">You also might create resources that aren't accessible from hello Internet in hello **Private** subnet.</span></span> <span data-ttu-id="b8732-143">toocreate hello 第二個子網路中，輸入**myVnet**在 hello**搜尋資源**hello hello 頁頂端的方塊。</span><span class="sxs-lookup"><span data-stu-id="b8732-143">toocreate hello second subnet, enter **myVnet** in hello **Search resources** box at hello top of hello page.</span></span> <span data-ttu-id="b8732-144">按一下**myVnet** hello 搜尋結果中出現。</span><span class="sxs-lookup"><span data-stu-id="b8732-144">Click **myVnet** when it appears in hello search results.</span></span>
5. <span data-ttu-id="b8732-145">按一下**子網路**(在 hello**設定**> 一節) 上 hello**建立虛擬網路 （傳統）**刀鋒視窗中出現。</span><span class="sxs-lookup"><span data-stu-id="b8732-145">Click **Subnets** (in hello **SETTINGS** section) on hello **Create virtual network (classic)** blade that appears.</span></span>
6. <span data-ttu-id="b8732-146">按一下**+ 加**上 hello **myVnet-子網路**刀鋒視窗中出現。</span><span class="sxs-lookup"><span data-stu-id="b8732-146">Click **+Add** on hello **myVnet - Subnets** blade that appears.</span></span>
7. <span data-ttu-id="b8732-147">輸入**私人**如**名稱**上 hello**加入子網路**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="b8732-147">Enter **Private** for **Name** on hello **Add subnet** blade.</span></span> <span data-ttu-id="b8732-148">在 [位址範圍] 輸入 **10.0.1.0/24**。</span><span class="sxs-lookup"><span data-stu-id="b8732-148">Enter **10.0.1.0/24** for **Address range**.</span></span>  <span data-ttu-id="b8732-149">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="b8732-149">Click **OK**.</span></span>
8. <span data-ttu-id="b8732-150">在 hello **myVnet-子網路**刀鋒視窗中，您可以看到 hello**公用**和**私人**您所建立的子網路。</span><span class="sxs-lookup"><span data-stu-id="b8732-150">On hello **myVnet - Subnets** blade, you can see hello **Public** and **Private** subnets that you created.</span></span>
9. <span data-ttu-id="b8732-151">**選擇性**： 當您完成本教學課程時，您可能想 toodelete hello 資源，您所建立，讓您不必承受使用費用：</span><span class="sxs-lookup"><span data-stu-id="b8732-151">**Optional**: When you finish this tutorial, you might want toodelete hello resources that you created, so that you don't incur usage charges:</span></span>
    - <span data-ttu-id="b8732-152">按一下**概觀**上 hello **myVnet**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="b8732-152">Click **Overview** on hello **myVnet** blade.</span></span>
    - <span data-ttu-id="b8732-153">按一下 hello**刪除**圖示 hello **myVnet**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="b8732-153">Click hello **Delete** icon on hello **myVnet** blade.</span></span>
    - <span data-ttu-id="b8732-154">tooconfirm hello 刪除、 按一下**是**在 hello**刪除虛擬網路**方塊。</span><span class="sxs-lookup"><span data-stu-id="b8732-154">tooconfirm hello deletion, click **Yes** in hello **Delete virtual network** box.</span></span>

## <a name="azure-cli"></a><span data-ttu-id="b8732-155">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="b8732-155">Azure CLI</span></span>

1. <span data-ttu-id="b8732-156">您可以[安裝及設定 hello Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json)，或使用 hello CLI hello Azure 雲端殼層內。</span><span class="sxs-lookup"><span data-stu-id="b8732-156">You can either [install and configure hello Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json), or use hello CLI within hello Azure Cloud Shell.</span></span> <span data-ttu-id="b8732-157">hello Azure 雲端殼層是免費的 Bash 殼層，您可以直接在 hello Azure 入口網站中執行。</span><span class="sxs-lookup"><span data-stu-id="b8732-157">hello Azure Cloud Shell is a free Bash shell that you can run directly within hello Azure portal.</span></span> <span data-ttu-id="b8732-158">它有的 hello Azure CLI 預先安裝和設定 toouse 與您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="b8732-158">It has hello Azure CLI preinstalled and configured toouse with your account.</span></span> <span data-ttu-id="b8732-159">CLI 命令的 tooget 說明輸入`azure <command> --help`。</span><span class="sxs-lookup"><span data-stu-id="b8732-159">tooget help for CLI commands, type `azure <command> --help`.</span></span> 
2. <span data-ttu-id="b8732-160">CLI 工作階段中，登入 tooAzure hello 命令所示。</span><span class="sxs-lookup"><span data-stu-id="b8732-160">In a CLI session, log in tooAzure with hello command that follows.</span></span> <span data-ttu-id="b8732-161">如果您按一下**試試**hello 方塊下方，在雲端殼層會開啟。</span><span class="sxs-lookup"><span data-stu-id="b8732-161">If you click **Try it** in hello box below, a Cloud Shell opens.</span></span> <span data-ttu-id="b8732-162">您可以登入 tooyour Azure 訂用帳戶，而不需輸入 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="b8732-162">You can log in tooyour Azure subscription, without entering hello following command:</span></span>

    ```azurecli-interactive
    azure login
    ```

3. <span data-ttu-id="b8732-163">tooensure hello CLI 可在服務管理模式中，輸入下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="b8732-163">tooensure hello CLI is in Service Management mode, enter hello following command:</span></span>

    ```azurecli-interactive
    azure config mode asm
    ```

4. <span data-ttu-id="b8732-164">建立具有私人子網路的虛擬網路：</span><span class="sxs-lookup"><span data-stu-id="b8732-164">Create a virtual network with a private subnet:</span></span>

    ```azurecli-interactive
    azure network vnet create --vnet myVnet --address-space 10.0.0.0 --cidr 16  --subnet-name Private --subnet-start-ip 10.0.0.0 --subnet-cidr 24 --location "East US"
    ```

5. <span data-ttu-id="b8732-165">建立 hello 虛擬網路內的公用子網路：</span><span class="sxs-lookup"><span data-stu-id="b8732-165">Create a public subnet within hello virtual network:</span></span>

    ```azurecli-interactive
    azure network vnet subnet create --name Public --vnet-name myVnet --address-prefix 10.0.1.0/24
    ```    
    
6. <span data-ttu-id="b8732-166">檢閱 hello 虛擬網路和子網路：</span><span class="sxs-lookup"><span data-stu-id="b8732-166">Review hello virtual network and subnets:</span></span>

    ```azurecli-interactive
    azure network vnet show --vnet myVnet
    ```

7. <span data-ttu-id="b8732-167">**選擇性**： 您可以建立當您完成本教學課程，讓您不必承受使用費 toodelete hello 資源：</span><span class="sxs-lookup"><span data-stu-id="b8732-167">**Optional**: You might want toodelete hello resources that you created when you finish this tutorial, so that you don't incur usage charges:</span></span>

    ```azurecli-interactive
    azure network vnet delete --vnet myVnet --quiet
    ```

> [!NOTE]
> <span data-ttu-id="b8732-168">雖然您無法指定資源群組 toocreate （傳統） 的虛擬網路中使用 hello CLI，Azure 會建立名為的資源群組的 hello 虛擬網路*預設網路*。</span><span class="sxs-lookup"><span data-stu-id="b8732-168">Though you can't specify a resource group toocreate a virtual network (classic) in using hello CLI, Azure creates hello virtual network in a resource group named *Default-Networking*.</span></span>

## <a name="powershell"></a><span data-ttu-id="b8732-169">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b8732-169">PowerShell</span></span>

1. <span data-ttu-id="b8732-170">安裝 hello hello PowerShell 最新版本[Azure](https://www.powershellgallery.com/packages/Azure)模組。</span><span class="sxs-lookup"><span data-stu-id="b8732-170">Install hello latest version of hello PowerShell [Azure](https://www.powershellgallery.com/packages/Azure) module.</span></span> <span data-ttu-id="b8732-171">如果您是新 tooAzure PowerShell，請參閱[Azure PowerShell 概觀](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="b8732-171">If you're new tooAzure PowerShell, see [Azure PowerShell overview](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
2. <span data-ttu-id="b8732-172">啟動 PowerShell 工作階段。</span><span class="sxs-lookup"><span data-stu-id="b8732-172">Start a PowerShell session.</span></span>
3. <span data-ttu-id="b8732-173">在 PowerShell 中，登入 tooAzure 輸入 hello`Add-AzureAccount`命令。</span><span class="sxs-lookup"><span data-stu-id="b8732-173">In PowerShell, log in tooAzure by entering hello `Add-AzureAccount` command.</span></span>
4. <span data-ttu-id="b8732-174">變更 hello 以下路徑和檔案名稱，視需要再匯出您現有的網路組態檔：</span><span class="sxs-lookup"><span data-stu-id="b8732-174">Change hello following path and filename, as appropriate, then export your existing network configuration file:</span></span>

    ```powershell
    Get-AzureVNetConfig -ExportToFile c:\azure\NetworkConfig.xml
    ```

5. <span data-ttu-id="b8732-175">toocreate 具有公用和私用子網路的虛擬網路使用任何文字編輯器 tooadd hello **VirtualNetworkSite**後面 toohello 網路組態檔項目。</span><span class="sxs-lookup"><span data-stu-id="b8732-175">toocreate a virtual network with public and private subnets, use any text editor tooadd hello **VirtualNetworkSite** element that follows toohello network configuration file.</span></span>

    ```xml
    <VirtualNetworkSite name="myVnet" Location="East US">
        <AddressSpace>
          <AddressPrefix>10.0.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="Private">
            <AddressPrefix>10.0.0.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Public">
            <AddressPrefix>10.0.1.0/24</AddressPrefix>
          </Subnet>
        </Subnets>
      </VirtualNetworkSite>
    ```

    <span data-ttu-id="b8732-176">完整檢閱 hello[網路組態檔結構描述](https://msdn.microsoft.com/library/azure/jj157100.aspx)。</span><span class="sxs-lookup"><span data-stu-id="b8732-176">Review hello full [network configuration file schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>

6. <span data-ttu-id="b8732-177">匯入 hello 網路組態檔：</span><span class="sxs-lookup"><span data-stu-id="b8732-177">Import hello network configuration file:</span></span>

    ```powershell
    Set-AzureVNetConfig -ConfigurationPath c:\azure\NetworkConfig.xml
    ```

    > [!WARNING]
    > <span data-ttu-id="b8732-178">匯入已變更的網路組態檔，可能會導致變更 tooexisting （傳統） 您的訂用帳戶中的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="b8732-178">Importing a changed network configuration file can cause changes tooexisting virtual networks (classic) in your subscription.</span></span> <span data-ttu-id="b8732-179">確定您只有新增 hello 的上一個虛擬網路，且您不變更或移除任何現有的虛擬網路從您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="b8732-179">Ensure you only add hello previous virtual network and that you don't change or remove any existing virtual networks from your subscription.</span></span> 

7. <span data-ttu-id="b8732-180">檢閱 hello 虛擬網路和子網路：</span><span class="sxs-lookup"><span data-stu-id="b8732-180">Review hello virtual network and subnets:</span></span>

    ```powershell
    Get-AzureVNetSite -VNetName "myVnet"
    ```

8. <span data-ttu-id="b8732-181">**選擇性**： 您可能會想 toodelete hello 資源時所建立完成此教學課程中，如此您就不會產生使用費用。</span><span class="sxs-lookup"><span data-stu-id="b8732-181">**Optional**: You might want toodelete hello resources that you created when you finish this tutorial, so that you don't incur usage charges.</span></span> <span data-ttu-id="b8732-182">toodelete hello 虛擬網路，完成步驟 4-6 同樣地，此時間移除 hello **VirtualNetworkSite**步驟 5 中所加入的項目。</span><span class="sxs-lookup"><span data-stu-id="b8732-182">toodelete hello virtual network, complete steps 4-6 again, this time removing hello **VirtualNetworkSite** element you added in step 5.</span></span>
 
> [!NOTE]
> <span data-ttu-id="b8732-183">雖然您無法在 PowerShell 中使用指定的資源群組 toocreate （傳統） 的虛擬網路，Azure 會建立名為的資源群組的 hello 虛擬網路*預設網路*。</span><span class="sxs-lookup"><span data-stu-id="b8732-183">Though you can't specify a resource group toocreate a virtual network (classic) in using PowerShell, Azure creates hello virtual network in a resource group named *Default-Networking*.</span></span>

---

## <a name="next-steps"></a><span data-ttu-id="b8732-184">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b8732-184">Next steps</span></span>

- <span data-ttu-id="b8732-185">toolearn 有關所有虛擬網路和子網路設定，請參閱[管理虛擬網路](virtual-network-manage-network.md)和[管理虛擬網路子網路](virtual-network-manage-subnet.md)。</span><span class="sxs-lookup"><span data-stu-id="b8732-185">toolearn about all virtual network and subnet settings, see [Manage virtual networks](virtual-network-manage-network.md) and [Manage virtual network subnets](virtual-network-manage-subnet.md).</span></span> <span data-ttu-id="b8732-186">您必須使用實際執行環境 toomeet 不同需求中的虛擬網路和子網路的各種選項。</span><span class="sxs-lookup"><span data-stu-id="b8732-186">You have various options for using virtual networks and subnets in a production environment toomeet different requirements.</span></span>
- <span data-ttu-id="b8732-187">輸入和輸出 toofilter 子網路的流量，建立和套用[網路安全性群組](virtual-networks-nsg.md)toosubnets。</span><span class="sxs-lookup"><span data-stu-id="b8732-187">toofilter inbound and outbound subnet traffic, create and apply [network security groups](virtual-networks-nsg.md) toosubnets.</span></span>
- <span data-ttu-id="b8732-188">建立[Windows](../virtual-machines/windows/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json)或[Linux](../virtual-machines/linux/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json)虛擬機器，然後將它連線 tooan 現有的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="b8732-188">Create a [Windows](../virtual-machines/windows/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) or a [Linux](../virtual-machines/linux/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) virtual machine, and then connect it tooan existing virtual network.</span></span>
- <span data-ttu-id="b8732-189">tooconnect 兩個虛擬網路在 hello 相同的 Azure 位置中建立[虛擬網路對等互連](create-peering-different-deployment-models.md)hello 虛擬網路之間。</span><span class="sxs-lookup"><span data-stu-id="b8732-189">tooconnect two virtual networks in hello same Azure location, create a  [virtual network peering](create-peering-different-deployment-models.md) between hello virtual networks.</span></span> <span data-ttu-id="b8732-190">您可以對等虛擬網路 （資源管理員） tooa 虛擬網路 （傳統），但您無法建立對等互連介於兩個虛擬網路 （傳統）。</span><span class="sxs-lookup"><span data-stu-id="b8732-190">You can peer a virtual network (Resource Manager) tooa virtual network (classic), but you cannot create a peering between two virtual networks (classic).</span></span>
- <span data-ttu-id="b8732-191">使用 hello 虛擬網路 tooan 在內部部署網路連線[VPN 閘道](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json)或[Azure ExpressRoute](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md?toc=%2fazure%2fvirtual-network%2ftoc.json)循環。</span><span class="sxs-lookup"><span data-stu-id="b8732-191">Connect hello virtual network tooan on-premises network by using a [VPN Gateway](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) or [Azure ExpressRoute](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md?toc=%2fazure%2fvirtual-network%2ftoc.json) circuit.</span></span>
