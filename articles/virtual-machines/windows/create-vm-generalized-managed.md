---
title: "在 Azure 中從受控 VM 映像建立 VM | Microsoft Docs"
description: "在 Resource Manager 部署模型中使用 Azure PowerShell，從一般化受控 VM 映像建立 Windows 虛擬機器。"
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: cynthn
ms.openlocfilehash: 2bb2d66271178a64ec0f4642e46b23f5618a56d9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-vm-from-a-managed-image"></a><span data-ttu-id="a570d-103">從 Managed 映像建立 VM</span><span class="sxs-lookup"><span data-stu-id="a570d-103">Create a VM from a managed image</span></span>

<span data-ttu-id="a570d-104">您可以在 Azure 中從受控 VM 映像建立多個 VM。</span><span class="sxs-lookup"><span data-stu-id="a570d-104">You can create multiple VMs from a managed VM image in Azure.</span></span> <span data-ttu-id="a570d-105">受控 VM 映像包含建立 VM 所需的資訊，包括 OS 和資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="a570d-105">A managed VM image contains the information necessary to create a VM, including the OS and data disks.</span></span> <span data-ttu-id="a570d-106">組成映像的 VHD (包括 OS 磁碟和任何資料磁碟) 會儲存為受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="a570d-106">The VHDs that make up the image, including both the OS disks and any data disks, are stored as managed disks.</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="a570d-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="a570d-107">Prerequisites</span></span>

<span data-ttu-id="a570d-108">您必須已經[建立受控 VM 映像](capture-image-resource.md)，才能用來建立新的 VM。</span><span class="sxs-lookup"><span data-stu-id="a570d-108">You need to have already [created a managed VM image](capture-image-resource.md) to use for creating the new VM.</span></span> 

<span data-ttu-id="a570d-109">請確定您擁有最新版的 AzureRM.Compute 和 AzureRM.Network PowerShell 模組。</span><span class="sxs-lookup"><span data-stu-id="a570d-109">Make sure that you have the latest versions of the AzureRM.Compute and AzureRM.Network PowerShell modules.</span></span> <span data-ttu-id="a570d-110">以系統管理員身分開啟 PowerShell 命令提示字元，執行下列命令安裝它們。</span><span class="sxs-lookup"><span data-stu-id="a570d-110">Open a PowerShell prompt as an Administrator and run the following command to install them.</span></span>

