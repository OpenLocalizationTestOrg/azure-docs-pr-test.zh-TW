---
title: "Azure 中的 Windows VM aaaCustomize |Microsoft 文件"
description: "了解如何 toouse hello 自訂指令碼延伸和金鑰保存庫 toocustomize Windows Azure 中的 Vm"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 08/11/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: c03b2bb6d70875134c63ea2fe4c2e2c1777c2188
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocustomize-a-windows-virtual-machine-in-azure"></a>如何 toocustomize Azure 中的 Windows 虛擬機器
通常需要快速且一致的方式，某種形式的自動化 tooconfigure 虛擬機器 (Vm)。 常見的方法 toocustomize Windows VM 是 toouse[自訂指令碼延伸的視窗](extensions-customscript.md)。 在本教學課程中，您了解如何：

> [!div class="checklist"]
> * 使用 hello 自訂指令碼擴充 tooinstall IIS
> * 建立 VM 使用 hello 自訂指令碼擴充
> * 套用 hello 延伸之後，檢視正在執行的 IIS 站台

本教學課程需要 hello Azure PowerShell 模組版本 3.6 版或更新版本。 執行` Get-Module -ListAvailable AzureRM`toofind hello 版本。 如果您需要 tooupgrade，請參閱[安裝 Azure PowerShell 模組](/powershell/azure/install-azurerm-ps)。


## <a name="custom-script-extension-overview"></a>自訂指令碼擴充功能概觀
hello 自訂指令碼擴充功能下載並在 Azure Vm 上執行指令碼。 此擴充功能適用於部署後組態、軟體安裝或其他任何組態/管理工作。 可以從 Azure 儲存體或 GitHub 下載指令碼，或提供 toohello 在執行階段的延伸模組的 Azure 入口網站。

hello 自訂指令碼擴充功能與整合 Azure 資源管理員範本，並也可以執行使用 hello Azure CLI、 PowerShell、 Azure 入口網站或 hello Azure 虛擬機器 REST API。

您可以使用 Windows 和 Linux Vm 建立 hello 自訂指令碼擴充。


## <a name="create-virtual-machine"></a>Create virtual machine
建立 VM 之前，請先使用 [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) 來建立資源群組。 hello 下列範例會建立名為的資源群組*myResourceGroupAutomate*在 hello *EastUS*位置：

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroupAutomate -Location EastUS
```

設定系統管理員使用者名稱和密碼具有 hello Vm [Get-credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):

```powershell
$cred = Get-Credential
```

現在您可以建立 hello 與 VM[新增 AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm)。 hello 下列範例會建立所需的 hello 虛擬網路的元件，hello 作業系統組態，然後建立名為的 VM *myVM*:

```powershell
# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork `
    -ResourceGroupName myResourceGroupAutomate `
    -Location EastUS `
    -Name myVnet `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$publicIP = New-AzureRmPublicIpAddress `
    -ResourceGroupName myResourceGroupAutomate `
    -Location EastUS `
    -AllocationMethod Static `
    -IdleTimeoutInMinutes 4 `
    -Name "myPublicIP"

# Create an inbound network security group rule for port 3389
$nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig `
    -Name myNetworkSecurityGroupRuleRDP  `
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
    -Name myNetworkSecurityGroupRuleWWW  `
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
    -ResourceGroupName myResourceGroupAutomate `
    -Location EastUS `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRuleRDP,$nsgRuleWeb

# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface `
    -Name myNic `
    -ResourceGroupName myResourceGroupAutomate `
    -Location EastUS `
    -SubnetId $vnet.Subnets[0].Id `
    -PublicIpAddressId $publicIP.Id `
    -NetworkSecurityGroupId $nsg.Id

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName myVM -VMSize Standard_DS2 | `
Set-AzureRmVMOperatingSystem -Windows -ComputerName myVM -Credential $cred | `
Set-AzureRmVMSourceImage -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer -Skus 2016-Datacenter -Version latest | `
Add-AzureRmVMNetworkInterface -Id $nic.Id

New-AzureRmVM -ResourceGroupName myResourceGroupAutomate -Location EastUS -VM $vmConfig
```

花幾分鐘，讓 hello 資源和 VM toobe 建立。


## <a name="automate-iis-install"></a>自動安裝 IIS
使用[組 AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall hello 自訂指令碼擴充。 hello 延伸模組執行`powershell Add-WindowsFeature Web-Server`tooinstall hello IIS 網頁伺服器，然後再更新 hello *Default.htm*頁面 tooshow hello 主機名稱的 hello VM:

```powershell
Set-AzureRmVMExtension -ResourceGroupName myResourceGroupAutomate `
    -ExtensionName IIS `
    -VMName myVM `
    -Publisher Microsoft.Compute `
    -ExtensionType CustomScriptExtension `
    -TypeHandlerVersion 1.4 `
    -SettingString '{"commandToExecute":"powershell Add-WindowsFeature Web-Server; powershell Add-Content -Path \"C:\\inetpub\\wwwroot\\Default.htm\" -Value $($env:computername)"}' `
    -Location EastUS
```


## <a name="test-web-site"></a>測試網站
取得您的負載平衡器的 hello 公用 IP 位址[Get AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress)。 hello 下列範例會取得 IP 位址 hello *myPublicIP*稍早建立：

```powershell
Get-AzureRmPublicIPAddress `
    -ResourceGroupName myResourceGroupAutomate `
    -Name myPublicIP | select IpAddress
```

然後，您就可以 tooa 網頁瀏覽器中輸入 hello 公用 IP 位址。 hello 網站將會顯示，包括 hello hello VM 主機名稱的 hello 負載平衡器分散流量 tooas hello 下列範例中：

![執行中的 IIS 網站](./media/tutorial-automate-vm-deployment/running-iis-website.png)


## <a name="next-steps"></a>後續步驟

在本教學課程中，您可以自動化的 hello 在 VM 安裝 IIS。 您已了解如何︰

> [!div class="checklist"]
> * 使用 hello 自訂指令碼擴充 tooinstall IIS
> * 建立 VM 使用 hello 自訂指令碼擴充
> * 套用 hello 延伸之後，檢視正在執行的 IIS 站台

如何前進 toohello 下一個教學課程 toolearn toocreate 自訂 VM 映像。

> [!div class="nextstepaction"]
> [建立自訂的 VM 映像](./tutorial-custom-images.md)
