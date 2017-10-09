---
title: "aaaCreate 和管理 Windows Azure 中的 Vm 使用多個 Nic |Microsoft 文件"
description: "深入了解如何 toocreate 和管理使用 Azure PowerShell 或資源管理員範本中有多個 Nic 附加的 tooit Windows VM。"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 9bff5b6d-79ac-476b-a68f-6f8754768413
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/05/2017
ms.author: iainfou
ms.openlocfilehash: c3c7d7569aca6f047238146d84b2ffccf05d4079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-a-windows-virtual-machine-that-has-multiple-nics"></a><span data-ttu-id="1b59b-103">建立及管理具有多個 NIC 的 Windows 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="1b59b-103">Create and manage a Windows virtual machine that has multiple NICs</span></span>
<span data-ttu-id="1b59b-104">在 Azure 中的虛擬機器 (Vm) 可以有多個虛擬網路介面卡 (Nic) 附加 toothem。</span><span class="sxs-lookup"><span data-stu-id="1b59b-104">Virtual machines (VMs) in Azure can have multiple virtual network interface cards (NICs) attached toothem.</span></span> <span data-ttu-id="1b59b-105">常見的案例是 toohave 前端和後端連線的不同子網路或網路專用 tooa 監視或備份解決方案。</span><span class="sxs-lookup"><span data-stu-id="1b59b-105">A common scenario is toohave different subnets for front-end and back-end connectivity, or a network dedicated tooa monitoring or backup solution.</span></span> <span data-ttu-id="1b59b-106">這篇文章說明如何將 toocreate 具有多個 Nic VM 附加 tooit。</span><span class="sxs-lookup"><span data-stu-id="1b59b-106">This article details how toocreate a VM that has multiple NICs attached tooit.</span></span> <span data-ttu-id="1b59b-107">您也了解如何從現有的 VM tooadd 或移除 Nic。</span><span class="sxs-lookup"><span data-stu-id="1b59b-107">You also learn how tooadd or remove NICs from an existing VM.</span></span> <span data-ttu-id="1b59b-108">不同的 [VM 大小](sizes.md) 支援不同數量的 NIC，因此可據以調整您的 VM。</span><span class="sxs-lookup"><span data-stu-id="1b59b-108">Different [VM sizes](sizes.md) support a varying number of NICs, so size your VM accordingly.</span></span>

