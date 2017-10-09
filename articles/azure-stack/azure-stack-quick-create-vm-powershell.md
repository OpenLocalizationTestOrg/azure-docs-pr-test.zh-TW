---
title: "aaaCreate Azure 堆疊中使用 PowerShell 的 Windows 虛擬機器 |Microsoft 文件"
description: "在 Azure Stack 中使用 PowerShell 建立 Windows 虛擬機器。"
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: sngun
ms.openlocfilehash: de063eae6f0782d8916da991f285a9de6b41def4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-virtual-machine-by-using-powershell-in-azure-stack"></a>在 Azure Stack 中使用 PowerShell 建立 Windows 虛擬機器

您不需要 toobuy hello 的虛擬化彈性和維護 Azure 堆疊提供中的虛擬機器 hello 實體硬體執行它。 當您使用虛擬機器時，了解有可用在 Azure 中的 hello 功能和 Azure 堆疊之間的一些差異，請參閱 toohello [Azure 堆疊中的虛擬機器的考量](azure-stack-vm-considerations.md)相關的主題 toolearn這些差異。 

此 Windows Server 2016 中的虛擬機器 Azure 堆疊引導使用 PowerShell toocreate 詳細資料。 您可以執行從 hello Azure 堆疊開發套件，或是從 windows 的外部用戶端的這篇文章中所述，如果您透過 VPN 連線的 hello 步驟。 

## <a name="prerequisites"></a>必要條件

1. 根據預設，hello Azure 堆疊 marketplace 未包含 hello Windows Server 2016 映像。 因此，您可以建立虛擬機器之前，請確定該 hello Azure 堆疊運算子[新增 hello Windows Server 2016 映像 toohello Azure 堆疊 marketplace](azure-stack-add-default-image.md)。 
2. Azure 堆疊需要特定版本的 Azure PowerShell 模組 toocreate，並管理 hello 資源。 使用中所述的 hello 步驟[安裝 PowerShell Azure 堆疊以](azure-stack-powershell-install.md)主題 tooinstall hello 必要的版本。
3. [設定 hello Azure 堆疊使用者的 PowerShell 環境](azure-stack-powershell-configure-user.md) 

## <a name="create-a-resource-group"></a>建立資源群組

資源群組是在其中部署與管理 Azure Stack 資源的邏輯容器。 使用下列程式碼區塊 toocreate 資源群組的 hello。 我們已為此文件中的所有變數指派值，您可以使用它們或指派不同的值。  

```powershell
# Create variables toostore hello location and resource group names.
$location = "local"
$ResourceGroupName = "myResourceGroup"

New-AzureRmResourceGroup `
  -Name $ResourceGroupName `
  -Location $location
```

## <a name="create-storage-resources"></a>建立儲存體資源 

建立儲存體帳戶和儲存體容器 toostore hello Windows Server 2016 映像。

```powershell
# Create variables toostore hello storage account name and hello storage account SKU information
$StorageAccountName = "mystorageaccount"
$SkuName = "Standard_LRS"

# Create a new storage account
$StorageAccount = New-AzureRMStorageAccount `
  -Location $location `
  -ResourceGroupName $ResourceGroupName `
  -Type $SkuName `
  -Name $StorageAccountName

Set-AzureRmCurrentStorageAccount `
  -StorageAccountName $storageAccountName `
  -ResourceGroupName $resourceGroupName

# Create a storage container toostore hello virtual machine image
$containerName = 'osdisks'
$container = New-AzureStorageContainer `
  -Name $containerName `
  -Permission Blob
```

## <a name="create-networking-resources"></a>建立網路資源

建立虛擬網路、子網路和公用 IP 位址。 這些資源是使用的 tooprovide 網路連線 toohello 虛擬機器。  

```powershell
# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
  -Name mySubnet `
  -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName $ResourceGroupName `
  -Location $location `
  -Name MyVnet `
  -AddressPrefix 192.168.0.0/16 `
  -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$pip = New-AzureRmPublicIpAddress `
  -ResourceGroupName $ResourceGroupName `
  -Location $location `
  -AllocationMethod Static `
  -IdleTimeoutInMinutes 4 `
  -Name "mypublicdns$(Get-Random)"
```

### <a name="create-a-network-security-group-and-a-network-security-group-rule"></a>建立網路安全性群組和網路安全性群組規則

hello 網路安全性小組會使用輸入和輸出規則，以保護 hello 虛擬機器。 可讓建立輸入的規則的連接埠 3389 tooallow 連入遠端桌面連線和通訊埠 80 tooallow 傳入的 web 流量的輸入的規則。

