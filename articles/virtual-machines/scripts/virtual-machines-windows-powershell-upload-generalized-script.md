---
title: "將通用 VHD 上傳至 Azure 的 PowerShell 指令碼範例 | Microsoft Docs"
description: "使用 Resource Manager 部署模型和受控磁碟，將通用 VHD 上傳至 Azure 並新建 VM 的 PowerShell 範例指令碼。"
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
ms.openlocfilehash: cd3d87bb4384971e28d3330cd5c1a3d351129036
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="sample-script-to-upload-a-vhd-to-azure-and-create-a-new-vm"></a><span data-ttu-id="32f67-103">將 VHD 上傳至 Azure 並新建 VM 的範例指令碼</span><span class="sxs-lookup"><span data-stu-id="32f67-103">Sample script to upload a VHD to Azure and create a new VM</span></span>

<span data-ttu-id="32f67-104">此指令碼會使用來自通用 VM 的本機 .vhd 檔案，將其上傳到 Azure，再建立受控磁碟映像，並新建 VM。</span><span class="sxs-lookup"><span data-stu-id="32f67-104">This script takes a local .vhd file from a generalized VM and uploads it to Azure, creates a Managed Disk image and uses the to create a new VM.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="32f67-105">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="32f67-105">Sample script</span></span>

```powershell
# Provide values for the variables
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

# Get the username and password to be used for the administrators account on the VM. 
# This is used when connecting to the VM using RDP.

$cred = Get-Credential

# Upload the VHD
New-AzureRmResourceGroup -Name $resourceGroup -Location $location
New-AzureRmStorageAccount -ResourceGroupName $resourceGroup -Name $storageAccount -Location $location `
    -SkuName $storageType -Kind "Storage"
$urlOfUploadedImageVhd = ('https://' + $storageaccount + '.blob.core.windows.net/' + $containername + '/' + $vhdName)
Add-AzureRmVhd -ResourceGroupName $resourceGroup -Destination $urlOfUploadedImageVhd `
    -LocalFilePath $localPath

# Note: Uploading the VHD may take awhile!

# Create a managed image from the uploaded VHD 
$imageConfig = New-AzureRmImageConfig -Location $location
$imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsType Windows -OsState Generalized `
    -BlobUri $urlOfUploadedImageVhd
$image = New-AzureRmImage -ImageName $imageName -ResourceGroupName $resourceGroup -Image $imageConfig
 
# Create the networking resources
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

# Start building the VM configuration
$vm = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize

# Set the VM image as source image for the new VM
$vm = Set-AzureRmVMSourceImage -VM $vm -Id $image.Id

# Finish the VM configuration and add the NIC.
$vm = Set-AzureRmVMOSDisk -VM $vm  -DiskSizeInGB $diskSizeGB -CreateOption FromImage -Caching ReadWrite
$vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName $computerName -Credential $cred `
    -ProvisionVMAgent -EnableAutoUpdate
$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id

# Create the VM
New-AzureRmVM -VM $vm -ResourceGroupName $resourceGroup -Location $location

# Verify that the VM was created
$vmList = Get-AzureRmVM -ResourceGroupName $resourceGroup
$vmList.Name


```


<!-- 
[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-iis/create-windows-vm-iis.ps1 "Create VM IIS")] -->

## <a name="clean-up-deployment"></a><span data-ttu-id="32f67-106">清除部署</span><span class="sxs-lookup"><span data-stu-id="32f67-106">Clean up deployment</span></span> 

<span data-ttu-id="32f67-107">執行下列命令來移除資源群組、VM 和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="32f67-107">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name $resourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="32f67-108">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="32f67-108">Script explanation</span></span>

