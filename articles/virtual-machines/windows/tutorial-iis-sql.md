---
title: "在 Azure 中建立執行 SQL&#92;IIS&#92;.NET 堆疊的 VM | Microsoft Docs"
description: "教學課程 - 在 Windows 虛擬機器上安裝 Azure SQL、IIS、.NET 堆疊。"
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
ms.date: 10/24/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 6f7ef46d9c40138c211427845423783fefde5dc3
ms.sourcegitcommit: e5355615d11d69fc8d3101ca97067b3ebb3a45ef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/31/2017
---
# <a name="install-a-sql92iis92net-stack-in-azure"></a>在 Azure 中安裝 SQL&#92;IIS&#92;.NET 堆疊

在本教學課程中，我們會使用 Azure PowerShell 來安裝 SQL&#92;IIS&#92;.NET 堆疊。 此堆疊是由兩個執行 Windows Server 2016 的 VM 所組成，一個包含 IIS 和 .NET 而另一個則是包含 SQL Server。

> [!div class="checklist"]
> * 使用 New-AzVM 建立 VM
> * 在 VM 上安裝 IIS 和 .NET Core SDK
> * 建立執行 SQL Server 的 VM
> * 安裝 SQL Server 擴充功能



## <a name="create-a-iis-vm"></a>建立 IIS VM 

在此範例中，我們會使用 PowerShell Cloud Shell 中的 [New-AzVM](https://www.powershellgallery.com/packages/AzureRM.Compute.Experiments) Cmdlet 快速建立 Windows Server 2016 VM，然後再安裝 IIS 和 .NET Framework。 IIS 和 SQL VM 會共用資源群組和虛擬網路，因此我們要建立那些名稱的變數。

按一下程式碼區塊右上角的 [試試看] 按鈕，在此視窗中啟動 Cloud Shell。 系統會在命令提示字元中要求您提供虛擬機器的認證。

```azurepowershell-interactive
$vNetName = "myIISSQLvNet"
$resourceGroup = "myIISSQLGroup"
New-AzVm -Name myIISVM -ResourceGroupName $resourceGroup -VirtualNetworkName $vNetName 
```

使用自訂指令碼擴充功能安裝 IIS 和 .NET Framework。

```azurepowershell-interactive

Set-AzureRmVMExtension -ResourceGroupName $resourceGroup `
    -ExtensionName IIS `
    -VMName myIISVM `
    -Publisher Microsoft.Compute `
    -ExtensionType CustomScriptExtension `
    -TypeHandlerVersion 1.4 `
    -SettingString '{"commandToExecute":"powershell Add-WindowsFeature Web-Server,Web-Asp-Net45,NET-Framework-Features"}' `
    -Location EastUS
```

## <a name="azure-sql-vm"></a>Azure SQL VM

我們要使用 SQL Server 的預先設定 Azure Marketplace 來建立 SQL VM。 我們會先建立 VM，然後在 VM 上安裝 SQL Server 擴充功能。 


```azurepowershell-interactive
# Create user object. You get a pop-up prompting you to enter the credentials for the VM.
$cred = Get-Credential -Message "Enter a username and password for the virtual machine."

# Create a subnet configuration
$vNet = Get-AzureRmVirtualNetwork -Name $vNetName -ResourceGroupName $resourceGroup
Add-AzureRmVirtualNetworkSubnetConfig -Name mySQLSubnet -VirtualNetwork $vNet -AddressPrefix "192.168.2.0/24"
Set-AzureRmVirtualNetwork -VirtualNetwork $vNet


# Create a public IP address and specify a DNS name
$pip = New-AzureRmPublicIpAddress -ResourceGroupName $resourceGroup -Location eastus `
  -Name "mypublicdns$(Get-Random)" -AllocationMethod Static -IdleTimeoutInMinutes 4

# Create an inbound network security group rule for port 3389
$nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleRDP  -Protocol Tcp `
  -Direction Inbound -Priority 1000 -SourceAddressPrefix * -SourcePortRange * -DestinationAddressPrefix * `
  -DestinationPortRange 3389 -Access Allow


# Create a network security group
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $resourceGroup -Location eastus `
  -Name myNetworkSecurityGroup -SecurityRules $nsgRuleRDP

# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface -Name mySQLNic -ResourceGroupName $resourceGroup -Location eastus `
  -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName mySQLVM -VMSize Standard_D1 | `
Set-AzureRmVMOperatingSystem -Windows -ComputerName mySQLVM -Credential $cred | `
Set-AzureRmVMSourceImage -PublisherName MicrosoftSQLServer -Offer SQL2014SP2-WS2012R2 -Skus Enterprise -Version latest | `
Add-AzureRmVMNetworkInterface -Id $nic.Id

# Create the VM
New-AzureRmVM -ResourceGroupName $resourceGroup -Location eastus -VM $vmConfig
```

使用 [Set-AzureRmVMSqlServerExtension](/powershell/module/azurerm.compute/set-azurermvmsqlserverextension) 將 [SQL Server 擴充功能](/sql/virtual-machines-windows-sql-server-agent-extension.md)新增至 SQL VM。

```azurepowershell-interactive
Set-AzureRmVMSqlServerExtension -ResourceGroupName $resourceGroup -VMName mySQLVM -name "SQLExtension"
```

## <a name="next-steps"></a>後續步驟

在本教學課程中，您會使用 Azure PowerShell 來安裝 SQL&#92;IIS&#92;.NET 堆疊。 您已了解如何︰

> [!div class="checklist"]
> * 使用 New-AzVM 建立 VM
> * 在 VM 上安裝 IIS 和 .NET Core SDK
> * 建立執行 SQL Server 的 VM
> * 安裝 SQL Server 擴充功能

前進到下一個教學課程，以了解如何使用 SSL 憑證保護 IIS Web 伺服器。

> [!div class="nextstepaction"]
> [使用 SSL 憑證保護 IIS Web 伺服器](tutorial-secure-web-server.md)

