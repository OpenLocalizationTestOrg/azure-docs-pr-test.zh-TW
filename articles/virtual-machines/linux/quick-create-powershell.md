---
title: "Azure 快速入門 - 建立 VM PowerShell | Microsoft Docs"
description: "快速了解如何使用 PowerShell 建立 Linux 虛擬機器"
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
ms.openlocfilehash: adcf492d4c2d935c880167675a1ed97566156ec7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-linux-virtual-machine-with-powershell"></a><span data-ttu-id="f8eb7-103">使用 PowerShell 建立 Linux 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="f8eb7-103">Create a Linux virtual machine with PowerShell</span></span>

<span data-ttu-id="f8eb7-104">Azure PowerShell 模組用於從 PowerShell 命令列或在指令碼中建立和管理 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="f8eb7-104">The Azure PowerShell module is used to create and manage Azure resources from the PowerShell command line or in scripts.</span></span> <span data-ttu-id="f8eb7-105">本指南詳細說明如何使用 Azure PowerShell 模組來部署執行 Ubuntu 伺服器的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="f8eb7-105">This guide details using the Azure PowerShell module to deploy a virtual machine running Ubuntu server.</span></span> <span data-ttu-id="f8eb7-106">一旦部署伺服器，就會建立 SSH 連線，以及安裝 NGINX Web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="f8eb7-106">Once the server is deployed, an SSH connection is created, and an NGINX webserver is installed.</span></span>

<span data-ttu-id="f8eb7-107">如果您沒有 Azure 訂用帳戶，請在開始前建立 [免費帳戶](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) 。</span><span class="sxs-lookup"><span data-stu-id="f8eb7-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="f8eb7-108">本快速入門需要 Azure PowerShell 模組 3.6 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="f8eb7-108">This quick start requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="f8eb7-109">執行 ` Get-Module -ListAvailable AzureRM` 以尋找版本。</span><span class="sxs-lookup"><span data-stu-id="f8eb7-109">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="f8eb7-110">如果您需要安裝或升級，請參閱[安裝 Azure PowerShell 模組](/powershell/azure/install-azurerm-ps)。</span><span class="sxs-lookup"><span data-stu-id="f8eb7-110">If you need to install or upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

