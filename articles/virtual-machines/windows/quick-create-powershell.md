---
title: "快速入門-aaaAzure 建立 Windows VM PowerShell |Microsoft 文件"
description: "使用 PowerShell 的 Windows 虛擬機器快速了解 toocreate"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 5e92435bf7ee443a01c158fed91c356363e2f425
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-virtual-machine-with-powershell"></a>使用 PowerShell 建立 Windows 虛擬機器

hello Azure PowerShell 模組是使用的 toocreate，及管理 Azure 資源，從 hello PowerShell 命令列或指令碼中。 使用 PowerShell toocreate 和 Azure 虛擬機器執行 Windows Server 2016 本指南詳細說明。 當部署完成之後，我們 toohello 伺服器連接，並安裝 IIS。  

如果您沒有 Azure 訂用帳戶，請在開始前建立 [免費帳戶](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) 。

本快速入門需要 hello Azure PowerShell 模組版本 3.6 版或更新版本。 執行` Get-Module -ListAvailable AzureRM`toofind hello 版本。 如果您需要 tooinstall 或升級，請參閱[安裝 Azure PowerShell 模組](/powershell/azure/install-azurerm-ps)。

## <a name="log-in-tooazure"></a>登入 tooAzure

登入 Azure 訂用帳戶以 hello tooyour`Login-AzureRmAccount`命令，並遵循螢幕上指示 hello。

```powershell
Login-AzureRmAccount
```

## <a name="create-resource-group"></a>建立資源群組

使用 [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) 建立 Azure 資源群組。 資源群組是在其中部署與管理 Azure 資源的邏輯容器。 

```powershell
New-AzureRmResourceGroup -Name myResourceGroup -Location EastUS
```

## <a name="create-networking-resources"></a>建立網路資源

### <a name="create-a-virtual-network-subnet-and-a-public-ip-address"></a>建立虛擬網路、子網路和公用 IP 位址。 
這些資源是使用的 tooprovide 網路連線 toohello 虛擬機器並將它連接 toohello 網際網路。

```powershell
# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name mySubnet -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork -ResourceGroupName myResourceGroup -Location EastUS `
    -Name MYvNET -AddressPrefix 192.168.0.0/16 -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$pip = New-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup -Location EastUS `
    -AllocationMethod Static -IdleTimeoutInMinutes 4 -Name "mypublicdns$(Get-Random)"
```

### <a name="create-a-network-security-group-and-a-network-security-group-rule"></a>建立網路安全性群組和網路安全性群組規則。 
網路安全性群組 hello 可保護使用輸入和輸出規則 hello 虛擬機器。 在此情況下，會建立連接埠 3389 的輸入規則，以允許連入的遠端桌面連線。 我們也想要 toocreate 的輸入規則允許連入的 web 流量的連接埠 80。

```powershell
# Create an inbound network security group rule for port 3389
$nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleRDP  -Protocol Tcp `
    -Direction Inbound -Priority 1000 -SourceAddressPrefix * -SourcePortRange * -DestinationAddressPrefix * `
    -DestinationPortRange 3389 -Access Allow

# Create an inbound network security group rule for port 80
$nsgRuleWeb = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleWWW  -Protocol Tcp `
    -Direction Inbound -Priority 1001 -SourceAddressPrefix * -SourcePortRange * -DestinationAddressPrefix * `
    -DestinationPortRange 80 -Access Allow

# Create a network security group
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName myResourceGroup -Location EastUS `
    -Name myNetworkSecurityGroup -SecurityRules $nsgRuleRDP,$nsgRuleWeb
```

### <a name="create-a-network-card-for-hello-virtual-machine"></a>建立 hello 虛擬機器網路介面卡。 
建立與網路卡[新增 AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) hello 虛擬機器。 hello 網路卡會連接 hello 虛擬機器 tooa 子網路、 網路安全性群組和公用 IP 位址。

```powershell
# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface -Name myNic -ResourceGroupName myResourceGroup -Location EastUS `
    -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id
```

## <a name="create-virtual-machine"></a>Create virtual machine

建立虛擬機器組態。 這項設定包括 hello 虛擬機器，例如虛擬機器映像、 大小和驗證設定部署時所使用的 hello 設定。 執行此步驟時，系統會提示您輸入認證。 您輸入的 hello 值會設定為 hello 使用者名稱和密碼 hello 虛擬機器。

```powershell
# Define a credential object
$cred = Get-Credential

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName myVM -VMSize Standard_DS2 | `
    Set-AzureRmVMOperatingSystem -Windows -ComputerName myVM -Credential $cred | `
    Set-AzureRmVMSourceImage -PublisherName MicrosoftWindowsServer -Offer WindowsServer `
    -Skus 2016-Datacenter -Version latest | Add-AzureRmVMNetworkInterface -Id $nic.Id
```

建立虛擬機器 hello[新增 AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm)。

```powershell
New-AzureRmVM -ResourceGroupName myResourceGroup -Location EastUS -VM $vmConfig
```

## <a name="connect-toovirtual-machine"></a>Toovirtual 機器連線

Hello 部署已完成之後，請使用 hello 的虛擬機器建立遠端桌面連線。

使用 hello [Get AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress)命令 tooreturn hello 公用 IP 位址的 hello 虛擬機器。 記下此 IP 位址，讓您能連接 tooit 與您的瀏覽器 tootest web 連線，在未來的步驟。

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup | Select IpAddress
```

使用 hello 下列命令 toocreate 與 hello 虛擬機器的遠端桌面工作階段。 Hello IP 位址取代成 hello *publicIPAddress*的虛擬機器。 出現提示時，輸入 hello 建立 hello 虛擬機器時使用的認證。

```bash 
mstsc /v:<publicIpAddress>
```

## <a name="install-iis-via-powershell"></a>透過 PowerShell 安裝 IIS

既然您已登入 toohello Azure VM，您可以使用單行 PowerShell tooinstall IIS，並啟用 hello 本機防火牆規則 tooallow web 流量。 開啟 PowerShell 命令提示字元並執行下列命令的 hello:

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

## <a name="view-hello-iis-welcome-page"></a>檢視 hello IIS [歡迎使用] 頁面

安裝 IIS 和現在 hello 網際網路從 VM 上開啟連接埠 80，您可以使用網頁瀏覽器，您的選擇 tooview hello 預設 IIS 歡迎使用頁面。 要確定 toouse hello *publicIpAddress*您 toovisit hello 預設頁面上面所記載。 

![IIS 預設網站](./media/quick-create-powershell/default-iis-website.png) 

## <a name="clean-up-resources"></a>清除資源

當不再需要您可以使用 hello[移除 AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup)命令 tooremove hello 資源群組、 VM 和所有相關的資源。

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="next-steps"></a>後續步驟

在此快速入門中，您已部署簡單的虛擬機器、網路安全性群組規則，並已安裝 Web 伺服器。 進一步了解 Azure 虛擬機器，toolearn 繼續 toohello 教學課程適用於 Windows Vm。

> [!div class="nextstepaction"]
> [Azure Windows 虛擬機器教學課程](./tutorial-manage-vm.md)
