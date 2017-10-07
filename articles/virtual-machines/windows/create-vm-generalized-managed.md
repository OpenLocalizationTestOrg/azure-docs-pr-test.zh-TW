---
title: "從受管理的 VM 映像，在 Azure 中的 VM aaaCreate |Microsoft 文件"
description: "從通用 managed VM 映像在 hello Resource Manager 部署模型中使用 Azure PowerShell 中建立 Windows 虛擬機器。"
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
ms.openlocfilehash: 5036ef1533c144a9a328e94599b359e0166f337d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-from-a-managed-image"></a><span data-ttu-id="f0a46-103">從 Managed 映像建立 VM</span><span class="sxs-lookup"><span data-stu-id="f0a46-103">Create a VM from a managed image</span></span>

<span data-ttu-id="f0a46-104">您可以在 Azure 中從受控 VM 映像建立多個 VM。</span><span class="sxs-lookup"><span data-stu-id="f0a46-104">You can create multiple VMs from a managed VM image in Azure.</span></span> <span data-ttu-id="f0a46-105">受管理的 VM 映像包含 hello 資訊必要 toocreate VM，包括 hello OS 和資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="f0a46-105">A managed VM image contains hello information necessary toocreate a VM, including hello OS and data disks.</span></span> <span data-ttu-id="f0a46-106">hello hello 映像，包括 hello OS 磁碟和任何資料磁碟所組成，會儲存成受管理的磁碟的 Vhd。</span><span class="sxs-lookup"><span data-stu-id="f0a46-106">hello VHDs that make up hello image, including both hello OS disks and any data disks, are stored as managed disks.</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="f0a46-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="f0a46-107">Prerequisites</span></span>

<span data-ttu-id="f0a46-108">您必須已經 toohave[建立受管理的 VM 映像](capture-image-resource.md)toouse 建立 hello 新的 VM。</span><span class="sxs-lookup"><span data-stu-id="f0a46-108">You need toohave already [created a managed VM image](capture-image-resource.md) toouse for creating hello new VM.</span></span> 

<span data-ttu-id="f0a46-109">請確定您已擁有 hello hello AzureRM.Compute 和 AzureRM.Network PowerShell 模組最新版本。</span><span class="sxs-lookup"><span data-stu-id="f0a46-109">Make sure that you have hello latest versions of hello AzureRM.Compute and AzureRM.Network PowerShell modules.</span></span> <span data-ttu-id="f0a46-110">開啟以系統管理員的 PowerShell 命令提示字元，然後執行下列命令 tooinstall hello 它們。</span><span class="sxs-lookup"><span data-stu-id="f0a46-110">Open a PowerShell prompt as an Administrator and run hello following command tooinstall them.</span></span>