<span data-ttu-id="f8eb7-111">最後，名稱為 id_rsa.pub 的公開 SSH 金鑰必須儲存在 Windows 使用者設定檔的 .ssh 目錄中。</span><span class="sxs-lookup"><span data-stu-id="f8eb7-111">Finally, a public SSH key with the name *id_rsa.pub* needs to be stored in the *.ssh* directory of your Windows user profile.</span></span> <span data-ttu-id="f8eb7-112">如需建立適用於 Azure 之 SSH 金鑰的詳細資訊，請參閱[建立適用於 Azure 的 SSH 金鑰](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="f8eb7-112">For detailed information on creating SSH keys for Azure, see [Create SSH keys for Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="f8eb7-113">登入 Azure</span><span class="sxs-lookup"><span data-stu-id="f8eb7-113">Log in to Azure</span></span>

<span data-ttu-id="f8eb7-114">使用 `Login-AzureRmAccount` 命令登入 Azure 訂用帳戶並遵循畫面上的指示。</span><span class="sxs-lookup"><span data-stu-id="f8eb7-114">Log in to your Azure subscription with the `Login-AzureRmAccount` command and follow the on-screen directions.</span></span>

```powershell
Login-AzureRmAccount
```

## <a name="create-resource-group"></a><span data-ttu-id="f8eb7-115">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="f8eb7-115">Create resource group</span></span>

<span data-ttu-id="f8eb7-116">使用 [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) 建立 Azure 資源群組。</span><span class="sxs-lookup"><span data-stu-id="f8eb7-116">Create an Azure resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="f8eb7-117">資源群組是在其中部署與管理 Azure 資源的邏輯容器。</span><span class="sxs-lookup"><span data-stu-id="f8eb7-117">A resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

```powershell
New-AzureRmResourceGroup -Name myResourceGroup -Location eastus
```

## <a name="create-networking-resources"></a><span data-ttu-id="f8eb7-118">建立網路資源</span><span class="sxs-lookup"><span data-stu-id="f8eb7-118">Create networking resources</span></span>

<span data-ttu-id="f8eb7-119">建立虛擬網路、子網路和公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="f8eb7-119">Create a virtual network, subnet, and a public IP address.</span></span> <span data-ttu-id="f8eb7-120">這些資源用來提供虛擬機器的網路連線能力，並可將它連線到網際網路。</span><span class="sxs-lookup"><span data-stu-id="f8eb7-120">These resources are used to provide network connectivity to the virtual machine and connect it to the internet.</span></span>

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

<span data-ttu-id="f8eb7-121">建立網路安全性群組和網路安全性群組規則。</span><span class="sxs-lookup"><span data-stu-id="f8eb7-121">Create a network security group and a network security group rule.</span></span> <span data-ttu-id="f8eb7-122">網路安全性群組可使用輸入和輸出規則來保護虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="f8eb7-122">The network security group secures the virtual machine using inbound and outbound rules.</span></span> <span data-ttu-id="f8eb7-123">在此情況下，會建立連接埠 22 的輸入規則，以允許連入的 SSH 連線。</span><span class="sxs-lookup"><span data-stu-id="f8eb7-123">In this case, an inbound rule is created for port 22, which allows incoming SSH connections.</span></span> <span data-ttu-id="f8eb7-124">我們也會建立連接埠 80 的輸入規則，以允許連入的 Web 流量。</span><span class="sxs-lookup"><span data-stu-id="f8eb7-124">We also want to create an inbound rule for port 80, which allows incoming web traffic.</span></span>

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

<span data-ttu-id="f8eb7-125">使用 [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) 建立虛擬機器的網路卡。</span><span class="sxs-lookup"><span data-stu-id="f8eb7-125">Create a network card with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) for the virtual machine.</span></span> <span data-ttu-id="f8eb7-126">網路卡可讓虛擬機器連線到子網路、網路安全性群組和公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="f8eb7-126">The network card connects the virtual machine to a subnet, network security group, and public IP address.</span></span>

```powershell
# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface -Name myNic -ResourceGroupName myResourceGroup -Location eastus `
-SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id
```

## <a name="create-virtual-machine"></a><span data-ttu-id="f8eb7-127">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="f8eb7-127">Create virtual machine</span></span>

<span data-ttu-id="f8eb7-128">建立虛擬機器組態。</span><span class="sxs-lookup"><span data-stu-id="f8eb7-128">Create a virtual machine configuration.</span></span> <span data-ttu-id="f8eb7-129">此組態包括部署虛擬機器時所使用的組態，例如虛擬機器映像、大小和驗證組態。</span><span class="sxs-lookup"><span data-stu-id="f8eb7-129">This configuration includes the settings that are used when deploying the virtual machine such as a virtual machine image, size, and authentication configuration.</span></span>

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

<span data-ttu-id="f8eb7-130">使用 [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) 建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="f8eb7-130">Create the virtual machine with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span>

```powershell
New-AzureRmVM -ResourceGroupName myResourceGroup -Location eastus -VM $vmConfig
```

## <a name="connect-to-virtual-machine"></a><span data-ttu-id="f8eb7-131">連線至虛擬機器</span><span class="sxs-lookup"><span data-stu-id="f8eb7-131">Connect to virtual machine</span></span>

<span data-ttu-id="f8eb7-132">完成部署之後，建立與虛擬機器的 SSH 連線。</span><span class="sxs-lookup"><span data-stu-id="f8eb7-132">After the deployment has completed, create an SSH connection with the virtual machine.</span></span>

<span data-ttu-id="f8eb7-133">使用 [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) 命令，以傳回虛擬機器的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="f8eb7-133">Use the [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) command to return the public IP address of the virtual machine.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup | Select IpAddress
```

<span data-ttu-id="f8eb7-134">從已安裝 SSH 的系統，使用下列命令來連線至虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="f8eb7-134">From a system with SSH installed, used the following command to connect to the virtual machine.</span></span> <span data-ttu-id="f8eb7-135">如果使用 Windows，則可使用 [Putty](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-ssh-from-windows?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#create-a-private-key-for-putty) 來建立連線。</span><span class="sxs-lookup"><span data-stu-id="f8eb7-135">If working on Windows, [Putty](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-ssh-from-windows?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#create-a-private-key-for-putty) can be used to create the connection.</span></span> 

```bash 
ssh <Public IP Address>
```

<span data-ttu-id="f8eb7-136">出現提示時，登入使用者名稱為 azureuser。</span><span class="sxs-lookup"><span data-stu-id="f8eb7-136">When prompted, the login user name is *azureuser*.</span></span> <span data-ttu-id="f8eb7-137">如果在建立 SSH 金鑰時輸入複雜密碼，您也必須輸入此使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="f8eb7-137">If a passphrase was entered when creating SSH keys, you need to enter this as well.</span></span>


## <a name="install-nginx"></a><span data-ttu-id="f8eb7-138">安裝 NGINX</span><span class="sxs-lookup"><span data-stu-id="f8eb7-138">Install NGINX</span></span>

<span data-ttu-id="f8eb7-139">使用下列 bash 指令碼來更新套件來源及安裝最新的 NGINX 套件。</span><span class="sxs-lookup"><span data-stu-id="f8eb7-139">Use the following bash script to update package sources and install the latest NGINX package.</span></span> 

```bash 
#!/bin/bash

# update package source
apt-get -y update

# install NGINX
apt-get -y install nginx
```

## <a name="view-the-ngix-welcome-page"></a><span data-ttu-id="f8eb7-140">檢視 NGIX 歡迎使用頁面</span><span class="sxs-lookup"><span data-stu-id="f8eb7-140">View the NGIX welcome page</span></span>

<span data-ttu-id="f8eb7-141">安裝 NGINX 後，現在經由網際網路在您的 VM 上開啟連接埠 80 - 您可以使用所選的網頁瀏覽器來檢視預設 NGINX 歡迎使用畫面。</span><span class="sxs-lookup"><span data-stu-id="f8eb7-141">With NGINX installed and port 80 now open on your VM from the Internet - you can use a web browser of your choice to view the default NGINX welcome page.</span></span> <span data-ttu-id="f8eb7-142">請務必使用您上面記載的公用 IP 位址來瀏覽預設網頁。</span><span class="sxs-lookup"><span data-stu-id="f8eb7-142">Be sure to use the public IP address you documented above to visit the default page.</span></span> 

![預設 NGINX 網站](./media/quick-create-cli/nginx.png) 

## <a name="clean-up-resources"></a><span data-ttu-id="f8eb7-144">清除資源</span><span class="sxs-lookup"><span data-stu-id="f8eb7-144">Clean up resources</span></span>

<span data-ttu-id="f8eb7-145">若不再需要，您可以使用 [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) 命令來移除資源群組、VM 和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="f8eb7-145">When no longer needed, you can use the [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="f8eb7-146">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f8eb7-146">Next steps</span></span>

<span data-ttu-id="f8eb7-147">在此快速入門中，您已部署簡單的虛擬機器、網路安全性群組規則，並已安裝 Web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="f8eb7-147">In this quick start, you’ve deployed a simple virtual machine, a network security group rule, and installed a web server.</span></span> <span data-ttu-id="f8eb7-148">若要深入了解 Azure 虛擬機器，請繼續 Linux VM 的教學課程。</span><span class="sxs-lookup"><span data-stu-id="f8eb7-148">To learn more about Azure virtual machines, continue to the tutorial for Linux VMs.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f8eb7-149">Azure Linux 虛擬機器教學課程</span><span class="sxs-lookup"><span data-stu-id="f8eb7-149">Azure Linux virtual machine tutorials</span></span>](./tutorial-manage-vm.md)
