---
title: "aaaCommon PowerShell 命令適用於 Azure 虛擬機器 |Microsoft 文件"
description: "常見的 PowerShell 命令 tooget 您開始建立及管理 Windows Azure 中的 Vm。"
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: ba3839a2-f3d5-4e19-a5de-95bfb1c0e61e
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/17/2017
ms.author: davidmu
ms.openlocfilehash: 3de9bd4d20259ced2c0aa8ef7a3f7d9520a071d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="common-powershell-commands-for-creating-and-managing-azure-virtual-machines"></a>用於建立及管理 Azure 虛擬機器的常用 PowerShell 命令

本文涵蓋一些 hello Azure PowerShell 命令，您可以使用 toocreate 並管理您的 Azure 訂用帳戶中的虛擬機器。  如需特定命令列參數和選項的詳細說明，您可以使用 **Get-Help** *命令*。

請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)如需有關安裝 hello 最新版本的 Azure PowerShell 中，選取您的訂閱，並登入 tooyour 帳戶資訊。

如果一個以上的 hello 命令執行本文中，這些變數可能會有助您：

- $location-hello hello 虛擬機器的位置。 您可以使用[Get AzureRmLocation](https://docs.microsoft.com/powershell/module/azurerm.resources/get-azurermlocation) toofind[地理區域](https://azure.microsoft.com/regions/)適合您。
- $myResourceGroup-hello hello 包含 hello 虛擬機器的資源群組名稱。
- $myVM-hello hello 虛擬機器名稱。

## <a name="create-a-vm"></a>建立 VM

| Task | 命令 |
| ---- | ------- |
| 建立 VM 組態 |$vm = [New-AzureRmVMConfig](https://docs.microsoft.com/powershell/module/azurerm.compute/new-azurermvmconfig) -VMName $myVM -VMSize "Standard_D1_v1"<BR></BR><BR></BR>hello VM 組態是使用的 toodefine 或更新的設定 hello VM。 hello 組態初始化 hello hello VM 名稱及其[大小](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。 |
| 新增組態設定 |$vm = [Set-AzureRmVMOperatingSystem](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) -VM $vm -Windows -ComputerName $myVM -Credential $cred -ProvisionVMAgent -EnableAutoUpdate<BR></BR><BR></BR>作業系統設定包括[認證](https://technet.microsoft.com/library/hh849815.aspx)會加入您先前建立使用新 AzureRmVMConfig toohello 組態物件。 |
| 新增網路介面 |$vm = [Add-AzureRmVMNetworkInterface](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.5.0/Add-AzureRmVMNetworkInterface) -VM $vm -Id $nic.Id<BR></BR><BR></BR>VM 必須有[網路介面](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)toocommunicate 虛擬網路中的。 您也可以使用[Get AzureRmNetworkInterface](https://docs.microsoft.com/powershell/module/azurerm.compute/add-azurermvmnetworkinterface) tooretrieve 現有的網路介面物件。 |
| 指定平台映像 |$vm = [Set-AzureRmVMSourceImage](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmsourceimage) -VM $vm -PublisherName "publisher_name" -Offer "publisher_offer" -Skus "product_sku" -Version "latest"<BR></BR><BR></BR>[影像資訊](cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)會加入您先前建立使用新 AzureRmVMConfig toohello 組態物件。 當您設定 hello OS 磁碟 toouse 平台映像時，只會用於 hello 從此命令傳回的物件。 |
| 設定作業系統磁碟 toouse 平台映像 |$vm = [Set-AzureRmVMOSDisk](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmosdisk) -VM $vm -Name "myOSDisk" -VhdUri "http://mystore1.blob.core.windows.net/vhds/myOSDisk.vhd" -CreateOption FromImage<BR></BR><BR></BR>hello 作業系統磁碟和它的位置中的 hello 名稱[儲存體](../../storage/common/storage-powershell-guide-full.md)加入 toohello 您先前建立的組態物件。 |
| 設定作業系統磁碟 toouse 一般化映像 |$vm = Set-AzureRmVMOSDisk -VM $vm -Name "myOSDisk" -SourceImageUri "https://mystore1.blob.core.windows.net/system/Microsoft.Compute/Images/myimages/myprefix-osDisk.{guid}.vhd" -VhdUri "https://mystore1.blob.core.windows.net/vhds/disk_name.vhd" -CreateOption FromImage -Windows<BR></BR><BR></BR>hello 名稱 hello 作業系統磁碟、 hello 位置 hello 來源映像，以及在 hello 磁碟位置[儲存體](../../storage/common/storage-powershell-guide-full.md)加入 toohello 組態物件。 |
| 設定作業系統磁碟 toouse 特製化映像 |$vm = Set-AzureRmVMOSDisk -VM $vm -Name "myOSDisk" -VhdUri "http://mystore1.blob.core.windows.net/vhds/" -CreateOption Attach -Windows |
| 建立 VM |[New-AzureRmVM]() -ResourceGroupName $myResourceGroup -Location $location -VM $vm<BR></BR><BR></BR>所有資源都會在[資源群組](../../azure-resource-manager/powershell-azure-resource-manager.md)中建立。 執行此命令之前，請執行 New-AzureRmVMConfig、Set-AzureRmVMOperatingSystem、Set-AzureRmVMSourceImage、Add-AzureRmVMNetworkInterface 和 Set-AzureRmVMOSDisk。 |

## <a name="get-information-about-vms"></a>取得 VM 的相關資訊

| Task | 命令 |
| ---- | ------- |
| 列出訂用帳戶中的 VM |[Get-AzureRmVM](https://docs.microsoft.com/powershell/module/azurerm.compute/get-azurermvm) |
| 列出資源群組中的 VM |Get-AzureRmVM -ResourceGroupName $myResourceGroup<BR></BR><BR></BR>您的訂用帳戶中的 tooget 一份資源群組，請使用[Get AzureRmResourceGroup](https://docs.microsoft.com/powershell/module/azurerm.resources/get-azurermresourcegroup)。 |
| 取得 VM 的相關資訊 |Get-AzureRmVM -ResourceGroupName $myResourceGroup -Name $myVM |

## <a name="manage-vms"></a>管理 VM
| Task | 命令 |
| --- | --- |
| 啟動 VM |[Start-AzureRmVM](https://docs.microsoft.com/powershell/module/azurerm.compute/start-azurermvm) -ResourceGroupName $myResourceGroup -Name $myVM |
| 停止 VM |[Stop-AzureRmVM](https://docs.microsoft.com/powershell/module/azurerm.compute/stop-azurermvm) -ResourceGroupName $myResourceGroup -Name $myVM |
| 重新啟動執行中的 VM |[Restart-AzureRmVM](https://docs.microsoft.com/powershell/module/azurerm.compute/restart-azurermvm) -ResourceGroupName $myResourceGroup -Name $myVM |
| 刪除 VM |[Remove-AzureRmVM](https://docs.microsoft.com/powershell/module/azurerm.compute/remove-azurermvm) -ResourceGroupName $myResourceGroup -Name $myVM |
| 一般化 VM |[Set-AzureRmVm](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvm) -ResourceGroupName $myResourceGroup -Name $myVM -Generalized<BR></BR><BR></BR>您在執行 Save-AzureRmVMImage 前需執行此命令。 |
| 擷取 VM |[Save-AzureRmVMImage](https://docs.microsoft.com/powershell/module/azurerm.compute/save-azurermvmimage) -ResourceGroupName $myResourceGroup -VMName $myVM -DestinationContainerName "myImageContainer" -VHDNamePrefix "myImagePrefix" -Path "C:\filepath\filename.json"<BR></BR><BR></BR>虛擬機器必須[準備、 關閉和一般化](prepare-for-upload-vhd-image.md)toobe 用 toocreate 映像。 請在執行此命令前，執行 Set-AzureRmVm。 |
| 更新 VM |[Update-AzureRmVM](https://docs.microsoft.com/powershell/module/azurerm.compute/update-azurermvm) -ResourceGroupName $myResourceGroup -VM $vm<BR></BR><BR></BR>取得使用 Get AzureRmVM hello 目前 VM 組態設定，變更組態設定，在 hello VM 物件，然後再執行此命令。 |
| 新增資料磁碟 tooa VM |[Add-AzureRmVMDataDisk](https://docs.microsoft.com/powershell/module/azurerm.compute/add-azurermvmdatadisk) -VM $vm -Name "myDataDisk" -VhdUri "https://mystore1.blob.core.windows.net/vhds/myDataDisk.vhd" -LUN # -Caching ReadWrite -DiskSizeinGB # -CreateOption Empty<BR></BR><BR></BR>使用 Get AzureRmVM tooget hello VM 物件。 指定 hello 的 LUN 編號和 hello hello 磁碟大小。 執行更新 AzureRmVM tooapply hello 組態變更 toohello VM。 您新增的 hello 磁碟未初始化。 |
| 從 VM 移除資料磁碟 |[Remove-AzureRmVMDataDisk](https://docs.microsoft.com/powershell/module/azurerm.compute/remove-azurermvmdatadisk) -VM $vm -Name "myDataDisk"<BR></BR><BR></BR>使用 Get AzureRmVM tooget hello VM 物件。 執行更新 AzureRmVM tooapply hello 組態變更 toohello VM。 |
| 新增延伸模組 tooa VM |[Set-AzureRmVMExtension](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmextension) -ResourceGroupName $myResourceGroup -Location $location -VMName $myVM -Name "extensionName" -Publisher "publisherName" -Type "extensionType" -TypeHandlerVersion "#.#" -Settings $Settings -ProtectedSettings $ProtectedSettings<BR></BR><BR></BR>執行此命令，以適當的 hello[組態資訊](template-description.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json#extensions)想 tooinstall hello 延伸模組。 |
| 移除 VM 延伸模組 |[Remove-AzureRmVMExtension](https://docs.microsoft.com/powershell/module/azurerm.compute/remove-azurermvmextension) -ResourceGroupName $myResourceGroup -Name "extensionName" -VMName $myVM |

## <a name="next-steps"></a>後續步驟
* 請參閱 hello 建立虛擬機器中的基本步驟[建立使用資源管理員和 PowerShell 的 Windows VM](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。