```powershell
Install-Module AzureRM.Compute,AzureRM.Network
```
<span data-ttu-id="f0a46-111">如需詳細資訊，請參閱 [Azure PowerShell 版本控制](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="f0a46-111">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>



## <a name="collect-information-about-hello-image"></a><span data-ttu-id="f0a46-112">收集 hello 映像的相關資訊</span><span class="sxs-lookup"><span data-stu-id="f0a46-112">Collect information about hello image</span></span>

<span data-ttu-id="f0a46-113">首先我們需要 toogather hello 映像相關資訊的基本資訊，並針對 hello 映像建立的變數。</span><span class="sxs-lookup"><span data-stu-id="f0a46-113">First we need toogather basic information about hello image and create a variable for hello image.</span></span> <span data-ttu-id="f0a46-114">這個範例會使用名為受管理的 VM 映像**myImage**也就是在 hello **myResourceGroup** hello 中的資源群組**中央美國西部**位置。</span><span class="sxs-lookup"><span data-stu-id="f0a46-114">This example uses a managed VM image named **myImage** that is in hello **myResourceGroup** resource group in hello **West Central US** location.</span></span> 

```powershell
$rgName = "myResourceGroup"
$location = "West Central US"
$imageName = "myImage"
$image = Get-AzureRMImage -ImageName $imageName -ResourceGroupName $rgName
```

## <a name="create-a-virtual-network"></a><span data-ttu-id="f0a46-115">建立虛擬網路</span><span class="sxs-lookup"><span data-stu-id="f0a46-115">Create a virtual network</span></span>
<span data-ttu-id="f0a46-116">建立 hello vNet 和子網路的 hello[虛擬網路](../../virtual-network/virtual-networks-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="f0a46-116">Create hello vNet and subnet of hello [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="f0a46-117">建立 hello 子網路。</span><span class="sxs-lookup"><span data-stu-id="f0a46-117">Create hello subnet.</span></span> <span data-ttu-id="f0a46-118">這個範例會建立名為的子網路**mySubnet** hello 位址前置詞與**10.0.0.0/24**。</span><span class="sxs-lookup"><span data-stu-id="f0a46-118">This example creates a subnet named **mySubnet** with hello address prefix of **10.0.0.0/24**.</span></span>  
   
    ```powershell
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="f0a46-119">建立 hello 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="f0a46-119">Create hello virtual network.</span></span> <span data-ttu-id="f0a46-120">這個範例會建立虛擬網路，名為**myVnet** hello 位址前置詞與**10.0.0.0/16**。</span><span class="sxs-lookup"><span data-stu-id="f0a46-120">This example creates a virtual network named **myVnet** with hello address prefix of **10.0.0.0/16**.</span></span>  
   
    ```powershell
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

## <a name="create-a-public-ip-address-and-network-interface"></a><span data-ttu-id="f0a46-121">建立公用 IP 位址和網路介面</span><span class="sxs-lookup"><span data-stu-id="f0a46-121">Create a public IP address and network interface</span></span>

<span data-ttu-id="f0a46-122">tooenable 與 hello hello 虛擬網路中的虛擬機器的通訊，您需要[公用 IP 位址](../../virtual-network/virtual-network-ip-addresses-overview-arm.md)和網路介面。</span><span class="sxs-lookup"><span data-stu-id="f0a46-122">tooenable communication with hello virtual machine in hello virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="f0a46-123">建立公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="f0a46-123">Create a public IP address.</span></span> <span data-ttu-id="f0a46-124">此範例會建立名為 **myPip** 的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="f0a46-124">This example creates a public IP address named **myPip**.</span></span> 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="f0a46-125">建立 hello nic。</span><span class="sxs-lookup"><span data-stu-id="f0a46-125">Create hello NIC.</span></span> <span data-ttu-id="f0a46-126">此範例會建立名為 **myNic** 的 NIC。</span><span class="sxs-lookup"><span data-stu-id="f0a46-126">This example creates a NIC named **myNic**.</span></span> 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

## <a name="create-hello-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="f0a46-127">建立網路安全性群組 hello 和 RDP 規則</span><span class="sxs-lookup"><span data-stu-id="f0a46-127">Create hello network security group and an RDP rule</span></span>

<span data-ttu-id="f0a46-128">toobe 無法 toolog tooyour 中的使用 RDP 的 VM，您需要 toohave 網路安全性規則 (NSG)，允許連接埠 3389 RDP 存取權。</span><span class="sxs-lookup"><span data-stu-id="f0a46-128">toobe able toolog in tooyour VM using RDP, you need toohave a network security rule (NSG) that allows RDP access on port 3389.</span></span> 

<span data-ttu-id="f0a46-129">此範例會建立名為 **myNsg** 的 NSG，其包含的規則 **myRdpRule** 可允許透過連接埠 3389 的 RDP 流量。</span><span class="sxs-lookup"><span data-stu-id="f0a46-129">This example creates an NSG named **myNsg** that contains a rule called **myRdpRule** that allows RDP traffic over port 3389.</span></span> <span data-ttu-id="f0a46-130">如需 Nsg 的詳細資訊，請參閱[使用 PowerShell 在 Azure 中開啟連接埠 tooa VM](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="f0a46-130">For more information about NSGs, see [Opening ports tooa VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

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


## <a name="create-a-variable-for-hello-virtual-network"></a><span data-ttu-id="f0a46-131">針對 hello 虛擬網路建立的變數</span><span class="sxs-lookup"><span data-stu-id="f0a46-131">Create a variable for hello virtual network</span></span>

<span data-ttu-id="f0a46-132">建立 hello 完成虛擬網路的變數。</span><span class="sxs-lookup"><span data-stu-id="f0a46-132">Create a variable for hello completed virtual network.</span></span> 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName

```

## <a name="get-hello-credentials-for-hello-vm"></a><span data-ttu-id="f0a46-133">取得 hello VM hello 認證</span><span class="sxs-lookup"><span data-stu-id="f0a46-133">Get hello credentials for hello VM</span></span>

<span data-ttu-id="f0a46-134">hello 下列 cmdlet 會開啟的視窗，您就會在輸入新的使用者名稱和密碼 toouse hello 的本機 administrator 帳戶從遠端存取 hello VM。</span><span class="sxs-lookup"><span data-stu-id="f0a46-134">hello following cmdlet will open a window where you will enter a new user name and password toouse as hello local administrator account for remotely accessing hello VM.</span></span> 

```powershell
$cred = Get-Credential
```

## <a name="set-variables-for-hello-vm-name-computer-name-and-hello-size-of-hello-vm"></a><span data-ttu-id="f0a46-135">Hello VM 設定的變數名稱，電腦名稱，而且 hello hello VM 的大小</span><span class="sxs-lookup"><span data-stu-id="f0a46-135">Set variables for hello VM name, computer name and hello size of hello VM</span></span>

1. <span data-ttu-id="f0a46-136">建立 hello VM 名稱與電腦名稱的變數。</span><span class="sxs-lookup"><span data-stu-id="f0a46-136">Create variables for hello VM name and computer name.</span></span> <span data-ttu-id="f0a46-137">此範例會設定為 hello VM 名稱**myVM**和 hello 電腦名稱與**myComputer**。</span><span class="sxs-lookup"><span data-stu-id="f0a46-137">This example sets hello VM name as **myVM** and hello computer name as **myComputer**.</span></span>

    ```powershell
    $vmName = "myVM"
    $computerName = "myComputer"
    ```
2. <span data-ttu-id="f0a46-138">設定 hello hello 虛擬機器大小。</span><span class="sxs-lookup"><span data-stu-id="f0a46-138">Set hello size of hello virtual machine.</span></span> <span data-ttu-id="f0a46-139">這個範例會建立 **Standard_DS1_v2** 大小的 VM。</span><span class="sxs-lookup"><span data-stu-id="f0a46-139">This example creates **Standard_DS1_v2** sized VM.</span></span> <span data-ttu-id="f0a46-140">請參閱 hello [VM 大小](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/)文件的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="f0a46-140">See hello [VM sizes](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/) documentation for more information.</span></span>

    ```powershell
    $vmSize = "Standard_DS1_v2"
    ```

3. <span data-ttu-id="f0a46-141">加入 hello VM 名稱和大小 toohello VM 組態。</span><span class="sxs-lookup"><span data-stu-id="f0a46-141">Add hello VM name and size toohello VM configuration.</span></span>

```powershell
$vm = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize
```

## <a name="set-hello-vm-image-as-source-image-for-hello-new-vm"></a><span data-ttu-id="f0a46-142">集 hello VM 映像 hello 的來源映像為新的 VM</span><span class="sxs-lookup"><span data-stu-id="f0a46-142">Set hello VM image as source image for hello new VM</span></span>

<span data-ttu-id="f0a46-143">設定使用受管理的 hello VM 映像的 hello 識別碼 hello 來源映像。</span><span class="sxs-lookup"><span data-stu-id="f0a46-143">Set hello source image using hello ID of hello managed VM image.</span></span>

```powershell
$vm = Set-AzureRmVMSourceImage -VM $vm -Id $image.Id
```

## <a name="set-hello-os-configuration-and-add-hello-nic"></a><span data-ttu-id="f0a46-144">設定 hello 作業系統設定以及新增 hello nic。</span><span class="sxs-lookup"><span data-stu-id="f0a46-144">Set hello OS configuration and add hello NIC.</span></span>

<span data-ttu-id="f0a46-145">輸入 hello 儲存類型 （PremiumLRS 或 StandardLRS） 和 hello hello 作業系統磁碟大小。</span><span class="sxs-lookup"><span data-stu-id="f0a46-145">Enter hello storage type (PremiumLRS or StandardLRS) and hello size of hello OS disk.</span></span> <span data-ttu-id="f0a46-146">此範例會設定 hello 帳戶類型太**PremiumLRS**，太 hello 磁碟大小**128 GB**和磁碟快取太**ReadWrite**。</span><span class="sxs-lookup"><span data-stu-id="f0a46-146">This example sets hello account type too**PremiumLRS**, hello disk size too**128 GB** and disk caching too**ReadWrite**.</span></span>

```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm  -StorageAccountType PremiumLRS -DiskSizeInGB 128 `
-CreateOption FromImage -Caching ReadWrite

$vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName $computerName `
-Credential $cred -ProvisionVMAgent -EnableAutoUpdate

$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

## <a name="create-hello-vm"></a><span data-ttu-id="f0a46-147">建立 hello VM</span><span class="sxs-lookup"><span data-stu-id="f0a46-147">Create hello VM</span></span>

<span data-ttu-id="f0a46-148">建立新的 Vm 使用 hello 組態，我們已建立及儲存在 hello 的 hello **$vm**變數。</span><span class="sxs-lookup"><span data-stu-id="f0a46-148">Create hello new Vm using hello configuration that we have built and stored in hello **$vm** variable.</span></span>

```powershell
New-AzureRmVM -VM $vm -ResourceGroupName $rgName -Location $location
```

## <a name="verify-that-hello-vm-was-created"></a><span data-ttu-id="f0a46-149">請確認 VM 已建立該 hello</span><span class="sxs-lookup"><span data-stu-id="f0a46-149">Verify that hello VM was created</span></span>
<span data-ttu-id="f0a46-150">完成時，您應該會看到新建立的 VM 中 hello hello [Azure 入口網站](https://portal.azure.com)下**瀏覽** > **虛擬機器**，或使用 hello 下列PowerShell 命令：</span><span class="sxs-lookup"><span data-stu-id="f0a46-150">When complete, you should see hello newly created VM in hello [Azure portal](https://portal.azure.com) under **Browse** > **Virtual machines**, or by using hello following PowerShell commands:</span></span>

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="f0a46-151">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f0a46-151">Next steps</span></span>
<span data-ttu-id="f0a46-152">toomanage 新的虛擬機器使用 Azure PowerShell，請參閱[建立及管理 Windows Vm hello Azure PowerShell 模組](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="f0a46-152">toomanage your new virtual machine with Azure PowerShell, see [Create and manage Windows VMs with hello Azure PowerShell module](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

