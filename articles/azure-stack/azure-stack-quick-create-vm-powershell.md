---
title: "在 Azure Stack 中使用 PowerShell 建立 Windows 虛擬機器 | Microsoft Docs"
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
ms.openlocfilehash: 4b6706b289e323706009c40e9d1ad0149f8accc5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-windows-virtual-machine-by-using-powershell-in-azure-stack"></a>在 Azure Stack 中使用 PowerShell 建立 Windows 虛擬機器

Azure Stack 中的虛擬機器讓您能夠有彈性地進行虛擬化，而不需購買並維護執行虛擬機器的實體硬體。 當您使用虛擬機器時，請了解 Azure 和 Azure Stack 中所提供的功能之間具有某些差異，請參閱[Azure Stack 中虛擬機器的考量](azure-stack-vm-considerations.md)主題以了解這些差異。 

本指南詳細說明如何使用 PowerShell 在 Azure Stack 中建立 Windows Server 2016 虛擬機器。 您可以從 Azure Stack 開發套件，或從以 Windows 為基礎的外部用戶端 (如果您透過 VPN 連線) 來執行這篇文章中所述的步驟。 

## <a name="prerequisites"></a>必要條件

1. 依預設，Azure Stack 市集不包含 Windows Server 2016 映像。 因此，在您可以建立虛擬機器之前，請確定 Azure Stack 操作員[將 Windows Server 2016 映像新增至 Azure Stack 市集](azure-stack-add-default-image.md)。 
2. Azure Stack 需要特定版本的 Azure PowerShell 模組才能建立和管理資源。 請使用[安裝 Azure Stack 的 PowerShell](azure-stack-powershell-install.md) 主題中所述的步驟來安裝需要的版本。
3. [設定 Azure Stack 使用者的 PowerShell 環境](azure-stack-powershell-configure-user.md) 

## <a name="create-a-resource-group"></a>建立資源群組

資源群組是在其中部署與管理 Azure Stack 資源的邏輯容器。 請使用下列程式碼區塊來建立資源群組。 我們已為此文件中的所有變數指派值，您可以使用它們或指派不同的值。  

```powershell
# Create variables to store the location and resource group names.
$location = "local"
$ResourceGroupName = "myResourceGroup"

New-AzureRmResourceGroup `
  -Name $ResourceGroupName `
  -Location $location
```

## <a name="create-storage-resources"></a>建立儲存體資源 

建立儲存體帳戶和儲存體容器來儲存 Windows Server 2016 映像。

```powershell
# Create variables to store the storage account name and the storage account SKU information
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

# Create a storage container to store the virtual machine image
$containerName = 'osdisks'
$container = New-AzureStorageContainer `
  -Name $containerName `
  -Permission Blob
```

## <a name="create-networking-resources"></a>建立網路資源

建立虛擬網路、子網路和公用 IP 位址。 這些資源用來提供虛擬機器的網路連線能力。  

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

網路安全性群組可透過使用輸入和輸出規則來保護虛擬機器。 讓我們建立連接埠 3389 的輸入規則以允許傳入的遠端桌面連線，並建立連接埠 80 的輸入規則以允許傳入的 Web 流量。

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
 
### <a name="create-a-network-card-for-the-virtual-machine"></a>建立虛擬機器的網路卡

網路卡可讓虛擬機器連線到子網路、網路安全性群組和公用 IP 位址。

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

建立虛擬機器組態。 此組態包括部署虛擬機器時所使用的設定，例如虛擬機器映像、大小和認證。

```powershell
# Define a credential object to store the username and password for the virtual machine
$UserName='demouser'
$Password='Password@123'| ConvertTo-SecureString -Force -AsPlainText
$Credential=New-Object PSCredential($UserName,$Password)

# Create the virtual machine configuration object
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

# Sets the operating system disk properties on a virtual machine. 
$VirtualMachine = Set-AzureRmVMOSDisk `
  -VM $VirtualMachine `
  -Name $osDiskName `
  -VhdUri $OsDiskUri `
  -CreateOption FromImage | `
  Add-AzureRmVMNetworkInterface -Id $nic.Id 

#Create the virtual machine.
New-AzureRmVM `
  -ResourceGroupName $ResourceGroupName `
  -Location $location `
  -VM $VirtualMachine
```

## <a name="connect-to-the-virtual-machine"></a>連接至虛擬機器

成功建立虛擬機器之後，從開發套件，或從以 Windows 為基礎的外部用戶端 (如果透過 VPN 連線) 來開啟虛擬機器的遠端桌面連線。 若要遠端存取您在上一個步驟中所建立的虛擬機器，則需要其公用 IP 位址。 執行下列命令，以取得虛擬機器的公用 IP 位址： 

```powershell
Get-AzureRmPublicIpAddress `
  -ResourceGroupName $ResourceGroupName | Select IpAddress
```
 
使用下列命令，建立使用虛擬機器的遠端桌面工作階段。 以虛擬機器的公用 IP 位址取代 IP 位址。 出現提示時，輸入您在建立虛擬機器時所使用的使用者名稱和密碼。

```powershell
mstsc /v:<publicIpAddress>
```
## <a name="delete-the-virtual-machine"></a>刪除虛擬機器

當不再需要時，請使用下列命令來移除包含虛擬機器及其相關資源的資源群組：

```powershell
Remove-AzureRmResourceGroup `
  -Name $ResourceGroupName
```

## <a name="next-steps"></a>後續步驟

若要了解 Azure Stack 中的儲存體，請參閱[儲存體概觀](azure-stack-storage-overview.md)主題。

