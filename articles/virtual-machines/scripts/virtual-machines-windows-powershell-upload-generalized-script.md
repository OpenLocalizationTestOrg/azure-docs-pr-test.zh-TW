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
# <a name="sample-script-tooupload-a-vhd-tooazure-and-create-a-new-vm"></a>範例指令碼 tooupload VHD tooAzure 並建立新的 VM

此指令碼會將本機的.vhd 檔從一般化 VM 和 tooAzure 上傳、 建立受管理的磁碟映像和使用 hello toocreate 新的 VM。

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>範例指令碼

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

## <a name="clean-up-deployment"></a>清除部署 

執行下列命令 tooremove hello 資源群組、 VM 和所有相關的資源的 hello。

```powershell
Remove-AzureRmResourceGroup -Name $resourceGroup
```

## <a name="script-explanation"></a>指令碼說明

此指令碼會使用下列命令 toocreate hello 部署的 hello。 Hello 資料表中的每個項目連結 toocommand 特定文件。

| 命令                                                                                                             | 注意事項                                                                                                                                                                                |
|---------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup)                           | 建立用來存放所有資源的資源群組。                                                                                                                          |
| [New-AzureRmStorageAccount](/powershell/module/azurerm.resources/new-azurermstorageaccount)                         | 建立儲存體帳戶。                                                                                                                                                           |
| [Add-AzureRmVhd](/powershell/module/azurerm.resources/add-azurermvhd)                                               | 上傳從內部部署虛擬機器 tooa blob 在 Azure 中的雲端儲存體帳戶中的虛擬硬碟。                                                                       |
| [New-AzureRmImageConfig](/powershell/module/azurerm.resources/new-azurermimageconfig)                               | 建立可設定的映像物件。                                                                                                                                                 |
| [Set-AzureRmImageOsDisk](/powershell/module/azurerm.resources/set-azurermimageosdisk)                               | 映像物件上設定 hello 作業系統磁碟屬性。                                                                                                                        |
| [New-AzureRmImage](/powershell/module/azurerm.resources/new-azurermimage)                                           | 建立新的映像。                                                                                                                                                                 |
| [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.resources/new-azurermvirtualnetworksubnetconfig) | 建立子網路組態。 此設定可搭配 hello 虛擬網路建立程序。                                                                                |
| [New-AzureRmVirtualNetwork](/powershell/module/azurerm.resources/new-azurermvirtualnetwork)                         | 建立虛擬網路。                                                                                                                                                           |
| [New-AzureRmPublicIpAddress](/powershell/module/azurerm.resources/new-azurermpublicipaddress)                       | 建立公用 IP 位址。                                                                                                                                                         |
| [New-AzureRmNetworkInterface](/powershell/module/azurerm.resources/new-azurermnetworkinterface)                     | 建立網路介面。                                                                                                                                                         |
| [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.resources/new-azurermnetworksecurityruleconfig)   | 建立網路安全性群組規則組態。 此設定時，使用的 toocreate NSG 規則建立 hello NSG。                                                       |
| [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.resources/new-azurermnetworksecuritygroup)             | 建立網路安全性群組。                                                                                                                                                    |
| [Get-AzureRmVirtualNetwork](/powershell/module/azurerm.resources/get-azurermvirtualnetwork)                         | 取得資源群組中的虛擬網路。                                                                                                                                          |
| [New-AzureRmVMConfig](/powershell/module/azurerm.resources/new-azurermvmconfig)                                     | 建立 VM 組態。 此組態包括 VM 名稱、作業系統和系統管理認證等資訊。 在建立 VM 時，會使用 hello 組態。 |
| [Set-AzureRmVMSourceImage](/powershell/module/azurerm.resources/set-azurermvmsourceimage)                           | 指定虛擬機器的映像。                                                                                                                                            |
| [Set-AzureRmVMOSDisk](/powershell/module/azurerm.resources/set-azurermvmosdisk)                                     | 虛擬機器上設定 hello 作業系統磁碟屬性。                                                                                                                      |
| [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.resources/set-azurermvmoperatingsystem)                   | 虛擬機器上設定 hello 作業系統磁碟屬性。                                                                                                                      |
| [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.resources/add-azurermvmnetworkinterface)                 | 新增網路介面 tooa 虛擬機器。                                                                                                                                       |
| [New-AzureRmVM](/powershell/module/azurerm.resources/new-azurermvm)                                                 | 建立虛擬機器。                                                                                                                                                            |
| [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup)                     | 移除資源群組及其內含的所有資源。                                                                                                                         |

## <a name="next-steps"></a>後續步驟

如需有關 hello Azure PowerShell 模組的詳細資訊，請參閱[Azure PowerShell 文件](/powershell/azure/overview)。

其他虛擬機器的 PowerShell 指令碼範例可以在 hello [Azure Windows VM 文件](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。