```powershell
# Create an inbound network security group rule for port 3389
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

# Create an inbound network security group rule for port 80
$nsgRuleWeb = New-AzureRmNetworkSecurityRuleConfig `
  -Name myNetworkSecurityGroupRuleWWW `
  -Protocol Tcp `
  -Direction Inbound `
  -Priority 1001 `
  -SourceAddressPrefix * `
  -SourcePortRange * `
  -DestinationAddressPrefix * `
  -DestinationPortRange 80 `
  -Access Allow

# Create a network security group
$nsg = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName $ResourceGroupName `
  -Location $location `
  -Name myNetworkSecurityGroup `
  -SecurityRules $nsgRuleRDP,$nsgRuleWeb 
```
 
### <a name="create-a-network-card-for-hello-virtual-machine"></a>建立 hello 虛擬機器的網路卡

hello 網路卡會連接 hello 虛擬機器 tooa 子網路、 網路安全性群組和公用 IP 位址。

```powershell
# Create a virtual network card and associate it with public IP address and NSG
$nic = New-AzureRmNetworkInterface `
  -Name myNic `
  -ResourceGroupName $ResourceGroupName `
  -Location $location `
  -SubnetId $vnet.Subnets[0].Id `
  -PublicIpAddressId $pip.Id `
  -NetworkSecurityGroupId $nsg.Id 
```

## <a name="create-a-virtual-machine"></a>建立虛擬機器

建立虛擬機器組態。 hello 設定包含部署 hello 在虛擬機器的虛擬機器映像、 大小、 認證時所使用的 hello 設定。

```powershell
# Define a credential object toostore hello username and password for hello virtual machine
$UserName='demouser'
$Password='Password@123'| ConvertTo-SecureString -Force -AsPlainText
$Credential=New-Object PSCredential($UserName,$Password)

# Create hello virtual machine configuration object
$VmName = "VirtualMachinelatest"
$VmSize = "Standard_A1"
$VirtualMachine = New-AzureRmVMConfig `
  -VMName $VmName `
  -VMSize $VmSize 

$VirtualMachine = Set-AzureRmVMOperatingSystem `
  -VM $VirtualMachine `
  -Windows `
  -ComputerName "MainComputer" `
  -Credential $Credential 

$VirtualMachine = Set-AzureRmVMSourceImage `
  -VM $VirtualMachine `
  -PublisherName "MicrosoftWindowsServer" `
  -Offer "WindowsServer" `
  -Skus "2016-Datacenter" `
  -Version "latest"

$osDiskName = "OsDisk"
$osDiskUri = '{0}vhds/{1}-{2}.vhd' -f `
  $StorageAccount.PrimaryEndpoints.Blob.ToString(),`
  $vmName.ToLower(), `
  $osDiskName

# Sets hello operating system disk properties on a virtual machine. 
$VirtualMachine = Set-AzureRmVMOSDisk `
  -VM $VirtualMachine `
  -Name $osDiskName `
  -VhdUri $OsDiskUri `
  -CreateOption FromImage | `
  Add-AzureRmVMNetworkInterface -Id $nic.Id 

#Create hello virtual machine.
New-AzureRmVM `
  -ResourceGroupName $ResourceGroupName `
  -Location $location `
  -VM $VirtualMachine
```

## <a name="connect-toohello-virtual-machine"></a>Toohello 虛擬機器連線

已成功建立 hello 的虛擬機器之後，開啟遠端桌面連線 toohello 虛擬機器從 hello 開發套件，或從 windows 的外部用戶端如果透過 VPN 連線。 tooremote hello hello 先前步驟中所建立的虛擬機器，您需要其公用 IP 位址。 執行下列命令 tooget hello 公用 IP 位址的 hello 虛擬機器的 hello: 

```powershell
Get-AzureRmPublicIpAddress `
  -ResourceGroupName $ResourceGroupName | Select IpAddress
```
 
使用 hello 下列命令 toocreate 與 hello 虛擬機器的遠端桌面工作階段。 取代虛擬機器的 hello publicIPAddress hello IP 位址。 出現提示時，輸入 hello 使用者名稱和您建立 hello 虛擬機器時使用的密碼。

```powershell
mstsc /v:<publicIpAddress>
```
## <a name="delete-hello-virtual-machine"></a>刪除 hello 虛擬機器

當不再需要請使用下列命令 tooremove hello 資源群組含有 hello 虛擬機器和其相關的資源的 hello:

```powershell
Remove-AzureRmResourceGroup `
  -Name $ResourceGroupName
```

## <a name="next-steps"></a>後續步驟

關於 Azure 堆疊中的儲存體 toolearn 參考 toohello[存放裝置總覽](azure-stack-storage-overview.md)主題。

