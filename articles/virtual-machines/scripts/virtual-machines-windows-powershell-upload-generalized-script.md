---
title: "aaaUpload 一般化的 VHD tooAzure PowerShell 指令碼範例 |Microsoft 文件"
description: "PowerShell 範例指令碼 tooupload 一般化的 VHD tooAzure，並建立新的 VM 使用 hello 資源管理員部署模型和受管理的磁碟。"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/18/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 72b4ff09eb7a6ba1604b9d5cbac51e60eded7545
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="sample-script-tooupload-a-vhd-tooazure-and-create-a-new-vm"></a><span data-ttu-id="fa33a-103">範例指令碼 tooupload VHD tooAzure 並建立新的 VM</span><span class="sxs-lookup"><span data-stu-id="fa33a-103">Sample script tooupload a VHD tooAzure and create a new VM</span></span>

<span data-ttu-id="fa33a-104">此指令碼會將本機的.vhd 檔從一般化 VM 和 tooAzure 上傳、 建立受管理的磁碟映像和使用 hello toocreate 新的 VM。</span><span class="sxs-lookup"><span data-stu-id="fa33a-104">This script takes a local .vhd file from a generalized VM and uploads it tooAzure, creates a Managed Disk image and uses hello toocreate a new VM.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="fa33a-105">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="fa33a-105">Sample script</span></span>

```powershell
# Provide values for hello variables
$resourceGroup = 'myResourceGroup'
$location = 'EastUS'
$storageaccount = 'mystorageaccount'
$storageType = 'Standard_LRS'
$containername = 'mycontainer'
$localPath = 'C:\Users\Public\Documents\Hyper-V\VHDs\generalized.vhd'
$vmName = 'myVM'
$imageName = 'myImage'
$vhdName = 'myUploadedVhd.vhd'
$diskSizeGB = '128'
$subnetName = 'mySubnet'
$vnetName = 'myVnet'
$ipName = 'myPip'
$nicName = 'myNic'
$nsgName = 'myNsg'
$ruleName = 'myRdpRule'
$vmName = 'myVM'
$computerName = 'myComputerName'
$vmSize = 'Standard_DS1_v2'

# Get hello username and password toobe used for hello administrators account on hello VM. 
# This is used when connecting toohello VM using RDP.

$cred = Get-Credential

# Upload hello VHD
New-AzureRmResourceGroup -Name $resourceGroup -Location $location
New-AzureRmStorageAccount -ResourceGroupName $resourceGroup -Name $storageAccount -Location $location `
    -SkuName $storageType -Kind "Storage"
$urlOfUploadedImageVhd = ('https://' + $storageaccount + '.blob.core.windows.net/' + $containername + '/' + $vhdName)
Add-AzureRmVhd -ResourceGroupName $resourceGroup -Destination $urlOfUploadedImageVhd `
    -LocalFilePath $localPath

# Note: Uploading hello VHD may take awhile!

# Create a managed image from hello uploaded VHD 
$imageConfig = New-AzureRmImageConfig -Location $location
$imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsType Windows -OsState Generalized `
    -BlobUri $urlOfUploadedImageVhd
$image = New-AzureRmImage -ImageName $imageName -ResourceGroupName $resourceGroup -Image $imageConfig
 
# Create hello networking resources
$singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
$vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $resourceGroup -Location $location `
    -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
$pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $resourceGroup -Location $location `
    -AllocationMethod Dynamic
$nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $resourceGroup -Location $location `
    -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name $ruleName -Description 'Allow RDP' -Access Allow `
    -Protocol Tcp -Direction Inbound -Priority 110 -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $resourceGroup -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $resourceGroup -Name $vnetName

# Start building hello VM configuration
$vm = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize

# Set hello VM image as source image for hello new VM
$vm = Set-AzureRmVMSourceImage -VM $vm -Id $image.Id

# Finish hello VM configuration and add hello NIC.
$vm = Set-AzureRmVMOSDisk -VM $vm  -DiskSizeInGB $diskSizeGB -CreateOption FromImage -Caching ReadWrite
$vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName $computerName -Credential $cred `
    -ProvisionVMAgent -EnableAutoUpdate
$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id

# Create hello VM
New-AzureRmVM -VM $vm -ResourceGroupName $resourceGroup -Location $location

# Verify that hello VM was created
$vmList = Get-AzureRmVM -ResourceGroupName $resourceGroup
$vmList.Name


```


<!-- 
[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-iis/create-windows-vm-iis.ps1 "Create VM IIS")] -->

## <a name="clean-up-deployment"></a><span data-ttu-id="fa33a-106">清除部署</span><span class="sxs-lookup"><span data-stu-id="fa33a-106">Clean up deployment</span></span> 

<span data-ttu-id="fa33a-107">執行下列命令 tooremove hello 資源群組、 VM 和所有相關的資源的 hello。</span><span class="sxs-lookup"><span data-stu-id="fa33a-107">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name $resourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="fa33a-108">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="fa33a-108">Script explanation</span></span>

