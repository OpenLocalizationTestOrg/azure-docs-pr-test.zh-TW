---
title: "快速入門-aaaAzure 建立 VM PowerShell |Microsoft 文件"
description: "使用 PowerShell 的 Linux 虛擬機器快速了解 toocreate"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: f05ea7fedafe4fda660dc6084ae57ebf9dced473
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-virtual-machine-with-powershell"></a>使用 PowerShell 建立 Linux 虛擬機器

hello Azure PowerShell 模組是使用的 toocreate，及管理 Azure 資源，從 hello PowerShell 命令列或指令碼中。 本指南將詳細說明使用 hello Azure PowerShell 模組 toodeploy 執行 Ubuntu server 的虛擬機器。 Hello 伺服器部署之後，建立 SSH 連線，以及 NGINX 網頁伺服器已安裝。

如果您沒有 Azure 訂用帳戶，請在開始前建立 [免費帳戶](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) 。

本快速入門需要 hello Azure PowerShell 模組版本 3.6 版或更新版本。 執行` Get-Module -ListAvailable AzureRM`toofind hello 版本。 如果您需要 tooinstall 或升級，請參閱[安裝 Azure PowerShell 模組](/powershell/azure/install-azurerm-ps)。

最後，公開 SSH 金鑰以 hello 名稱*id_rsa.pub*必須儲存在 hello toobe *.ssh*您的 Windows 使用者設定檔的目錄。 如需建立適用於 Azure 之 SSH 金鑰的詳細資訊，請參閱[建立適用於 Azure 的 SSH 金鑰](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。

## <a name="log-in-tooazure"></a>登入 tooAzure

登入 Azure 訂用帳戶以 hello tooyour`Login-AzureRmAccount`命令，並遵循螢幕上指示 hello。

```powershell
Login-AzureRmAccount
```

## <a name="create-resource-group"></a>建立資源群組

使用 [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) 建立 Azure 資源群組。 資源群組是在其中部署與管理 Azure 資源的邏輯容器。 

```powershell
New-AzureRmResourceGroup -Name myResourceGroup -Location eastus
```

## <a name="create-networking-resources"></a>建立網路資源

建立虛擬網路、子網路和公用 IP 位址。 這些資源是使用的 tooprovide 網路連線 toohello 虛擬機器並將它連接 toohello 網際網路。

```powershell
# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name mySubnet -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork -ResourceGroupName myResourceGroup -Location eastus `
-Name MYvNET -AddressPrefix 192.168.0.0/16 -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$pip = New-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup -Location eastus `
-AllocationMethod Static -IdleTimeoutInMinutes 4 -Name "mypublicdns$(Get-Random)"
```

建立網路安全性群組和網路安全性群組規則。 網路安全性群組 hello 可保護使用輸入和輸出規則 hello 虛擬機器。 在此情況下，會建立連接埠 22 的輸入規則，以允許連入的 SSH 連線。 我們也想要 toocreate 的輸入規則允許連入的 web 流量的連接埠 80。

```powershell
# Create an inbound network security group rule for port 22
$nsgRuleSSH = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleSSH  -Protocol Tcp `
-Direction Inbound -Priority 1000 -SourceAddressPrefix * -SourcePortRange * -DestinationAddressPrefix * `
-DestinationPortRange 22 -Access Allow

# Create an inbound network security group rule for port 80
$nsgRuleWeb = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleWWW  -Protocol Tcp `
-Direction Inbound -Priority 1001 -SourceAddressPrefix * -SourcePortRange * -DestinationAddressPrefix * `
-DestinationPortRange 80 -Access Allow

# Create a network security group
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName myResourceGroup -Location eastus `
-Name myNetworkSecurityGroup -SecurityRules $nsgRuleSSH,$nsgRuleWeb
```

建立與網路卡[新增 AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) hello 虛擬機器。 hello 網路卡會連接 hello 虛擬機器 tooa 子網路、 網路安全性群組和公用 IP 位址。

```powershell
# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface -Name myNic -ResourceGroupName myResourceGroup -Location eastus `
-SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id
```

## <a name="create-virtual-machine"></a>Create virtual machine

建立虛擬機器組態。 這項設定包括 hello 虛擬機器，例如虛擬機器映像、 大小和驗證設定部署時所使用的 hello 設定。

```powershell
# Define a credential object
$securePassword = ConvertTo-SecureString ' ' -AsPlainText -Force
$cred = New-Object System.Management.Automation.PSCredential ("azureuser", $securePassword)

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName myVM -VMSize Standard_D1 | `
Set-AzureRmVMOperatingSystem -Linux -ComputerName myVM -Credential $cred -DisablePasswordAuthentication | `
Set-AzureRmVMSourceImage -PublisherName Canonical -Offer UbuntuServer -Skus 14.04.2-LTS -Version latest | `
Add-AzureRmVMNetworkInterface -Id $nic.Id

# Configure SSH Keys
$sshPublicKey = Get-Content "$env:USERPROFILE\.ssh\id_rsa.pub"
Add-AzureRmVMSshPublicKey -VM $vmconfig -KeyData $sshPublicKey -Path "/home/azureuser/.ssh/authorized_keys"
```

建立虛擬機器 hello[新增 AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm)。

```powershell
New-AzureRmVM -ResourceGroupName myResourceGroup -Location eastus -VM $vmConfig
```

## <a name="connect-toovirtual-machine"></a>Toovirtual 機器連線

Hello 部署完成後，建立 SSH 連線與 hello 虛擬機器。

使用 hello [Get AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress)命令 tooreturn hello 公用 IP 位址的 hello 虛擬機器。

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup | Select IpAddress
```

從透過 SSH 安裝系統，使用的 hello 下列命令 tooconnect toohello 虛擬機器。 如果在 Windows 中，使用[Putty](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-ssh-from-windows?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#create-a-private-key-for-putty)可以是使用的 toocreate hello 連線。 

```bash 
ssh <Public IP Address>
```

出現提示時，hello 登入使用者名稱為*azureuser*。 如果建立 SSH 金鑰時，所輸入的複雜密碼，您需要此以及 tooenter。


## <a name="install-nginx"></a>安裝 NGINX

使用 hello 以下撞指令碼 tooupdate 封裝來源，並安裝最新 NGINX 套件 hello。 

```bash 
#!/bin/bash

# update package source
apt-get -y update

# install NGINX
apt-get -y install nginx
```

## <a name="view-hello-ngix-welcome-page"></a>檢視 hello NGIX 歡迎使用 頁面

現在從 hello 網際網路-VM 上開啟連接埠 80 與 NGINX 安裝中，您可以使用網頁瀏覽器，您的選擇 tooview hello 預設 NGINX 歡迎頁面。 為確定 toouse hello 公用 IP 位址您 toovisit hello 預設頁面上面所記載。 

![預設 NGINX 網站](./media/quick-create-cli/nginx.png) 

## <a name="clean-up-resources"></a>清除資源

當不再需要您可以使用 hello[移除 AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup)命令 tooremove hello 資源群組、 VM 和所有相關的資源。

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="next-steps"></a>後續步驟

在此快速入門中，您已部署簡單的虛擬機器、網路安全性群組規則，並已安裝 Web 伺服器。 進一步了解 Azure 虛擬機器，toolearn 繼續 toohello 教學課程適用於 Linux Vm。

> [!div class="nextstepaction"]
> [Azure Linux 虛擬機器教學課程](./tutorial-manage-vm.md)