<span data-ttu-id="32f67-109">此指令碼會使用下列命令來建立部署。</span><span class="sxs-lookup"><span data-stu-id="32f67-109">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="32f67-110">下表中的每個項目都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="32f67-110">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="32f67-111">命令</span><span class="sxs-lookup"><span data-stu-id="32f67-111">Command</span></span>                                                                                                             | <span data-ttu-id="32f67-112">注意事項</span><span class="sxs-lookup"><span data-stu-id="32f67-112">Notes</span></span>                                                                                                                                                                                |
|---------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [<span data-ttu-id="32f67-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="32f67-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup)                           | <span data-ttu-id="32f67-114">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="32f67-114">Creates a resource group in which all resources are stored.</span></span>                                                                                                                          |
| [<span data-ttu-id="32f67-115">New-AzureRmStorageAccount</span><span class="sxs-lookup"><span data-stu-id="32f67-115">New-AzureRmStorageAccount</span></span>](/powershell/module/azurerm.resources/new-azurermstorageaccount)                         | <span data-ttu-id="32f67-116">建立儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="32f67-116">Creates a storage account.</span></span>                                                                                                                                                           |
| [<span data-ttu-id="32f67-117">Add-AzureRmVhd</span><span class="sxs-lookup"><span data-stu-id="32f67-117">Add-AzureRmVhd</span></span>](/powershell/module/azurerm.resources/add-azurermvhd)                                               | <span data-ttu-id="32f67-118">將虛擬硬碟從內部部署虛擬機器上傳至 Azure 雲端儲存體帳戶中的 Blob。</span><span class="sxs-lookup"><span data-stu-id="32f67-118">Uploads a virtual hard disk from an on-premises virtual machine to a blob in a cloud storage account in Azure.</span></span>                                                                       |
| [<span data-ttu-id="32f67-119">New-AzureRmImageConfig</span><span class="sxs-lookup"><span data-stu-id="32f67-119">New-AzureRmImageConfig</span></span>](/powershell/module/azurerm.resources/new-azurermimageconfig)                               | <span data-ttu-id="32f67-120">建立可設定的映像物件。</span><span class="sxs-lookup"><span data-stu-id="32f67-120">Creates a configurable image object.</span></span>                                                                                                                                                 |
| [<span data-ttu-id="32f67-121">Set-AzureRmImageOsDisk</span><span class="sxs-lookup"><span data-stu-id="32f67-121">Set-AzureRmImageOsDisk</span></span>](/powershell/module/azurerm.resources/set-azurermimageosdisk)                               | <span data-ttu-id="32f67-122">設定映像物件上的作業系統磁碟屬性。</span><span class="sxs-lookup"><span data-stu-id="32f67-122">Sets the operating system disk properties on an image object.</span></span>                                                                                                                        |
| [<span data-ttu-id="32f67-123">New-AzureRmImage</span><span class="sxs-lookup"><span data-stu-id="32f67-123">New-AzureRmImage</span></span>](/powershell/module/azurerm.resources/new-azurermimage)                                           | <span data-ttu-id="32f67-124">建立新的映像。</span><span class="sxs-lookup"><span data-stu-id="32f67-124">Creates a new image.</span></span>                                                                                                                                                                 |
| [<span data-ttu-id="32f67-125">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="32f67-125">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.resources/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="32f67-126">建立子網路組態。</span><span class="sxs-lookup"><span data-stu-id="32f67-126">Creates a subnet configuration.</span></span> <span data-ttu-id="32f67-127">此組態可使用於虛擬網路建立程序。</span><span class="sxs-lookup"><span data-stu-id="32f67-127">This configuration is used with the virtual network creation process.</span></span>                                                                                |
| [<span data-ttu-id="32f67-128">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="32f67-128">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.resources/new-azurermvirtualnetwork)                         | <span data-ttu-id="32f67-129">建立虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="32f67-129">Creates a virtual network.</span></span>                                                                                                                                                           |
| [<span data-ttu-id="32f67-130">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="32f67-130">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.resources/new-azurermpublicipaddress)                       | <span data-ttu-id="32f67-131">建立公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="32f67-131">Creates a public IP address.</span></span>                                                                                                                                                         |
| [<span data-ttu-id="32f67-132">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="32f67-132">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.resources/new-azurermnetworkinterface)                     | <span data-ttu-id="32f67-133">建立網路介面。</span><span class="sxs-lookup"><span data-stu-id="32f67-133">Creates a network interface.</span></span>                                                                                                                                                         |
| [<span data-ttu-id="32f67-134">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="32f67-134">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.resources/new-azurermnetworksecurityruleconfig)   | <span data-ttu-id="32f67-135">建立網路安全性群組規則組態。</span><span class="sxs-lookup"><span data-stu-id="32f67-135">Creates a network security group rule configuration.</span></span> <span data-ttu-id="32f67-136">建立 NSG 時，此組態用來建立 NSG 規則。</span><span class="sxs-lookup"><span data-stu-id="32f67-136">This configuration is used to create an NSG rule when the NSG is created.</span></span>                                                       |
| [<span data-ttu-id="32f67-137">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="32f67-137">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.resources/new-azurermnetworksecuritygroup)             | <span data-ttu-id="32f67-138">建立網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="32f67-138">Creates a network security group.</span></span>                                                                                                                                                    |
| [<span data-ttu-id="32f67-139">Get-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="32f67-139">Get-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.resources/get-azurermvirtualnetwork)                         | <span data-ttu-id="32f67-140">取得資源群組中的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="32f67-140">Gets a virtual network in a resource group.</span></span>                                                                                                                                          |
| [<span data-ttu-id="32f67-141">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="32f67-141">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.resources/new-azurermvmconfig)                                     | <span data-ttu-id="32f67-142">建立 VM 組態。</span><span class="sxs-lookup"><span data-stu-id="32f67-142">Creates a VM configuration.</span></span> <span data-ttu-id="32f67-143">此組態包括 VM 名稱、作業系統和系統管理認證等資訊。</span><span class="sxs-lookup"><span data-stu-id="32f67-143">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="32f67-144">建立 VM 時會使用此組態。</span><span class="sxs-lookup"><span data-stu-id="32f67-144">The configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="32f67-145">Set-AzureRmVMSourceImage</span><span class="sxs-lookup"><span data-stu-id="32f67-145">Set-AzureRmVMSourceImage</span></span>](/powershell/module/azurerm.resources/set-azurermvmsourceimage)                           | <span data-ttu-id="32f67-146">指定虛擬機器的映像。</span><span class="sxs-lookup"><span data-stu-id="32f67-146">Specifies an image for a virtual machine.</span></span>                                                                                                                                            |
| [<span data-ttu-id="32f67-147">Set-AzureRmVMOSDisk</span><span class="sxs-lookup"><span data-stu-id="32f67-147">Set-AzureRmVMOSDisk</span></span>](/powershell/module/azurerm.resources/set-azurermvmosdisk)                                     | <span data-ttu-id="32f67-148">設定虛擬機器上的作業系統磁碟屬性。</span><span class="sxs-lookup"><span data-stu-id="32f67-148">Sets the operating system disk properties on a virtual machine.</span></span>                                                                                                                      |
| [<span data-ttu-id="32f67-149">Set-AzureRmVMOperatingSystem</span><span class="sxs-lookup"><span data-stu-id="32f67-149">Set-AzureRmVMOperatingSystem</span></span>](/powershell/module/azurerm.resources/set-azurermvmoperatingsystem)                   | <span data-ttu-id="32f67-150">設定虛擬機器上的作業系統磁碟屬性。</span><span class="sxs-lookup"><span data-stu-id="32f67-150">Sets the operating system disk properties on a virtual machine.</span></span>                                                                                                                      |
| [<span data-ttu-id="32f67-151">Add-AzureRmVMNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="32f67-151">Add-AzureRmVMNetworkInterface</span></span>](/powershell/module/azurerm.resources/add-azurermvmnetworkinterface)                 | <span data-ttu-id="32f67-152">將網路介面新增至虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="32f67-152">Adds a network interface to a virtual machine.</span></span>                                                                                                                                       |
| [<span data-ttu-id="32f67-153">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="32f67-153">New-AzureRmVM</span></span>](/powershell/module/azurerm.resources/new-azurermvm)                                                 | <span data-ttu-id="32f67-154">建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="32f67-154">Create a virtual machine.</span></span>                                                                                                                                                            |
| [<span data-ttu-id="32f67-155">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="32f67-155">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup)                     | <span data-ttu-id="32f67-156">移除資源群組及其內含的所有資源。</span><span class="sxs-lookup"><span data-stu-id="32f67-156">Removes a resource group and all resources contained within.</span></span>                                                                                                                         |

## <a name="next-steps"></a><span data-ttu-id="32f67-157">後續步驟</span><span class="sxs-lookup"><span data-stu-id="32f67-157">Next steps</span></span>

<span data-ttu-id="32f67-158">如需有關 Azure PowerShell 模組的詳細資訊，請參閱 [Azure PowerShell 文件](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="32f67-158">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="32f67-159">您可以在 [Azure Windows VM 文件](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)中找到其他的虛擬機器 PowerShell 指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="32f67-159">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