<span data-ttu-id="fa33a-109">此指令碼會使用下列命令 toocreate hello 部署的 hello。</span><span class="sxs-lookup"><span data-stu-id="fa33a-109">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="fa33a-110">Hello 資料表中的每個項目連結 toocommand 特定文件。</span><span class="sxs-lookup"><span data-stu-id="fa33a-110">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="fa33a-111">命令</span><span class="sxs-lookup"><span data-stu-id="fa33a-111">Command</span></span>                                                                                                             | <span data-ttu-id="fa33a-112">注意事項</span><span class="sxs-lookup"><span data-stu-id="fa33a-112">Notes</span></span>                                                                                                                                                                                |
|---------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [<span data-ttu-id="fa33a-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="fa33a-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup)                           | <span data-ttu-id="fa33a-114">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="fa33a-114">Creates a resource group in which all resources are stored.</span></span>                                                                                                                          |
| [<span data-ttu-id="fa33a-115">New-AzureRmStorageAccount</span><span class="sxs-lookup"><span data-stu-id="fa33a-115">New-AzureRmStorageAccount</span></span>](/powershell/module/azurerm.resources/new-azurermstorageaccount)                         | <span data-ttu-id="fa33a-116">建立儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="fa33a-116">Creates a storage account.</span></span>                                                                                                                                                           |
| [<span data-ttu-id="fa33a-117">Add-AzureRmVhd</span><span class="sxs-lookup"><span data-stu-id="fa33a-117">Add-AzureRmVhd</span></span>](/powershell/module/azurerm.resources/add-azurermvhd)                                               | <span data-ttu-id="fa33a-118">上傳從內部部署虛擬機器 tooa blob 在 Azure 中的雲端儲存體帳戶中的虛擬硬碟。</span><span class="sxs-lookup"><span data-stu-id="fa33a-118">Uploads a virtual hard disk from an on-premises virtual machine tooa blob in a cloud storage account in Azure.</span></span>                                                                       |
| [<span data-ttu-id="fa33a-119">New-AzureRmImageConfig</span><span class="sxs-lookup"><span data-stu-id="fa33a-119">New-AzureRmImageConfig</span></span>](/powershell/module/azurerm.resources/new-azurermimageconfig)                               | <span data-ttu-id="fa33a-120">建立可設定的映像物件。</span><span class="sxs-lookup"><span data-stu-id="fa33a-120">Creates a configurable image object.</span></span>                                                                                                                                                 |
| [<span data-ttu-id="fa33a-121">Set-AzureRmImageOsDisk</span><span class="sxs-lookup"><span data-stu-id="fa33a-121">Set-AzureRmImageOsDisk</span></span>](/powershell/module/azurerm.resources/set-azurermimageosdisk)                               | <span data-ttu-id="fa33a-122">映像物件上設定 hello 作業系統磁碟屬性。</span><span class="sxs-lookup"><span data-stu-id="fa33a-122">Sets hello operating system disk properties on an image object.</span></span>                                                                                                                        |
| [<span data-ttu-id="fa33a-123">New-AzureRmImage</span><span class="sxs-lookup"><span data-stu-id="fa33a-123">New-AzureRmImage</span></span>](/powershell/module/azurerm.resources/new-azurermimage)                                           | <span data-ttu-id="fa33a-124">建立新的映像。</span><span class="sxs-lookup"><span data-stu-id="fa33a-124">Creates a new image.</span></span>                                                                                                                                                                 |
| [<span data-ttu-id="fa33a-125">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="fa33a-125">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.resources/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="fa33a-126">建立子網路組態。</span><span class="sxs-lookup"><span data-stu-id="fa33a-126">Creates a subnet configuration.</span></span> <span data-ttu-id="fa33a-127">此設定可搭配 hello 虛擬網路建立程序。</span><span class="sxs-lookup"><span data-stu-id="fa33a-127">This configuration is used with hello virtual network creation process.</span></span>                                                                                |
| [<span data-ttu-id="fa33a-128">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="fa33a-128">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.resources/new-azurermvirtualnetwork)                         | <span data-ttu-id="fa33a-129">建立虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="fa33a-129">Creates a virtual network.</span></span>                                                                                                                                                           |
| [<span data-ttu-id="fa33a-130">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="fa33a-130">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.resources/new-azurermpublicipaddress)                       | <span data-ttu-id="fa33a-131">建立公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="fa33a-131">Creates a public IP address.</span></span>                                                                                                                                                         |
| [<span data-ttu-id="fa33a-132">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="fa33a-132">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.resources/new-azurermnetworkinterface)                     | <span data-ttu-id="fa33a-133">建立網路介面。</span><span class="sxs-lookup"><span data-stu-id="fa33a-133">Creates a network interface.</span></span>                                                                                                                                                         |
| [<span data-ttu-id="fa33a-134">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="fa33a-134">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.resources/new-azurermnetworksecurityruleconfig)   | <span data-ttu-id="fa33a-135">建立網路安全性群組規則組態。</span><span class="sxs-lookup"><span data-stu-id="fa33a-135">Creates a network security group rule configuration.</span></span> <span data-ttu-id="fa33a-136">此設定時，使用的 toocreate NSG 規則建立 hello NSG。</span><span class="sxs-lookup"><span data-stu-id="fa33a-136">This configuration is used toocreate an NSG rule when hello NSG is created.</span></span>                                                       |
| [<span data-ttu-id="fa33a-137">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="fa33a-137">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.resources/new-azurermnetworksecuritygroup)             | <span data-ttu-id="fa33a-138">建立網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="fa33a-138">Creates a network security group.</span></span>                                                                                                                                                    |
| [<span data-ttu-id="fa33a-139">Get-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="fa33a-139">Get-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.resources/get-azurermvirtualnetwork)                         | <span data-ttu-id="fa33a-140">取得資源群組中的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="fa33a-140">Gets a virtual network in a resource group.</span></span>                                                                                                                                          |
| [<span data-ttu-id="fa33a-141">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="fa33a-141">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.resources/new-azurermvmconfig)                                     | <span data-ttu-id="fa33a-142">建立 VM 組態。</span><span class="sxs-lookup"><span data-stu-id="fa33a-142">Creates a VM configuration.</span></span> <span data-ttu-id="fa33a-143">此組態包括 VM 名稱、作業系統和系統管理認證等資訊。</span><span class="sxs-lookup"><span data-stu-id="fa33a-143">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="fa33a-144">在建立 VM 時，會使用 hello 組態。</span><span class="sxs-lookup"><span data-stu-id="fa33a-144">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="fa33a-145">Set-AzureRmVMSourceImage</span><span class="sxs-lookup"><span data-stu-id="fa33a-145">Set-AzureRmVMSourceImage</span></span>](/powershell/module/azurerm.resources/set-azurermvmsourceimage)                           | <span data-ttu-id="fa33a-146">指定虛擬機器的映像。</span><span class="sxs-lookup"><span data-stu-id="fa33a-146">Specifies an image for a virtual machine.</span></span>                                                                                                                                            |
| [<span data-ttu-id="fa33a-147">Set-AzureRmVMOSDisk</span><span class="sxs-lookup"><span data-stu-id="fa33a-147">Set-AzureRmVMOSDisk</span></span>](/powershell/module/azurerm.resources/set-azurermvmosdisk)                                     | <span data-ttu-id="fa33a-148">虛擬機器上設定 hello 作業系統磁碟屬性。</span><span class="sxs-lookup"><span data-stu-id="fa33a-148">Sets hello operating system disk properties on a virtual machine.</span></span>                                                                                                                      |
| [<span data-ttu-id="fa33a-149">Set-AzureRmVMOperatingSystem</span><span class="sxs-lookup"><span data-stu-id="fa33a-149">Set-AzureRmVMOperatingSystem</span></span>](/powershell/module/azurerm.resources/set-azurermvmoperatingsystem)                   | <span data-ttu-id="fa33a-150">虛擬機器上設定 hello 作業系統磁碟屬性。</span><span class="sxs-lookup"><span data-stu-id="fa33a-150">Sets hello operating system disk properties on a virtual machine.</span></span>                                                                                                                      |
| [<span data-ttu-id="fa33a-151">Add-AzureRmVMNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="fa33a-151">Add-AzureRmVMNetworkInterface</span></span>](/powershell/module/azurerm.resources/add-azurermvmnetworkinterface)                 | <span data-ttu-id="fa33a-152">新增網路介面 tooa 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="fa33a-152">Adds a network interface tooa virtual machine.</span></span>                                                                                                                                       |
| [<span data-ttu-id="fa33a-153">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="fa33a-153">New-AzureRmVM</span></span>](/powershell/module/azurerm.resources/new-azurermvm)                                                 | <span data-ttu-id="fa33a-154">建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="fa33a-154">Create a virtual machine.</span></span>                                                                                                                                                            |
| [<span data-ttu-id="fa33a-155">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="fa33a-155">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup)                     | <span data-ttu-id="fa33a-156">移除資源群組及其內含的所有資源。</span><span class="sxs-lookup"><span data-stu-id="fa33a-156">Removes a resource group and all resources contained within.</span></span>                                                                                                                         |

## <a name="next-steps"></a><span data-ttu-id="fa33a-157">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fa33a-157">Next steps</span></span>

<span data-ttu-id="fa33a-158">如需有關 hello Azure PowerShell 模組的詳細資訊，請參閱[Azure PowerShell 文件](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="fa33a-158">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="fa33a-159">其他虛擬機器的 PowerShell 指令碼範例可以在 hello [Azure Windows VM 文件](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="fa33a-159">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
