---
title: "aaaCreate 自訂 VM 映像以 hello Azure PowerShell |Microsoft 文件"
description: "教學課程-建立自訂 VM 映像使用 hello Azure PowerShell。"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/08/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 3a759fe1b7e7b72f531399b0f4a99e341713c6a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-of-an-azure-vm-using-powershell"></a>使用 PowerShell 建立 Azure VM 的自訂映像

自訂映像類似 Marketplace 映像，但您要自行建立它們。 自訂映像可以使用的 toobootstrap 組態，例如預先載入應用程式、 應用程式設定和其他作業系統設定。 在本教學課程中，您將建立自己的 Azure 虛擬機器自訂映像。 您會了解如何：

> [!div class="checklist"]
> * 執行 sysprep 及一般化 VM
> * 建立自訂映像
> * 從自訂映像建立 VM
> * 列出您的訂用帳戶中的所有 hello 映像
> * 删除映像

本教學課程需要 hello Azure PowerShell 模組版本 3.6 版或更新版本。 執行` Get-Module -ListAvailable AzureRM`toofind hello 版本。 如果您需要 tooupgrade，請參閱[安裝 Azure PowerShell 模組](/powershell/azure/install-azurerm-ps)。

## <a name="before-you-begin"></a>開始之前

下列的 hello 步驟詳細說明 tootake 現有的 VM 並開啟它的可重複使用的自訂映像，您可以使用 toocreate 新 VM 執行個體。

在本教學課程 toocomplete hello 範例中的，您必須擁有現有的虛擬機器。 如有需要，這個[指令碼範例](../scripts/virtual-machines-windows-powershell-sample-create-vm.md)可以為您建立一部虛擬機器。 當工作透過 hello 教學課程中，取代 hello 資源群組和 VM 名稱在需要時。

## <a name="prepare-vm"></a>準備 VM

toocreate 虛擬機器的映像，您需要 tooprepare hello 一般化 hello VM 解除配置，，然後將標示 hello 來源為一般化 Azure 中 VM 的 VM。

### <a name="generalize-hello-windows-vm-using-sysprep"></a>一般化 hello Windows VM 使用 Sysprep