<span data-ttu-id="1b59b-109">如需詳細資訊，包括如何 toocreate 多個 Nic 內您自己的 PowerShell 指令碼，請參閱[部署多個 NIC Vm](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="1b59b-109">For detailed information, including how toocreate multiple NICs within your own PowerShell scripts, see [deploying multiple-NIC VMs](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1b59b-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="1b59b-110">Prerequisites</span></span>
<span data-ttu-id="1b59b-111">請確定您擁有 hello[最新的 Azure PowerShell 版本安裝並設定](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="1b59b-111">Make sure that you have hello [latest Azure PowerShell version installed and configured](/powershell/azure/overview).</span></span>

<span data-ttu-id="1b59b-112">在 hello 下列範例中，會取代您自己的值的範例參數名稱。</span><span class="sxs-lookup"><span data-stu-id="1b59b-112">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="1b59b-113">範例參數名稱包含 *myResourceGroup*、*myVnet* 和 *myVM*。</span><span class="sxs-lookup"><span data-stu-id="1b59b-113">Example parameter names include *myResourceGroup*, *myVnet*, and *myVM*.</span></span>


## <a name="create-a-vm-with-multiple-nics"></a><span data-ttu-id="1b59b-114">建立具有多個 NIC 的 VM</span><span class="sxs-lookup"><span data-stu-id="1b59b-114">Create a VM with multiple NICs</span></span>
<span data-ttu-id="1b59b-115">首先，建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="1b59b-115">First, create a resource group.</span></span> <span data-ttu-id="1b59b-116">hello 下列範例會建立名為的資源群組*myResourceGroup*在 hello *EastUs*位置：</span><span class="sxs-lookup"><span data-stu-id="1b59b-116">hello following example creates a resource group named *myResourceGroup* in hello *EastUs* location:</span></span>

```powershell
New-AzureRmResourceGroup -Name "myResourceGroup" -Location "EastUS"
```

### <a name="create-virtual-network-and-subnets"></a><span data-ttu-id="1b59b-117">建立虛擬網路和子網路</span><span class="sxs-lookup"><span data-stu-id="1b59b-117">Create virtual network and subnets</span></span>
<span data-ttu-id="1b59b-118">常見的案例是針對虛擬網路 toohave 兩個或多個子網路。</span><span class="sxs-lookup"><span data-stu-id="1b59b-118">A common scenario is for a virtual network toohave two or more subnets.</span></span> <span data-ttu-id="1b59b-119">前端的流量，hello 其他後端流量可能會成為一個子網路。</span><span class="sxs-lookup"><span data-stu-id="1b59b-119">One subnet may be for front-end traffic, hello other for back-end traffic.</span></span> <span data-ttu-id="1b59b-120">tooconnect tooboth 子網路，然後您使用多個 Nic VM 上。</span><span class="sxs-lookup"><span data-stu-id="1b59b-120">tooconnect tooboth subnets, you then use multiple NICs on your VM.</span></span>

1. <span data-ttu-id="1b59b-121">使用 [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) 定義兩個虛擬網路子網路。</span><span class="sxs-lookup"><span data-stu-id="1b59b-121">Define two virtual network subnets with [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span></span> <span data-ttu-id="1b59b-122">hello 下列範例會定義 hello 子網路的*mySubnetFrontEnd*和*mySubnetBackEnd*:</span><span class="sxs-lookup"><span data-stu-id="1b59b-122">hello following example defines hello subnets for *mySubnetFrontEnd* and *mySubnetBackEnd*:</span></span>

    ```powershell
    $mySubnetFrontEnd = New-AzureRmVirtualNetworkSubnetConfig -Name "mySubnetFrontEnd" `
        -AddressPrefix "192.168.1.0/24"
    $mySubnetBackEnd = New-AzureRmVirtualNetworkSubnetConfig -Name "mySubnetBackEnd" `
        -AddressPrefix "192.168.2.0/24"
    ```

2. <span data-ttu-id="1b59b-123">使用 [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) 建立虛擬網路和子網路。</span><span class="sxs-lookup"><span data-stu-id="1b59b-123">Create your virtual network and subnets with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span></span> <span data-ttu-id="1b59b-124">hello 下列範例會建立虛擬網路，名為*myVnet*:</span><span class="sxs-lookup"><span data-stu-id="1b59b-124">hello following example creates a virtual network named *myVnet*:</span></span>

    ```powershell
    $myVnet = New-AzureRmVirtualNetwork -ResourceGroupName "myResourceGroup" `
        -Location "EastUs" `
        -Name "myVnet" `
        -AddressPrefix "192.168.0.0/16" `
        -Subnet $mySubnetFrontEnd,$mySubnetBackEnd
    ```


### <a name="create-multiple-nics"></a><span data-ttu-id="1b59b-125">建立多個 NIC</span><span class="sxs-lookup"><span data-stu-id="1b59b-125">Create multiple NICs</span></span>
<span data-ttu-id="1b59b-126">使用 [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) 建立兩個 NIC。</span><span class="sxs-lookup"><span data-stu-id="1b59b-126">Create two NICs with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span></span> <span data-ttu-id="1b59b-127">附加一個 NIC toohello 前端子網路和一個 NIC toohello 後端子。</span><span class="sxs-lookup"><span data-stu-id="1b59b-127">Attach one NIC toohello front-end subnet and one NIC toohello back-end subnet.</span></span> <span data-ttu-id="1b59b-128">hello 下列範例會建立名為的 Nic *myNic1*和*myNic2*:</span><span class="sxs-lookup"><span data-stu-id="1b59b-128">hello following example creates NICs named *myNic1* and *myNic2*:</span></span>

```powershell
$frontEnd = $myVnet.Subnets|?{$_.Name -eq 'mySubnetFrontEnd'}
$myNic1 = New-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" `
    -Name "myNic1" `
    -Location "EastUs" `
    -SubnetId $frontEnd.Id

$backEnd = $myVnet.Subnets|?{$_.Name -eq 'mySubnetBackEnd'}
$myNic2 = New-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" `
    -Name "myNic2" `
    -Location "EastUs" `
    -SubnetId $backEnd.Id
```

<span data-ttu-id="1b59b-129">通常您也會建立[網路安全性群組](../../virtual-network/virtual-networks-nsg.md)或[負載平衡器](../../load-balancer/load-balancer-overview.md)toohelp 管理，以及將流量分散到您的 Vm。</span><span class="sxs-lookup"><span data-stu-id="1b59b-129">Typically you also create a [network security group](../../virtual-network/virtual-networks-nsg.md) or [load balancer](../../load-balancer/load-balancer-overview.md) toohelp manage and distribute traffic across your VMs.</span></span> <span data-ttu-id="1b59b-130">hello[更詳細的多個 NIC VM](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md)文章將逐步引導您完成建立網路安全性群組並指派 Nic。</span><span class="sxs-lookup"><span data-stu-id="1b59b-130">hello [more detailed multiple-NIC VM](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md) article guides you through creating a network security group and assigning NICs.</span></span>

### <a name="create-hello-virtual-machine"></a><span data-ttu-id="1b59b-131">建立 hello 的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="1b59b-131">Create hello virtual machine</span></span>
<span data-ttu-id="1b59b-132">現在開始 toobuild VM 組態。</span><span class="sxs-lookup"><span data-stu-id="1b59b-132">Now start toobuild your VM configuration.</span></span> <span data-ttu-id="1b59b-133">每個 VM 的大小，您可以加入 tooa VM 之 Nic 的 hello 總數的上限。</span><span class="sxs-lookup"><span data-stu-id="1b59b-133">Each VM size has a limit for hello total number of NICs that you can add tooa VM.</span></span> <span data-ttu-id="1b59b-134">如需詳細資訊，請參閱 [Windows VM 大小](sizes.md)。</span><span class="sxs-lookup"><span data-stu-id="1b59b-134">For more information, see [Windows VM sizes](sizes.md).</span></span>

1. <span data-ttu-id="1b59b-135">設定您的 VM 認證 toohello`$cred`變數，如下所示：</span><span class="sxs-lookup"><span data-stu-id="1b59b-135">Set your VM credentials toohello `$cred` variable as follows:</span></span>

    ```powershell
    $cred = Get-Credential
    ```

2. <span data-ttu-id="1b59b-136">使用 [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) 來定義您的 VM。</span><span class="sxs-lookup"><span data-stu-id="1b59b-136">Define your VM with [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig).</span></span> <span data-ttu-id="1b59b-137">hello 下列範例會定義名為的 VM *myVM* ，並使用支援超過兩個 Nic VM 大小 (*Standard_DS3_v2*):</span><span class="sxs-lookup"><span data-stu-id="1b59b-137">hello following example defines a VM named *myVM* and uses a VM size that supports more than two NICs (*Standard_DS3_v2*):</span></span>

    ```powershell
    $vmConfig = New-AzureRmVMConfig -VMName "myVM" -VMSize "Standard_DS3_v2"
    ```

3. <span data-ttu-id="1b59b-138">建立 VM 組態的 hello rest[組 AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem)和[組 AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage)。</span><span class="sxs-lookup"><span data-stu-id="1b59b-138">Create hello rest of your VM configuration with [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) and [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage).</span></span> <span data-ttu-id="1b59b-139">hello 下列範例會建立 Windows Server 2016 VM:</span><span class="sxs-lookup"><span data-stu-id="1b59b-139">hello following example creates a Windows Server 2016 VM:</span></span>

    ```powershell
    $vmConfig = Set-AzureRmVMOperatingSystem -VM $vmConfig `
        -Windows `
        -ComputerName "myVM" `
        -Credential $cred `
        -ProvisionVMAgent `
        -EnableAutoUpdate
    $vmConfig = Set-AzureRmVMSourceImage -VM $vmConfig `
        -PublisherName "MicrosoftWindowsServer" `
        -Offer "WindowsServer" `
        -Skus "2016-Datacenter" `
        -Version "latest"
   ```

4. <span data-ttu-id="1b59b-140">附加您先前建立的 hello 兩個 Nic[新增 AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="1b59b-140">Attach hello two NICs that you previously created with [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span></span>

    ```powershell
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $myNic1.Id -Primary
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $myNic2.Id
    ```

5. <span data-ttu-id="1b59b-141">最後，使用 [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) 建立 VM：</span><span class="sxs-lookup"><span data-stu-id="1b59b-141">Finally, create your VM with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm):</span></span>

    ```powershell
    New-AzureRmVM -VM $vmConfig -ResourceGroupName "myResourceGroup" -Location "EastUs"
    ```

## <a name="add-a-nic-tooan-existing-vm"></a><span data-ttu-id="1b59b-142">加入現有的 VM NIC tooan</span><span class="sxs-lookup"><span data-stu-id="1b59b-142">Add a NIC tooan existing VM</span></span>
<span data-ttu-id="1b59b-143">加入現有的 VM 虛擬 NIC tooan，deallocate hello VM，tooadd hello 虛擬 NIC，然後啟動 hello VM。</span><span class="sxs-lookup"><span data-stu-id="1b59b-143">tooadd a virtual NIC tooan existing VM, you deallocate hello VM, add hello virtual NIC, then start hello VM.</span></span>

1. <span data-ttu-id="1b59b-144">解除配置 hello 與 VM[停止 AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm)。</span><span class="sxs-lookup"><span data-stu-id="1b59b-144">Deallocate hello VM with [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span></span> <span data-ttu-id="1b59b-145">hello 下列範例會取消配置 hello 名為 VM *myVM*中*myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="1b59b-145">hello following example deallocates hello VM named *myVM* in *myResourceGroup*:</span></span>

    ```powershell
    Stop-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

2. <span data-ttu-id="1b59b-146">取得 hello hello VM 之現有的組態與[Get AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm)。</span><span class="sxs-lookup"><span data-stu-id="1b59b-146">Get hello existing configuration of hello VM with [Get-AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm).</span></span> <span data-ttu-id="1b59b-147">hello 下列範例會取得名為 VM hello 資訊*myVM*中*myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="1b59b-147">hello following example gets information for hello VM named *myVM* in *myResourceGroup*:</span></span>

    ```powershell
    $vm = Get-AzureRmVm -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

3. <span data-ttu-id="1b59b-148">hello 下列範例會建立虛擬 NIC 與[新增 AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface)名為*myNic3*太附加*mySubnetBackEnd*。</span><span class="sxs-lookup"><span data-stu-id="1b59b-148">hello following example creates a virtual NIC with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) named *myNic3* that is attached too*mySubnetBackEnd*.</span></span> <span data-ttu-id="1b59b-149">hello 虛擬 NIC，就會附加 toohello 名為 VM *myVM*中*myResourceGroup*與[新增 AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="1b59b-149">hello virtual NIC is then attached toohello VM named *myVM* in *myResourceGroup* with [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span></span>

    ```powershell
    # Get info for hello back end subnet
    $myVnet = Get-AzureRmVirtualNetwork -Name "myVnet" -ResourceGroupName "myResourceGroup"
    $backEnd = $myVnet.Subnets|?{$_.Name -eq 'mySubnetBackEnd'}

    # Create a virtual NIC
    $myNic3 = New-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" `
        -Name "myNic3" `
        -Location "EastUs" `
        -SubnetId $backEnd.Id

    # Get hello ID of hello new virtual NIC and add tooVM
    $nicId = (Get-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" -Name "MyNic3").Id
    Add-AzureRmVMNetworkInterface -VM $vm -Id $nicId | Update-AzureRmVm -ResourceGroupName "myResourceGroup"
    ```

    ### <a name="primary-virtual-nics"></a><span data-ttu-id="1b59b-150">主要虛擬 NIC</span><span class="sxs-lookup"><span data-stu-id="1b59b-150">Primary virtual NICs</span></span>
    <span data-ttu-id="1b59b-151">其中一個 hello Nic 上的多個 NIC VM 需要 toobe 主要。</span><span class="sxs-lookup"><span data-stu-id="1b59b-151">One of hello NICs on a multi-NIC VM needs toobe primary.</span></span> <span data-ttu-id="1b59b-152">如果其中一個 hello 現有的虛擬 Nic 上 hello VM 已設定為主要，則可以略過此步驟。</span><span class="sxs-lookup"><span data-stu-id="1b59b-152">If one of hello existing virtual NICs on hello VM is already set as primary, you can skip this step.</span></span> <span data-ttu-id="1b59b-153">hello 下列範例假設兩個虛擬 Nic 現在會出現在 VM 上，且您想 tooadd hello 第一個 NIC (`[0]`) 做為主要的 hello:</span><span class="sxs-lookup"><span data-stu-id="1b59b-153">hello following example assumes that two virtual NICs are now present on a VM and you wish tooadd hello first NIC (`[0]`) as hello primary:</span></span>
        
    ```powershell
    # List existing NICs on hello VM and find which one is primary
    $vm.NetworkProfile.NetworkInterfaces
    
    # Set NIC 0 toobe primary
    $vm.NetworkProfile.NetworkInterfaces[0].Primary = $true
    $vm.NetworkProfile.NetworkInterfaces[1].Primary = $false
    
    # Update hello VM state in Azure
    Update-AzureRmVM -VM $vm -ResourceGroupName "myResourceGroup"
    ```

4. <span data-ttu-id="1b59b-154">啟動 hello 與 VM[開始 AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm):</span><span class="sxs-lookup"><span data-stu-id="1b59b-154">Start hello VM with [Start-AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm):</span></span>

    ```powershell
    Start-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
    ```

## <a name="remove-a-nic-from-an-existing-vm"></a><span data-ttu-id="1b59b-155">從現有的 VM 移除 NIC</span><span class="sxs-lookup"><span data-stu-id="1b59b-155">Remove a NIC from an existing VM</span></span>
<span data-ttu-id="1b59b-156">tooremove 虛擬 NIC 從現有的 VM 解除配置 hello VM、 移除 hello 虛擬 NIC，然後開始 hello VM。</span><span class="sxs-lookup"><span data-stu-id="1b59b-156">tooremove a virtual NIC from an existing VM, you deallocate hello VM, remove hello virtual NIC, then start hello VM.</span></span>

1. <span data-ttu-id="1b59b-157">解除配置 hello 與 VM[停止 AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm)。</span><span class="sxs-lookup"><span data-stu-id="1b59b-157">Deallocate hello VM with [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span></span> <span data-ttu-id="1b59b-158">hello 下列範例會取消配置 hello 名為 VM *myVM*中*myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="1b59b-158">hello following example deallocates hello VM named *myVM* in *myResourceGroup*:</span></span>

    ```powershell
    Stop-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

2. <span data-ttu-id="1b59b-159">取得 hello hello VM 之現有的組態與[Get AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm)。</span><span class="sxs-lookup"><span data-stu-id="1b59b-159">Get hello existing configuration of hello VM with [Get-AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm).</span></span> <span data-ttu-id="1b59b-160">hello 下列範例會取得名為 VM hello 資訊*myVM*中*myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="1b59b-160">hello following example gets information for hello VM named *myVM* in *myResourceGroup*:</span></span>

    ```powershell
    $vm = Get-AzureRmVm -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

3. <span data-ttu-id="1b59b-161">取得資訊 hello 與移除 NIC [Get AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface)。</span><span class="sxs-lookup"><span data-stu-id="1b59b-161">Get information about hello NIC remove with [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface).</span></span> <span data-ttu-id="1b59b-162">hello 下列範例會取得資訊的相關*myNic3*:</span><span class="sxs-lookup"><span data-stu-id="1b59b-162">hello following example gets information about *myNic3*:</span></span>

    ```powershell
    # List existing NICs on hello VM if you need toodetermine NIC name
    $vm.NetworkProfile.NetworkInterfaces

    $nicId = (Get-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" -Name "myNic3").Id   
    ```

4. <span data-ttu-id="1b59b-163">移除 hello 與 NIC[移除 AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/remove-azurermvmnetworkinterface)然後更新 hello 與 VM[更新 AzureRmVm](/powershell/module/azurerm.compute/update-azurermvm)。</span><span class="sxs-lookup"><span data-stu-id="1b59b-163">Remove hello NIC with [Remove-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/remove-azurermvmnetworkinterface) and then update hello VM with [Update-AzureRmVm](/powershell/module/azurerm.compute/update-azurermvm).</span></span> <span data-ttu-id="1b59b-164">hello 下列範例會移除*myNic3*取得的`$nicId`hello 前面步驟中：</span><span class="sxs-lookup"><span data-stu-id="1b59b-164">hello following example removes *myNic3* as obtained by `$nicId` in hello preceding step:</span></span>

    ```powershell
    Remove-AzureRmVMNetworkInterface -VM $vm -NetworkInterfaceIDs $nicId | `
        Update-AzureRmVm -ResourceGroupName "myResourceGroup"
    ```   

5. <span data-ttu-id="1b59b-165">啟動 hello 與 VM[開始 AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm):</span><span class="sxs-lookup"><span data-stu-id="1b59b-165">Start hello VM with [Start-AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm):</span></span>

    ```powershell
    Start-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```   

## <a name="create-multiple-nics-with-templates"></a><span data-ttu-id="1b59b-166">使用範本建立多個 NIC</span><span class="sxs-lookup"><span data-stu-id="1b59b-166">Create multiple NICs with templates</span></span>
<span data-ttu-id="1b59b-167">Azure 資源管理員範本提供方式 toocreate 資源的多個執行個體在部署期間，例如建立多個 Nic。</span><span class="sxs-lookup"><span data-stu-id="1b59b-167">Azure Resource Manager templates provide a way toocreate multiple instances of a resource during deployment, such as creating multiple NICs.</span></span> <span data-ttu-id="1b59b-168">資源管理員範本使用宣告式的 JSON 檔案 toodefine 環境。</span><span class="sxs-lookup"><span data-stu-id="1b59b-168">Resource Manager templates use declarative JSON files toodefine your environment.</span></span> <span data-ttu-id="1b59b-169">如需詳細資訊，請參閱 [Azure Resource Manager 概觀](../../azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="1b59b-169">For more information, see [overview of Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="1b59b-170">您可以使用*複製*執行個體 toocreate toospecify hello 數目：</span><span class="sxs-lookup"><span data-stu-id="1b59b-170">You can use *copy* toospecify hello number of instances toocreate:</span></span>

```json
"copy": {
    "name": "multiplenics",
    "count": "[parameters('count')]"
}
```

<span data-ttu-id="1b59b-171">如需詳細資訊，請參閱[使用 copy 建立多個執行個體](../../resource-group-create-multiple.md)。</span><span class="sxs-lookup"><span data-stu-id="1b59b-171">For more information, see [creating multiple instances by using *copy*](../../resource-group-create-multiple.md).</span></span> 

<span data-ttu-id="1b59b-172">您也可以使用`copyIndex()`tooappend 數字的 tooa 資源名稱。</span><span class="sxs-lookup"><span data-stu-id="1b59b-172">You can also use `copyIndex()` tooappend a number tooa resource name.</span></span> <span data-ttu-id="1b59b-173">接著可以建立 myNic1、MyNic2 等等。</span><span class="sxs-lookup"><span data-stu-id="1b59b-173">You can then create *myNic1*, *MyNic2* and so on.</span></span> <span data-ttu-id="1b59b-174">hello 下列程式碼顯示附加 hello 索引值的範例：</span><span class="sxs-lookup"><span data-stu-id="1b59b-174">hello following code shows an example of appending hello index value:</span></span>

```json
"name": "[concat('myNic', copyIndex())]", 
```

<span data-ttu-id="1b59b-175">您可以閱讀[使用 Resource Manager 範本建立多個 NIC](../../virtual-network/virtual-network-deploy-multinic-arm-template.md)的完整範例。</span><span class="sxs-lookup"><span data-stu-id="1b59b-175">You can read a complete example of [creating multiple NICs by using Resource Manager templates](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1b59b-176">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1b59b-176">Next steps</span></span>
<span data-ttu-id="1b59b-177">檢閱[Windows VM 大小](sizes.md)當您嘗試 toocreate 具有多個 Nic VM。</span><span class="sxs-lookup"><span data-stu-id="1b59b-177">Review [Windows VM sizes](sizes.md) when you're trying toocreate a VM that has multiple NICs.</span></span> <span data-ttu-id="1b59b-178">請注意 toohello 最大數目的每個 VM 大小所支援的 Nic。</span><span class="sxs-lookup"><span data-stu-id="1b59b-178">Pay attention toohello maximum number of NICs that each VM size supports.</span></span> 