```powershell
Install-Module AzureRM.Compute,AzureRM.Network
```
<span data-ttu-id="a570d-111">如需詳細資訊，請參閱 [Azure PowerShell 版本控制](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="a570d-111">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>



## <a name="collect-information-about-the-image"></a><span data-ttu-id="a570d-112">收集映像相關資訊</span><span class="sxs-lookup"><span data-stu-id="a570d-112">Collect information about the image</span></span>

<span data-ttu-id="a570d-113">首先，我們需要收集映像的基本資訊，並建立映像的變數。</span><span class="sxs-lookup"><span data-stu-id="a570d-113">First we need to gather basic information about the image and create a variable for the image.</span></span> <span data-ttu-id="a570d-114">這個範例使用名為 **myImage** 的受控 VM 映像，其位於**美國中西部**位置的 **myResourceGroup** 資源群組中。</span><span class="sxs-lookup"><span data-stu-id="a570d-114">This example uses a managed VM image named **myImage** that is in the **myResourceGroup** resource group in the **West Central US** location.</span></span> 

```powershell
$rgName = "myResourceGroup"
$location = "West Central US"
$imageName = "myImage"
$image = Get-AzureRMImage -ImageName $imageName -ResourceGroupName $rgName
```

## <a name="create-a-virtual-network"></a><span data-ttu-id="a570d-115">建立虛擬網路</span><span class="sxs-lookup"><span data-stu-id="a570d-115">Create a virtual network</span></span>
<span data-ttu-id="a570d-116">建立[虛擬網路](../../virtual-network/virtual-networks-overview.md)的 vNet 和子網路。</span><span class="sxs-lookup"><span data-stu-id="a570d-116">Create the vNet and subnet of the [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="a570d-117">建立子網路。</span><span class="sxs-lookup"><span data-stu-id="a570d-117">Create the subnet.</span></span> <span data-ttu-id="a570d-118">這個範例會建立名為 **mySubnet** 且具有位址首碼 **10.0.0.0/24** 的子網路。</span><span class="sxs-lookup"><span data-stu-id="a570d-118">This example creates a subnet named **mySubnet** with the address prefix of **10.0.0.0/24**.</span></span>  
   
    ```powershell
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="a570d-119">建立虛擬網路</span><span class="sxs-lookup"><span data-stu-id="a570d-119">Create the virtual network.</span></span> <span data-ttu-id="a570d-120">這個範例會建立名為 **myVnet** 且具有位址首碼 **10.0.0.0/16** 的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="a570d-120">This example creates a virtual network named **myVnet** with the address prefix of **10.0.0.0/16**.</span></span>  
   
    ```powershell
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

## <a name="create-a-public-ip-address-and-network-interface"></a><span data-ttu-id="a570d-121">建立公用 IP 位址和網路介面</span><span class="sxs-lookup"><span data-stu-id="a570d-121">Create a public IP address and network interface</span></span>

<span data-ttu-id="a570d-122">若要能夠與虛擬網路中的虛擬機器進行通訊，您需要 [公用 IP 位址](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) 和網路介面。</span><span class="sxs-lookup"><span data-stu-id="a570d-122">To enable communication with the virtual machine in the virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="a570d-123">建立公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="a570d-123">Create a public IP address.</span></span> <span data-ttu-id="a570d-124">此範例會建立名為 **myPip** 的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="a570d-124">This example creates a public IP address named **myPip**.</span></span> 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="a570d-125">建立 NIC。</span><span class="sxs-lookup"><span data-stu-id="a570d-125">Create the NIC.</span></span> <span data-ttu-id="a570d-126">此範例會建立名為 **myNic** 的 NIC。</span><span class="sxs-lookup"><span data-stu-id="a570d-126">This example creates a NIC named **myNic**.</span></span> 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

## <a name="create-the-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="a570d-127">建立網路安全性群組和 RDP 規則</span><span class="sxs-lookup"><span data-stu-id="a570d-127">Create the network security group and an RDP rule</span></span>

<span data-ttu-id="a570d-128">若要能夠使用 RDP 登入 VM，您必須有可在連接埠 3389 上允許 RDP 存取的網路安全性規則 (NSG)。</span><span class="sxs-lookup"><span data-stu-id="a570d-128">To be able to log in to your VM using RDP, you need to have a network security rule (NSG) that allows RDP access on port 3389.</span></span> 

<span data-ttu-id="a570d-129">此範例會建立名為 **myNsg** 的 NSG，其包含的規則 **myRdpRule** 可允許透過連接埠 3389 的 RDP 流量。</span><span class="sxs-lookup"><span data-stu-id="a570d-129">This example creates an NSG named **myNsg** that contains a rule called **myRdpRule** that allows RDP traffic over port 3389.</span></span> <span data-ttu-id="a570d-130">如需 NSG 的詳細資訊，請參閱[使用 PowerShell 對 Azure 中的 VM 開啟連接埠](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="a570d-130">For more information about NSGs, see [Opening ports to a VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

```powershell
$nsgName = "myNsg"
$ruleName = "myRdpRule"
$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name $ruleName -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
```


## <a name="create-a-variable-for-the-virtual-network"></a><span data-ttu-id="a570d-131">建立虛擬網路的變數</span><span class="sxs-lookup"><span data-stu-id="a570d-131">Create a variable for the virtual network</span></span>

<span data-ttu-id="a570d-132">為已完成的虛擬網路建立變數。</span><span class="sxs-lookup"><span data-stu-id="a570d-132">Create a variable for the completed virtual network.</span></span> 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName

```

## <a name="get-the-credentials-for-the-vm"></a><span data-ttu-id="a570d-133">取得 VM 的認證</span><span class="sxs-lookup"><span data-stu-id="a570d-133">Get the credentials for the VM</span></span>

<span data-ttu-id="a570d-134">下列 Cmdlet 會開啟視窗，讓您輸入新的使用者名稱和密碼，作為從遠端存取 VM 時使用的本機管理員帳戶。</span><span class="sxs-lookup"><span data-stu-id="a570d-134">The following cmdlet will open a window where you will enter a new user name and password to use as the local administrator account for remotely accessing the VM.</span></span> 

```powershell
$cred = Get-Credential
```

## <a name="set-variables-for-the-vm-name-computer-name-and-the-size-of-the-vm"></a><span data-ttu-id="a570d-135">設定 VM 名稱、電腦名稱和 VM 大小的變數</span><span class="sxs-lookup"><span data-stu-id="a570d-135">Set variables for the VM name, computer name and the size of the VM</span></span>

1. <span data-ttu-id="a570d-136">建立 VM 名稱和電腦名稱的變數。</span><span class="sxs-lookup"><span data-stu-id="a570d-136">Create variables for the VM name and computer name.</span></span> <span data-ttu-id="a570d-137">此範例將 VM 名稱設定為 **myVM**，將電腦名稱設定為 **myComputer**。</span><span class="sxs-lookup"><span data-stu-id="a570d-137">This example sets the VM name as **myVM** and the computer name as **myComputer**.</span></span>

    ```powershell
    $vmName = "myVM"
    $computerName = "myComputer"
    ```
2. <span data-ttu-id="a570d-138">設定虛擬機器的大小。</span><span class="sxs-lookup"><span data-stu-id="a570d-138">Set the size of the virtual machine.</span></span> <span data-ttu-id="a570d-139">這個範例會建立 **Standard_DS1_v2** 大小的 VM。</span><span class="sxs-lookup"><span data-stu-id="a570d-139">This example creates **Standard_DS1_v2** sized VM.</span></span> <span data-ttu-id="a570d-140">如需詳細資訊，請參閱 [VM 大小](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/)文件。</span><span class="sxs-lookup"><span data-stu-id="a570d-140">See the [VM sizes](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/) documentation for more information.</span></span>

    ```powershell
    $vmSize = "Standard_DS1_v2"
    ```

3. <span data-ttu-id="a570d-141">將 VM 名稱和大小新增至 VM 設定。</span><span class="sxs-lookup"><span data-stu-id="a570d-141">Add the VM name and size to the VM configuration.</span></span>

```powershell
$vm = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize
```

## <a name="set-the-vm-image-as-source-image-for-the-new-vm"></a><span data-ttu-id="a570d-142">將 VM 映像設定為新 VM 的來源映像</span><span class="sxs-lookup"><span data-stu-id="a570d-142">Set the VM image as source image for the new VM</span></span>

<span data-ttu-id="a570d-143">使用受控 VM 映像的識別碼設定來源影像。</span><span class="sxs-lookup"><span data-stu-id="a570d-143">Set the source image using the ID of the managed VM image.</span></span>

```powershell
$vm = Set-AzureRmVMSourceImage -VM $vm -Id $image.Id
```

## <a name="set-the-os-configuration-and-add-the-nic"></a><span data-ttu-id="a570d-144">設定 OS 組態並新增 NIC。</span><span class="sxs-lookup"><span data-stu-id="a570d-144">Set the OS configuration and add the NIC.</span></span>

<span data-ttu-id="a570d-145">輸入儲存體類型 (PremiumLRS 或 StandardLRS) 和 OS 磁碟的大小。</span><span class="sxs-lookup"><span data-stu-id="a570d-145">Enter the storage type (PremiumLRS or StandardLRS) and the size of the OS disk.</span></span> <span data-ttu-id="a570d-146">這個範例將帳戶類型設定為 **PremiumLRS**、將磁碟大小設定為 **128GB**，並將磁碟快取設定為 **ReadWrite**。</span><span class="sxs-lookup"><span data-stu-id="a570d-146">This example sets the account type to **PremiumLRS**, the disk size to **128 GB** and disk caching to **ReadWrite**.</span></span>

```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm  -StorageAccountType PremiumLRS -DiskSizeInGB 128 `
-CreateOption FromImage -Caching ReadWrite

$vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName $computerName `
-Credential $cred -ProvisionVMAgent -EnableAutoUpdate

$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

## <a name="create-the-vm"></a><span data-ttu-id="a570d-147">建立 VM</span><span class="sxs-lookup"><span data-stu-id="a570d-147">Create the VM</span></span>

<span data-ttu-id="a570d-148">使用我們已建立並儲存在 **$vm** 變數中的組態來建立新 VM。</span><span class="sxs-lookup"><span data-stu-id="a570d-148">Create the new Vm using the configuration that we have built and stored in the **$vm** variable.</span></span>

```powershell
New-AzureRmVM -VM $vm -ResourceGroupName $rgName -Location $location
```

## <a name="verify-that-the-vm-was-created"></a><span data-ttu-id="a570d-149">確認已建立 VM</span><span class="sxs-lookup"><span data-stu-id="a570d-149">Verify that the VM was created</span></span>
<span data-ttu-id="a570d-150">完成時，在 [Azure 入口網站](https://portal.azure.com)的 [瀏覽] > [虛擬機器] 底下，或是使用下列 PowerShell 命令，應該就可以看到新建立的 VM：</span><span class="sxs-lookup"><span data-stu-id="a570d-150">When complete, you should see the newly created VM in the [Azure portal](https://portal.azure.com) under **Browse** > **Virtual machines**, or by using the following PowerShell commands:</span></span>

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="a570d-151">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a570d-151">Next steps</span></span>
<span data-ttu-id="a570d-152">若要使用 PowerShell 來管理您的新虛擬機器，請參閱[使用 Azure PowerShell 模組來建立和管理 Windows VM](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="a570d-152">To manage your new virtual machine with Azure PowerShell, see [Create and manage Windows VMs with the Azure PowerShell module](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

