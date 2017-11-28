---
title: "在 Azure 中建立和管理使用多個 NIC 的 Windows VM | Microsoft Docs"
description: "了解如何使用 Azure PowerShell 或 Resource Manager 範本，建立和管理連結多個 NIC 的 Windows VM。"
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
ms.openlocfilehash: 3bd99a67dae41de3533d7f6e244eb7ee3ecc4049
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-a-windows-virtual-machine-that-has-multiple-nics"></a><span data-ttu-id="ca45f-103">建立及管理具有多個 NIC 的 Windows 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="ca45f-103">Create and manage a Windows virtual machine that has multiple NICs</span></span>
<span data-ttu-id="ca45f-104">Azure 中的虛擬機器 (VM) 可以連結多個虛擬網路介面卡 (NIC)。</span><span class="sxs-lookup"><span data-stu-id="ca45f-104">Virtual machines (VMs) in Azure can have multiple virtual network interface cards (NICs) attached to them.</span></span> <span data-ttu-id="ca45f-105">常見案例是有不同的子網路可用於前端和後端連線，或者專門用來監視或備份解決方案的網路。</span><span class="sxs-lookup"><span data-stu-id="ca45f-105">A common scenario is to have different subnets for front-end and back-end connectivity, or a network dedicated to a monitoring or backup solution.</span></span> <span data-ttu-id="ca45f-106">本文詳述如何建立已連結多個 NIC 的 VM。</span><span class="sxs-lookup"><span data-stu-id="ca45f-106">This article details how to create a VM that has multiple NICs attached to it.</span></span> <span data-ttu-id="ca45f-107">您也了解如何新增或移除現有 VM 中的 NIC。</span><span class="sxs-lookup"><span data-stu-id="ca45f-107">You also learn how to add or remove NICs from an existing VM.</span></span> <span data-ttu-id="ca45f-108">不同的 [VM 大小](sizes.md) 支援不同數量的 NIC，因此可據以調整您的 VM。</span><span class="sxs-lookup"><span data-stu-id="ca45f-108">Different [VM sizes](sizes.md) support a varying number of NICs, so size your VM accordingly.</span></span>

