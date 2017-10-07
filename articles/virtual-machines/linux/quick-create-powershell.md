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
# <a name="create-a-linux-virtual-machine-with-powershell"></a><span data-ttu-id="8cec0-103">使用 PowerShell 建立 Linux 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="8cec0-103">Create a Linux virtual machine with PowerShell</span></span>

<span data-ttu-id="8cec0-104">hello Azure PowerShell 模組是使用的 toocreate，及管理 Azure 資源，從 hello PowerShell 命令列或指令碼中。</span><span class="sxs-lookup"><span data-stu-id="8cec0-104">hello Azure PowerShell module is used toocreate and manage Azure resources from hello PowerShell command line or in scripts.</span></span> <span data-ttu-id="8cec0-105">本指南將詳細說明使用 hello Azure PowerShell 模組 toodeploy 執行 Ubuntu server 的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="8cec0-105">This guide details using hello Azure PowerShell module toodeploy a virtual machine running Ubuntu server.</span></span> <span data-ttu-id="8cec0-106">Hello 伺服器部署之後，建立 SSH 連線，以及 NGINX 網頁伺服器已安裝。</span><span class="sxs-lookup"><span data-stu-id="8cec0-106">Once hello server is deployed, an SSH connection is created, and an NGINX webserver is installed.</span></span>

<span data-ttu-id="8cec0-107">如果您沒有 Azure 訂用帳戶，請在開始前建立 [免費帳戶](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) 。</span><span class="sxs-lookup"><span data-stu-id="8cec0-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="8cec0-108">本快速入門需要 hello Azure PowerShell 模組版本 3.6 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="8cec0-108">This quick start requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="8cec0-109">執行` Get-Module -ListAvailable AzureRM`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="8cec0-109">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="8cec0-110">如果您需要 tooinstall 或升級，請參閱[安裝 Azure PowerShell 模組](/powershell/azure/install-azurerm-ps)。</span><span class="sxs-lookup"><span data-stu-id="8cec0-110">If you need tooinstall or upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