Sysprep 會移除所有您個人的帳戶資訊，以及其他項目，並準備作為映像的 hello 機器 toobe。 如需 Sysprep 的詳細資訊，請參閱[如何 tooUse Sysprep： 簡介](http://technet.microsoft.com/library/bb457073.aspx)。


1. Toohello 虛擬機器連線。
2. 系統管理員身分開啟 hello 命令提示字元視窗。 變更 hello 目錄太*%windir%\system32\sysprep*，然後執行*sysprep.exe*。
3. 在 hello**系統準備工具**對話方塊中，選取*進入系統的全新體驗 (OOBE)*，並確定該 hello*一般化*選取核取方塊。
4. 在 關機選項 中選取 關機，然後按一下確定。
5. Sysprep 完成時，它會關閉 hello 虛擬機器。 **請勿重新啟動 hello VM**。

### <a name="deallocate-and-mark-hello-vm-as-generalized"></a>解除配置，並將標示為一般化 VM hello

toocreate 映像，hello VM 需要 toobe 解除配置，而且標示為已在 Azure 中的一般化。

已取消配置的 hello VM 使用[停止 AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm)。

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroupImages -Name myVM -Force
```

設定得 hello hello 虛擬機器狀態`-Generalized`使用[組 AzureRmVm](/powershell/module/azurerm.compute/set-azurermvm)。 
   
```powershell
Set-AzureRmVM -ResourceGroupName myResourceGroupImages -Name myVM -Generalized
```


## <a name="create-hello-image"></a>建立 hello 映像

現在您可以使用，以建立 hello VM 的映像[新增 AzureRmImageConfig](/powershell/module/azurerm.compute/new-azurermimageconfig)和[新增 AzureRmImage](/powershell/module/azurerm.compute/new-azurermimage)。 hello 下列範例會建立名為映像*myImage*從名為 VM *myVM*。

取得 hello 虛擬機器。 

```powershell
$vm = Get-AzureRmVM -Name myVM -ResourceGroupName myResourceGroupImages
```

建立 hello 映像設定。

```powershell
$image = New-AzureRmImageConfig -Location EastUS -SourceVirtualMachineId $vm.ID 
```

建立 hello 映像。

```powershell
New-AzureRmImage -Image $image -ImageName myImage -ResourceGroupName myResourceGroupImages
``` 

 
## <a name="create-vms-from-hello-image"></a>從 hello 映像建立 Vm

既然您具有映像，您可以建立一或多個新的 Vm 從 hello 映像。 從自訂映像建立 VM 是非常類似 toocreating 使用 Marketplace 映像的 VM。 當您使用 Marketplace 映像時，您會有 tooinformation 有關 hello 映像、 映像提供者、 方案、 SKU 和版本。 使用自訂映像，您只需要 tooprovide hello hello 自訂映像資源 ID。 

在下列指令碼的 hello，我們會建立一個變數*$image* toostore 資訊 hello 自訂映像使用[Get AzureRmImage](/powershell/module/azurerm.compute/get-azurermimage) ，然後使用[組 AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage)，並指定使用 hello hello ID *$image*變數剛才所建立。 

hello 指令碼會建立名為的 VM *myVMfromImage*我們新的資源群組中的自訂映像從名為*myResourceGroupFromImage*在 hello*美國西部*位置。


```powershell
$cred = Get-Credential -Message "Enter a username and password for hello virtual machine."

New-AzureRmResourceGroup -Name myResourceGroupFromImage -Location EastUS

$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24

$vnet = New-AzureRmVirtualNetwork `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -Name MYvNET `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

$pip = New-AzureRmPublicIpAddress `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -Name "mypublicdns$(Get-Random)" `
    -AllocationMethod Static `
    -IdleTimeoutInMinutes 4

  $nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig `
    -Name myNetworkSecurityGroupRuleRDP `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1000 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 3389 `
    -Access Allow

  $nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRuleRDP

$nic = New-AzureRmNetworkInterface `
    -Name myNic `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -SubnetId $vnet.Subnets[0].Id `
    -PublicIpAddressId $pip.Id `
    -NetworkSecurityGroupId $nsg.Id

$vmConfig = New-AzureRmVMConfig `
    -VMName myVMfromImage `
    -VMSize Standard_D1 | Set-AzureRmVMOperatingSystem -Windows `
        -ComputerName myComputer `
        -Credential $cred 

# Here is where we create a variable toostore information about hello image 
$image = Get-AzureRmImage `
    -ImageName myImage `
    -ResourceGroupName myResourceGroupImages

# Here is where we specify that we want toocreate hello VM from and image and provide hello image ID
$vmConfig = Set-AzureRmVMSourceImage -VM $vmConfig -Id $image.Id

$vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id

New-AzureRmVM `
    -ResourceGroupName myResourceGroupFromImage `
    -Location EastUS `
    -VM $vmConfig
```

## <a name="image-management"></a>映像管理 

以下是一些常見的管理映像工作的範例以及 toocomplete 它們使用 PowerShell。

依名稱列出所有映像。

```powershell
$images = Find-AzureRMResource -ResourceType Microsoft.Compute/images 
$images.name
```

删除映像。 此範例中刪除 hello 名為映像*myOldImage*從 hello *myResourceGroup*。

```powershell
Remove-AzureRmImage `
    -ImageName myOldImage `
    -ResourceGroupName myResourceGroup
```

## <a name="next-steps"></a>後續步驟

您在本教學課程中建立了自訂 VM 映像。 您已了解如何︰

> [!div class="checklist"]
> * 執行 sysprep 及一般化 VM
> * 建立自訂映像
> * 從自訂映像建立 VM
> * 列出您的訂用帳戶中的所有 hello 映像
> * 删除映像

前進 toohello 下一個教學課程的 toolearn 關於如何高可用性虛擬機器。

> [!div class="nextstepaction"]
> [建立高可用性 VM](tutorial-availability-sets.md)