<span data-ttu-id="ca45f-109">如需詳細資訊 (包括如何在自己的 PowerShell 指令碼內建立多個 NIC)，請參閱[部署多個 NIC 的 VM](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="ca45f-109">For detailed information, including how to create multiple NICs within your own PowerShell scripts, see [deploying multiple-NIC VMs](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ca45f-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="ca45f-110">Prerequisites</span></span>
<span data-ttu-id="ca45f-111">確定您已[安裝和設定最新的 Azure PowerShell 版本](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="ca45f-111">Make sure that you have the [latest Azure PowerShell version installed and configured](/powershell/azure/overview).</span></span>

<span data-ttu-id="ca45f-112">在下列範例中，請以您自己的值取代範例參數名稱。</span><span class="sxs-lookup"><span data-stu-id="ca45f-112">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="ca45f-113">範例參數名稱包含 *myResourceGroup*、*myVnet* 和 *myVM*。</span><span class="sxs-lookup"><span data-stu-id="ca45f-113">Example parameter names include *myResourceGroup*, *myVnet*, and *myVM*.</span></span>


## <a name="create-a-vm-with-multiple-nics"></a><span data-ttu-id="ca45f-114">建立具有多個 NIC 的 VM</span><span class="sxs-lookup"><span data-stu-id="ca45f-114">Create a VM with multiple NICs</span></span>
<span data-ttu-id="ca45f-115">首先，建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="ca45f-115">First, create a resource group.</span></span> <span data-ttu-id="ca45f-116">下列範例會在 EastUs 位置建立名為 myResourceGroup 的資源群組：</span><span class="sxs-lookup"><span data-stu-id="ca45f-116">The following example creates a resource group named *myResourceGroup* in the *EastUs* location:</span></span>

```powershell
New-AzureRmResourceGroup -Name "myResourceGroup" -Location "EastUS"
```

### <a name="create-virtual-network-and-subnets"></a><span data-ttu-id="ca45f-117">建立虛擬網路和子網路</span><span class="sxs-lookup"><span data-stu-id="ca45f-117">Create virtual network and subnets</span></span>
<span data-ttu-id="ca45f-118">常見的案例是有兩個或多個子網路的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="ca45f-118">A common scenario is for a virtual network to have two or more subnets.</span></span> <span data-ttu-id="ca45f-119">一個子網路可能用於前端流量，另一個則用於後端流量。</span><span class="sxs-lookup"><span data-stu-id="ca45f-119">One subnet may be for front-end traffic, the other for back-end traffic.</span></span> <span data-ttu-id="ca45f-120">若要連結至這兩個子網路，您可在 VM 上使用多個 NIC。</span><span class="sxs-lookup"><span data-stu-id="ca45f-120">To connect to both subnets, you then use multiple NICs on your VM.</span></span>

1. <span data-ttu-id="ca45f-121">使用 [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) 定義兩個虛擬網路子網路。</span><span class="sxs-lookup"><span data-stu-id="ca45f-121">Define two virtual network subnets with [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span></span> <span data-ttu-id="ca45f-122">下列範例會定義 mySubnetFrontEnd 和 mySubnetBackEnd 的子網路：</span><span class="sxs-lookup"><span data-stu-id="ca45f-122">The following example defines the subnets for *mySubnetFrontEnd* and *mySubnetBackEnd*:</span></span>

    ```powershell
    $mySubnetFrontEnd = New-AzureRmVirtualNetworkSubnetConfig -Name "mySubnetFrontEnd" `
        -AddressPrefix "192.168.1.0/24"
    $mySubnetBackEnd = New-AzureRmVirtualNetworkSubnetConfig -Name "mySubnetBackEnd" `
        -AddressPrefix "192.168.2.0/24"
    ```

2. <span data-ttu-id="ca45f-123">使用 [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) 建立虛擬網路和子網路。</span><span class="sxs-lookup"><span data-stu-id="ca45f-123">Create your virtual network and subnets with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span></span> <span data-ttu-id="ca45f-124">下列範例會建立名為 myVnet 的虛擬網路：</span><span class="sxs-lookup"><span data-stu-id="ca45f-124">The following example creates a virtual network named *myVnet*:</span></span>

    ```powershell
    $myVnet = New-AzureRmVirtualNetwork -ResourceGroupName "myResourceGroup" `
        -Location "EastUs" `
        -Name "myVnet" `
        -AddressPrefix "192.168.0.0/16" `
        -Subnet $mySubnetFrontEnd,$mySubnetBackEnd
    ```


### <a name="create-multiple-nics"></a><span data-ttu-id="ca45f-125">建立多個 NIC</span><span class="sxs-lookup"><span data-stu-id="ca45f-125">Create multiple NICs</span></span>
<span data-ttu-id="ca45f-126">使用 [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) 建立兩個 NIC。</span><span class="sxs-lookup"><span data-stu-id="ca45f-126">Create two NICs with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span></span> <span data-ttu-id="ca45f-127">將一個 NIC 連結到前端子網路，將另一個 NIC 連結到後端子網路。</span><span class="sxs-lookup"><span data-stu-id="ca45f-127">Attach one NIC to the front-end subnet and one NIC to the back-end subnet.</span></span> <span data-ttu-id="ca45f-128">下列範例會建立名為 myNic1 和 myNic2 的兩個 NIC：</span><span class="sxs-lookup"><span data-stu-id="ca45f-128">The following example creates NICs named *myNic1* and *myNic2*:</span></span>

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

<span data-ttu-id="ca45f-129">通常您也可以建立[網路安全性群組](../../virtual-network/virtual-networks-nsg.md)或[負載平衡器](../../load-balancer/load-balancer-overview.md)來協助管理，以及將流量分散到您的 VM。</span><span class="sxs-lookup"><span data-stu-id="ca45f-129">Typically you also create a [network security group](../../virtual-network/virtual-networks-nsg.md) or [load balancer](../../load-balancer/load-balancer-overview.md) to help manage and distribute traffic across your VMs.</span></span> <span data-ttu-id="ca45f-130">[多個 NIC 的 VM](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md)一文可逐步引導您建立網路安全性群組並指派 NIC。</span><span class="sxs-lookup"><span data-stu-id="ca45f-130">The [more detailed multiple-NIC VM](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md) article guides you through creating a network security group and assigning NICs.</span></span>

### <a name="create-the-virtual-machine"></a><span data-ttu-id="ca45f-131">建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="ca45f-131">Create the virtual machine</span></span>
<span data-ttu-id="ca45f-132">現在開始建置您的 VM 組態。</span><span class="sxs-lookup"><span data-stu-id="ca45f-132">Now start to build your VM configuration.</span></span> <span data-ttu-id="ca45f-133">在每個 VM 大小中，您可以新增至 VM 的 NIC 總數是有限制的。</span><span class="sxs-lookup"><span data-stu-id="ca45f-133">Each VM size has a limit for the total number of NICs that you can add to a VM.</span></span> <span data-ttu-id="ca45f-134">如需詳細資訊，請參閱 [Windows VM 大小](sizes.md)。</span><span class="sxs-lookup"><span data-stu-id="ca45f-134">For more information, see [Windows VM sizes](sizes.md).</span></span>

1. <span data-ttu-id="ca45f-135">將您的 VM 認證設定為 `$cred` 變數，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="ca45f-135">Set your VM credentials to the `$cred` variable as follows:</span></span>

    ```powershell
    $cred = Get-Credential
    ```

2. <span data-ttu-id="ca45f-136">使用 [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) 來定義您的 VM。</span><span class="sxs-lookup"><span data-stu-id="ca45f-136">Define your VM with [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig).</span></span> <span data-ttu-id="ca45f-137">下列範例會定義名為 myVM 的 VM，並使用支援兩個以上 NIC 的 VM 大小 (Standard_DS3_v2)：</span><span class="sxs-lookup"><span data-stu-id="ca45f-137">The following example defines a VM named *myVM* and uses a VM size that supports more than two NICs (*Standard_DS3_v2*):</span></span>

    ```powershell
    $vmConfig = New-AzureRmVMConfig -VMName "myVM" -VMSize "Standard_DS3_v2"
    ```

3. <span data-ttu-id="ca45f-138">使用 [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) 和 [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) 建立其餘的 VM 組態。</span><span class="sxs-lookup"><span data-stu-id="ca45f-138">Create the rest of your VM configuration with [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) and [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage).</span></span> <span data-ttu-id="ca45f-139">下列範例會建立 Windows Server 2016 VM：</span><span class="sxs-lookup"><span data-stu-id="ca45f-139">The following example creates a Windows Server 2016 VM:</span></span>

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

4. <span data-ttu-id="ca45f-140">使用 [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface) 連結您先前建立的兩個 NIC：</span><span class="sxs-lookup"><span data-stu-id="ca45f-140">Attach the two NICs that you previously created with [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span></span>

    ```powershell
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $myNic1.Id -Primary
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $myNic2.Id
    ```

5. <span data-ttu-id="ca45f-141">最後，使用 [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) 建立 VM：</span><span class="sxs-lookup"><span data-stu-id="ca45f-141">Finally, create your VM with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm):</span></span>

    ```powershell
    New-AzureRmVM -VM $vmConfig -ResourceGroupName "myResourceGroup" -Location "EastUs"
    ```

## <a name="add-a-nic-to-an-existing-vm"></a><span data-ttu-id="ca45f-142">將 NIC 新增至現有的 VM</span><span class="sxs-lookup"><span data-stu-id="ca45f-142">Add a NIC to an existing VM</span></span>
<span data-ttu-id="ca45f-143">若要將虛擬 NIC 新增至現有 VM，請解除配置 VM、新增虛擬 NIC，然後啟動 VM。</span><span class="sxs-lookup"><span data-stu-id="ca45f-143">To add a virtual NIC to an existing VM, you deallocate the VM, add the virtual NIC, then start the VM.</span></span>

1. <span data-ttu-id="ca45f-144">使用 [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) 來解除配置 VM。</span><span class="sxs-lookup"><span data-stu-id="ca45f-144">Deallocate the VM with [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span></span> <span data-ttu-id="ca45f-145">下列範例會解除配置 myResourceGroup 中名為 myVM 的 VM：</span><span class="sxs-lookup"><span data-stu-id="ca45f-145">The following example deallocates the VM named *myVM* in *myResourceGroup*:</span></span>

    ```powershell
    Stop-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

2. <span data-ttu-id="ca45f-146">使用 [Get-AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm) 取得 VM 的現有組態。</span><span class="sxs-lookup"><span data-stu-id="ca45f-146">Get the existing configuration of the VM with [Get-AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm).</span></span> <span data-ttu-id="ca45f-147">下列範例可取得 myResourceGroup 中名為 myVM 之 VM 的資訊：</span><span class="sxs-lookup"><span data-stu-id="ca45f-147">The following example gets information for the VM named *myVM* in *myResourceGroup*:</span></span>

    ```powershell
    $vm = Get-AzureRmVm -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

3. <span data-ttu-id="ca45f-148">下列範例會使用 [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) 建立虛擬 NIC，其名稱為 myNic3 並已連結至 mySubnetBackEnd。</span><span class="sxs-lookup"><span data-stu-id="ca45f-148">The following example creates a virtual NIC with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) named *myNic3* that is attached to *mySubnetBackEnd*.</span></span> <span data-ttu-id="ca45f-149">接著會使用 [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface)，將虛擬 NIC 連結至 myResourceGroup 中名為 myVM 的 VM：</span><span class="sxs-lookup"><span data-stu-id="ca45f-149">The virtual NIC is then attached to the VM named *myVM* in *myResourceGroup* with [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span></span>

    ```powershell
    # Get info for the back end subnet
    $myVnet = Get-AzureRmVirtualNetwork -Name "myVnet" -ResourceGroupName "myResourceGroup"
    $backEnd = $myVnet.Subnets|?{$_.Name -eq 'mySubnetBackEnd'}

    # Create a virtual NIC
    $myNic3 = New-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" `
        -Name "myNic3" `
        -Location "EastUs" `
        -SubnetId $backEnd.Id

    # Get the ID of the new virtual NIC and add to VM
    $nicId = (Get-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" -Name "MyNic3").Id
    Add-AzureRmVMNetworkInterface -VM $vm -Id $nicId | Update-AzureRmVm -ResourceGroupName "myResourceGroup"
    ```

    ### <a name="primary-virtual-nics"></a><span data-ttu-id="ca45f-150">主要虛擬 NIC</span><span class="sxs-lookup"><span data-stu-id="ca45f-150">Primary virtual NICs</span></span>
    <span data-ttu-id="ca45f-151">您必須在具有多個 NIC 的 VM 上將其中一個 NIC 設為主要。</span><span class="sxs-lookup"><span data-stu-id="ca45f-151">One of the NICs on a multi-NIC VM needs to be primary.</span></span> <span data-ttu-id="ca45f-152">如果 VM 上其中一個現有虛擬 NIC 已設定為主要，即可略過此步驟。</span><span class="sxs-lookup"><span data-stu-id="ca45f-152">If one of the existing virtual NICs on the VM is already set as primary, you can skip this step.</span></span> <span data-ttu-id="ca45f-153">下列範例假設有兩個虛擬 NIC 現在出現在 VM 上，而您想要新增第一個 NIC (`[0]`) 作為主要：</span><span class="sxs-lookup"><span data-stu-id="ca45f-153">The following example assumes that two virtual NICs are now present on a VM and you wish to add the first NIC (`[0]`) as the primary:</span></span>
        
    ```powershell
    # List existing NICs on the VM and find which one is primary
    $vm.NetworkProfile.NetworkInterfaces
    
    # Set NIC 0 to be primary
    $vm.NetworkProfile.NetworkInterfaces[0].Primary = $true
    $vm.NetworkProfile.NetworkInterfaces[1].Primary = $false
    
    # Update the VM state in Azure
    Update-AzureRmVM -VM $vm -ResourceGroupName "myResourceGroup"
    ```

4. <span data-ttu-id="ca45f-154">使用 [Start-AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm) 啟動 VM：</span><span class="sxs-lookup"><span data-stu-id="ca45f-154">Start the VM with [Start-AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm):</span></span>

    ```powershell
    Start-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
    ```

## <a name="remove-a-nic-from-an-existing-vm"></a><span data-ttu-id="ca45f-155">從現有的 VM 移除 NIC</span><span class="sxs-lookup"><span data-stu-id="ca45f-155">Remove a NIC from an existing VM</span></span>
<span data-ttu-id="ca45f-156">若要從現有的 VM 移除虛擬 NIC，您可以解除配置 VM，移除虛擬 NIC，然後啟動 VM。</span><span class="sxs-lookup"><span data-stu-id="ca45f-156">To remove a virtual NIC from an existing VM, you deallocate the VM, remove the virtual NIC, then start the VM.</span></span>

1. <span data-ttu-id="ca45f-157">使用 [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) 來解除配置 VM。</span><span class="sxs-lookup"><span data-stu-id="ca45f-157">Deallocate the VM with [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span></span> <span data-ttu-id="ca45f-158">下列範例會解除配置 myResourceGroup 中名為 myVM 的 VM：</span><span class="sxs-lookup"><span data-stu-id="ca45f-158">The following example deallocates the VM named *myVM* in *myResourceGroup*:</span></span>

    ```powershell
    Stop-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

2. <span data-ttu-id="ca45f-159">使用 [Get-AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm) 取得 VM 的現有組態。</span><span class="sxs-lookup"><span data-stu-id="ca45f-159">Get the existing configuration of the VM with [Get-AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm).</span></span> <span data-ttu-id="ca45f-160">下列範例可取得 myResourceGroup 中名為 myVM 之 VM 的資訊：</span><span class="sxs-lookup"><span data-stu-id="ca45f-160">The following example gets information for the VM named *myVM* in *myResourceGroup*:</span></span>

    ```powershell
    $vm = Get-AzureRmVm -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

3. <span data-ttu-id="ca45f-161">使用 [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface) 取得 NIC 移除相關資訊。</span><span class="sxs-lookup"><span data-stu-id="ca45f-161">Get information about the NIC remove with [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface).</span></span> <span data-ttu-id="ca45f-162">下列範例可取得 myNic3 相關資訊：</span><span class="sxs-lookup"><span data-stu-id="ca45f-162">The following example gets information about *myNic3*:</span></span>

    ```powershell
    # List existing NICs on the VM if you need to determine NIC name
    $vm.NetworkProfile.NetworkInterfaces

    $nicId = (Get-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" -Name "myNic3").Id   
    ```

4. <span data-ttu-id="ca45f-163">使用 [Remove-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/remove-azurermvmnetworkinterface) 移除 NIC，然後使用 [Update-AzureRmVm](/powershell/module/azurerm.compute/update-azurermvm) 更新 VM。</span><span class="sxs-lookup"><span data-stu-id="ca45f-163">Remove the NIC with [Remove-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/remove-azurermvmnetworkinterface) and then update the VM with [Update-AzureRmVm](/powershell/module/azurerm.compute/update-azurermvm).</span></span> <span data-ttu-id="ca45f-164">下列範例會移除前一個步驟中 `$nicId` 所取得的 myNic3：</span><span class="sxs-lookup"><span data-stu-id="ca45f-164">The following example removes *myNic3* as obtained by `$nicId` in the preceding step:</span></span>

    ```powershell
    Remove-AzureRmVMNetworkInterface -VM $vm -NetworkInterfaceIDs $nicId | `
        Update-AzureRmVm -ResourceGroupName "myResourceGroup"
    ```   

5. <span data-ttu-id="ca45f-165">使用 [Start-AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm) 啟動 VM：</span><span class="sxs-lookup"><span data-stu-id="ca45f-165">Start the VM with [Start-AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm):</span></span>

    ```powershell
    Start-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```   

## <a name="create-multiple-nics-with-templates"></a><span data-ttu-id="ca45f-166">使用範本建立多個 NIC</span><span class="sxs-lookup"><span data-stu-id="ca45f-166">Create multiple NICs with templates</span></span>
<span data-ttu-id="ca45f-167">Azure Resource Manager 範本提供一種方式，可在部署期間建立資源的多個執行個體，例如建立多個 NIC。</span><span class="sxs-lookup"><span data-stu-id="ca45f-167">Azure Resource Manager templates provide a way to create multiple instances of a resource during deployment, such as creating multiple NICs.</span></span> <span data-ttu-id="ca45f-168">Resource Manager 範本會使用宣告式 JSON 檔案來定義您的環境。</span><span class="sxs-lookup"><span data-stu-id="ca45f-168">Resource Manager templates use declarative JSON files to define your environment.</span></span> <span data-ttu-id="ca45f-169">如需詳細資訊，請參閱 [Azure Resource Manager 概觀](../../azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="ca45f-169">For more information, see [overview of Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="ca45f-170">您可以使用 *copy* 來指定要建立的執行個體數目：</span><span class="sxs-lookup"><span data-stu-id="ca45f-170">You can use *copy* to specify the number of instances to create:</span></span>

```json
"copy": {
    "name": "multiplenics",
    "count": "[parameters('count')]"
}
```

<span data-ttu-id="ca45f-171">如需詳細資訊，請參閱[使用 copy 建立多個執行個體](../../resource-group-create-multiple.md)。</span><span class="sxs-lookup"><span data-stu-id="ca45f-171">For more information, see [creating multiple instances by using *copy*](../../resource-group-create-multiple.md).</span></span> 

<span data-ttu-id="ca45f-172">您也可以使用 `copyIndex()`，在資源名稱後面附加一個數字。</span><span class="sxs-lookup"><span data-stu-id="ca45f-172">You can also use `copyIndex()` to append a number to a resource name.</span></span> <span data-ttu-id="ca45f-173">接著可以建立 myNic1、MyNic2 等等。</span><span class="sxs-lookup"><span data-stu-id="ca45f-173">You can then create *myNic1*, *MyNic2* and so on.</span></span> <span data-ttu-id="ca45f-174">下列程式碼顯示附加索引值的範例：</span><span class="sxs-lookup"><span data-stu-id="ca45f-174">The following code shows an example of appending the index value:</span></span>

```json
"name": "[concat('myNic', copyIndex())]", 
```

<span data-ttu-id="ca45f-175">您可以閱讀[使用 Resource Manager 範本建立多個 NIC](../../virtual-network/virtual-network-deploy-multinic-arm-template.md)的完整範例。</span><span class="sxs-lookup"><span data-stu-id="ca45f-175">You can read a complete example of [creating multiple NICs by using Resource Manager templates](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ca45f-176">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ca45f-176">Next steps</span></span>
<span data-ttu-id="ca45f-177">嘗試建立具有多個 NIC 的 VM 時，請檢閱 [Windows VM 大小](sizes.md)。</span><span class="sxs-lookup"><span data-stu-id="ca45f-177">Review [Windows VM sizes](sizes.md) when you're trying to create a VM that has multiple NICs.</span></span> <span data-ttu-id="ca45f-178">請注意每個 VM 大小所支援的 NIC 數目上限。</span><span class="sxs-lookup"><span data-stu-id="ca45f-178">Pay attention to the maximum number of NICs that each VM size supports.</span></span> 