<span data-ttu-id="8cec0-111">最後，公開 SSH 金鑰以 hello 名稱*id_rsa.pub*必須儲存在 hello toobe *.ssh*您的 Windows 使用者設定檔的目錄。</span><span class="sxs-lookup"><span data-stu-id="8cec0-111">Finally, a public SSH key with hello name *id_rsa.pub* needs toobe stored in hello *.ssh* directory of your Windows user profile.</span></span> <span data-ttu-id="8cec0-112">如需建立適用於 Azure 之 SSH 金鑰的詳細資訊，請參閱[建立適用於 Azure 的 SSH 金鑰](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="8cec0-112">For detailed information on creating SSH keys for Azure, see [Create SSH keys for Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="8cec0-113">登入 tooAzure</span><span class="sxs-lookup"><span data-stu-id="8cec0-113">Log in tooAzure</span></span>

<span data-ttu-id="8cec0-114">登入 Azure 訂用帳戶以 hello tooyour`Login-AzureRmAccount`命令，並遵循螢幕上指示 hello。</span><span class="sxs-lookup"><span data-stu-id="8cec0-114">Log in tooyour Azure subscription with hello `Login-AzureRmAccount` command and follow hello on-screen directions.</span></span>

```powershell
Login-AzureRmAccount
```

## <a name="create-resource-group"></a><span data-ttu-id="8cec0-115">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="8cec0-115">Create resource group</span></span>

<span data-ttu-id="8cec0-116">使用 [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) 建立 Azure 資源群組。</span><span class="sxs-lookup"><span data-stu-id="8cec0-116">Create an Azure resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="8cec0-117">資源群組是在其中部署與管理 Azure 資源的邏輯容器。</span><span class="sxs-lookup"><span data-stu-id="8cec0-117">A resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

```powershell
New-AzureRmResourceGroup -Name myResourceGroup -Location eastus
```

## <a name="create-networking-resources"></a><span data-ttu-id="8cec0-118">建立網路資源</span><span class="sxs-lookup"><span data-stu-id="8cec0-118">Create networking resources</span></span>

<span data-ttu-id="8cec0-119">建立虛擬網路、子網路和公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="8cec0-119">Create a virtual network, subnet, and a public IP address.</span></span> <span data-ttu-id="8cec0-120">這些資源是使用的 tooprovide 網路連線 toohello 虛擬機器並將它連接 toohello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="8cec0-120">These resources are used tooprovide network connectivity toohello virtual machine and connect it toohello internet.</span></span>

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

<span data-ttu-id="8cec0-121">建立網路安全性群組和網路安全性群組規則。</span><span class="sxs-lookup"><span data-stu-id="8cec0-121">Create a network security group and a network security group rule.</span></span> <span data-ttu-id="8cec0-122">網路安全性群組 hello 可保護使用輸入和輸出規則 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="8cec0-122">hello network security group secures hello virtual machine using inbound and outbound rules.</span></span> <span data-ttu-id="8cec0-123">在此情況下，會建立連接埠 22 的輸入規則，以允許連入的 SSH 連線。</span><span class="sxs-lookup"><span data-stu-id="8cec0-123">In this case, an inbound rule is created for port 22, which allows incoming SSH connections.</span></span> <span data-ttu-id="8cec0-124">我們也想要 toocreate 的輸入規則允許連入的 web 流量的連接埠 80。</span><span class="sxs-lookup"><span data-stu-id="8cec0-124">We also want toocreate an inbound rule for port 80, which allows incoming web traffic.</span></span>

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

<span data-ttu-id="8cec0-125">建立與網路卡[新增 AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="8cec0-125">Create a network card with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) for hello virtual machine.</span></span> <span data-ttu-id="8cec0-126">hello 網路卡會連接 hello 虛擬機器 tooa 子網路、 網路安全性群組和公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="8cec0-126">hello network card connects hello virtual machine tooa subnet, network security group, and public IP address.</span></span>

```powershell
# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface -Name myNic -ResourceGroupName myResourceGroup -Location eastus `
-SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id
```

## <a name="create-virtual-machine"></a><span data-ttu-id="8cec0-127">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="8cec0-127">Create virtual machine</span></span>

<span data-ttu-id="8cec0-128">建立虛擬機器組態。</span><span class="sxs-lookup"><span data-stu-id="8cec0-128">Create a virtual machine configuration.</span></span> <span data-ttu-id="8cec0-129">這項設定包括 hello 虛擬機器，例如虛擬機器映像、 大小和驗證設定部署時所使用的 hello 設定。</span><span class="sxs-lookup"><span data-stu-id="8cec0-129">This configuration includes hello settings that are used when deploying hello virtual machine such as a virtual machine image, size, and authentication configuration.</span></span>

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

<span data-ttu-id="8cec0-130">建立虛擬機器 hello[新增 AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm)。</span><span class="sxs-lookup"><span data-stu-id="8cec0-130">Create hello virtual machine with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span>

```powershell
New-AzureRmVM -ResourceGroupName myResourceGroup -Location eastus -VM $vmConfig
```

## <a name="connect-toovirtual-machine"></a><span data-ttu-id="8cec0-131">Toovirtual 機器連線</span><span class="sxs-lookup"><span data-stu-id="8cec0-131">Connect toovirtual machine</span></span>

<span data-ttu-id="8cec0-132">Hello 部署完成後，建立 SSH 連線與 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="8cec0-132">After hello deployment has completed, create an SSH connection with hello virtual machine.</span></span>

<span data-ttu-id="8cec0-133">使用 hello [Get AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress)命令 tooreturn hello 公用 IP 位址的 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="8cec0-133">Use hello [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) command tooreturn hello public IP address of hello virtual machine.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup | Select IpAddress
```

<span data-ttu-id="8cec0-134">從透過 SSH 安裝系統，使用的 hello 下列命令 tooconnect toohello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="8cec0-134">From a system with SSH installed, used hello following command tooconnect toohello virtual machine.</span></span> <span data-ttu-id="8cec0-135">如果在 Windows 中，使用[Putty](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-ssh-from-windows?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#create-a-private-key-for-putty)可以是使用的 toocreate hello 連線。</span><span class="sxs-lookup"><span data-stu-id="8cec0-135">If working on Windows, [Putty](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-ssh-from-windows?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#create-a-private-key-for-putty) can be used toocreate hello connection.</span></span> 

```bash 
ssh <Public IP Address>
```

<span data-ttu-id="8cec0-136">出現提示時，hello 登入使用者名稱為*azureuser*。</span><span class="sxs-lookup"><span data-stu-id="8cec0-136">When prompted, hello login user name is *azureuser*.</span></span> <span data-ttu-id="8cec0-137">如果建立 SSH 金鑰時，所輸入的複雜密碼，您需要此以及 tooenter。</span><span class="sxs-lookup"><span data-stu-id="8cec0-137">If a passphrase was entered when creating SSH keys, you need tooenter this as well.</span></span>


## <a name="install-nginx"></a><span data-ttu-id="8cec0-138">安裝 NGINX</span><span class="sxs-lookup"><span data-stu-id="8cec0-138">Install NGINX</span></span>

<span data-ttu-id="8cec0-139">使用 hello 以下撞指令碼 tooupdate 封裝來源，並安裝最新 NGINX 套件 hello。</span><span class="sxs-lookup"><span data-stu-id="8cec0-139">Use hello following bash script tooupdate package sources and install hello latest NGINX package.</span></span> 

```bash 
#!/bin/bash

# update package source
apt-get -y update

# install NGINX
apt-get -y install nginx
```

## <a name="view-hello-ngix-welcome-page"></a><span data-ttu-id="8cec0-140">檢視 hello NGIX 歡迎使用 頁面</span><span class="sxs-lookup"><span data-stu-id="8cec0-140">View hello NGIX welcome page</span></span>

<span data-ttu-id="8cec0-141">現在從 hello 網際網路-VM 上開啟連接埠 80 與 NGINX 安裝中，您可以使用網頁瀏覽器，您的選擇 tooview hello 預設 NGINX 歡迎頁面。</span><span class="sxs-lookup"><span data-stu-id="8cec0-141">With NGINX installed and port 80 now open on your VM from hello Internet - you can use a web browser of your choice tooview hello default NGINX welcome page.</span></span> <span data-ttu-id="8cec0-142">為確定 toouse hello 公用 IP 位址您 toovisit hello 預設頁面上面所記載。</span><span class="sxs-lookup"><span data-stu-id="8cec0-142">Be sure toouse hello public IP address you documented above toovisit hello default page.</span></span> 

![預設 NGINX 網站](./media/quick-create-cli/nginx.png) 

## <a name="clean-up-resources"></a><span data-ttu-id="8cec0-144">清除資源</span><span class="sxs-lookup"><span data-stu-id="8cec0-144">Clean up resources</span></span>

<span data-ttu-id="8cec0-145">當不再需要您可以使用 hello[移除 AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup)命令 tooremove hello 資源群組、 VM 和所有相關的資源。</span><span class="sxs-lookup"><span data-stu-id="8cec0-145">When no longer needed, you can use hello [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="8cec0-146">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8cec0-146">Next steps</span></span>

<span data-ttu-id="8cec0-147">在此快速入門中，您已部署簡單的虛擬機器、網路安全性群組規則，並已安裝 Web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="8cec0-147">In this quick start, you’ve deployed a simple virtual machine, a network security group rule, and installed a web server.</span></span> <span data-ttu-id="8cec0-148">進一步了解 Azure 虛擬機器，toolearn 繼續 toohello 教學課程適用於 Linux Vm。</span><span class="sxs-lookup"><span data-stu-id="8cec0-148">toolearn more about Azure virtual machines, continue toohello tutorial for Linux VMs.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="8cec0-149">Azure Linux 虛擬機器教學課程</span><span class="sxs-lookup"><span data-stu-id="8cec0-149">Azure Linux virtual machine tutorials</span></span>](./tutorial-manage-vm.md)
