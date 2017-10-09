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
# <a name="create-a-windows-virtual-machine-with-powershell"></a><span data-ttu-id="59360-103">使用 PowerShell 建立 Windows 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="59360-103">Create a Windows virtual machine with PowerShell</span></span>

<span data-ttu-id="59360-104">hello Azure PowerShell 模組是使用的 toocreate，及管理 Azure 資源，從 hello PowerShell 命令列或指令碼中。</span><span class="sxs-lookup"><span data-stu-id="59360-104">hello Azure PowerShell module is used toocreate and manage Azure resources from hello PowerShell command line or in scripts.</span></span> <span data-ttu-id="59360-105">使用 PowerShell toocreate 和 Azure 虛擬機器執行 Windows Server 2016 本指南詳細說明。</span><span class="sxs-lookup"><span data-stu-id="59360-105">This guide details using PowerShell toocreate and Azure virtual machine running Windows Server 2016.</span></span> <span data-ttu-id="59360-106">當部署完成之後，我們 toohello 伺服器連接，並安裝 IIS。</span><span class="sxs-lookup"><span data-stu-id="59360-106">Once deployment is complete, we connect toohello server and install IIS.</span></span>  

<span data-ttu-id="59360-107">如果您沒有 Azure 訂用帳戶，請在開始前建立 [免費帳戶](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) 。</span><span class="sxs-lookup"><span data-stu-id="59360-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="59360-108">本快速入門需要 hello Azure PowerShell 模組版本 3.6 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="59360-108">This quick start requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="59360-109">執行` Get-Module -ListAvailable AzureRM`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="59360-109">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="59360-110">如果您需要 tooinstall 或升級，請參閱[安裝 Azure PowerShell 模組](/powershell/azure/install-azurerm-ps)。</span><span class="sxs-lookup"><span data-stu-id="59360-110">If you need tooinstall or upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="59360-111">登入 tooAzure</span><span class="sxs-lookup"><span data-stu-id="59360-111">Log in tooAzure</span></span>

<span data-ttu-id="59360-112">登入 Azure 訂用帳戶以 hello tooyour`Login-AzureRmAccount`命令，並遵循螢幕上指示 hello。</span><span class="sxs-lookup"><span data-stu-id="59360-112">Log in tooyour Azure subscription with hello `Login-AzureRmAccount` command and follow hello on-screen directions.</span></span>

```powershell
Login-AzureRmAccount
```

## <a name="create-resource-group"></a><span data-ttu-id="59360-113">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="59360-113">Create resource group</span></span>

<span data-ttu-id="59360-114">使用 [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) 建立 Azure 資源群組。</span><span class="sxs-lookup"><span data-stu-id="59360-114">Create an Azure resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="59360-115">資源群組是在其中部署與管理 Azure 資源的邏輯容器。</span><span class="sxs-lookup"><span data-stu-id="59360-115">A resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

```powershell
New-AzureRmResourceGroup -Name myResourceGroup -Location EastUS
```

## <a name="create-networking-resources"></a><span data-ttu-id="59360-116">建立網路資源</span><span class="sxs-lookup"><span data-stu-id="59360-116">Create networking resources</span></span>

### <a name="create-a-virtual-network-subnet-and-a-public-ip-address"></a><span data-ttu-id="59360-117">建立虛擬網路、子網路和公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="59360-117">Create a virtual network, subnet, and a public IP address.</span></span> 
<span data-ttu-id="59360-118">這些資源是使用的 tooprovide 網路連線 toohello 虛擬機器並將它連接 toohello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="59360-118">These resources are used tooprovide network connectivity toohello virtual machine and connect it toohello internet.</span></span>

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

### <a name="create-a-network-security-group-and-a-network-security-group-rule"></a><span data-ttu-id="59360-119">建立網路安全性群組和網路安全性群組規則。</span><span class="sxs-lookup"><span data-stu-id="59360-119">Create a network security group and a network security group rule.</span></span> 
<span data-ttu-id="59360-120">網路安全性群組 hello 可保護使用輸入和輸出規則 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="59360-120">hello network security group secures hello virtual machine using inbound and outbound rules.</span></span> <span data-ttu-id="59360-121">在此情況下，會建立連接埠 3389 的輸入規則，以允許連入的遠端桌面連線。</span><span class="sxs-lookup"><span data-stu-id="59360-121">In this case, an inbound rule is created for port 3389, which allows incoming remote desktop connections.</span></span> <span data-ttu-id="59360-122">我們也想要 toocreate 的輸入規則允許連入的 web 流量的連接埠 80。</span><span class="sxs-lookup"><span data-stu-id="59360-122">We also want toocreate an inbound rule for port 80, which allows incoming web traffic.</span></span>

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

### <a name="create-a-network-card-for-hello-virtual-machine"></a><span data-ttu-id="59360-123">建立 hello 虛擬機器網路介面卡。</span><span class="sxs-lookup"><span data-stu-id="59360-123">Create a network card for hello virtual machine.</span></span> 
<span data-ttu-id="59360-124">建立與網路卡[新增 AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="59360-124">Create a network card with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) for hello virtual machine.</span></span> <span data-ttu-id="59360-125">hello 網路卡會連接 hello 虛擬機器 tooa 子網路、 網路安全性群組和公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="59360-125">hello network card connects hello virtual machine tooa subnet, network security group, and public IP address.</span></span>

```powershell
# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface -Name myNic -ResourceGroupName myResourceGroup -Location EastUS `
    -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id
```

## <a name="create-virtual-machine"></a><span data-ttu-id="59360-126">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="59360-126">Create virtual machine</span></span>

<span data-ttu-id="59360-127">建立虛擬機器組態。</span><span class="sxs-lookup"><span data-stu-id="59360-127">Create a virtual machine configuration.</span></span> <span data-ttu-id="59360-128">這項設定包括 hello 虛擬機器，例如虛擬機器映像、 大小和驗證設定部署時所使用的 hello 設定。</span><span class="sxs-lookup"><span data-stu-id="59360-128">This configuration includes hello settings that are used when deploying hello virtual machine such as a virtual machine image, size, and authentication configuration.</span></span> <span data-ttu-id="59360-129">執行此步驟時，系統會提示您輸入認證。</span><span class="sxs-lookup"><span data-stu-id="59360-129">When running this step, you are prompted for credentials.</span></span> <span data-ttu-id="59360-130">您輸入的 hello 值會設定為 hello 使用者名稱和密碼 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="59360-130">hello values that you enter are configured as hello user name and password for hello virtual machine.</span></span>

```powershell
# Define a credential object
$cred = Get-Credential

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName myVM -VMSize Standard_DS2 | `
    Set-AzureRmVMOperatingSystem -Windows -ComputerName myVM -Credential $cred | `
    Set-AzureRmVMSourceImage -PublisherName MicrosoftWindowsServer -Offer WindowsServer `
    -Skus 2016-Datacenter -Version latest | Add-AzureRmVMNetworkInterface -Id $nic.Id
```

<span data-ttu-id="59360-131">建立虛擬機器 hello[新增 AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm)。</span><span class="sxs-lookup"><span data-stu-id="59360-131">Create hello virtual machine with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span>

```powershell
New-AzureRmVM -ResourceGroupName myResourceGroup -Location EastUS -VM $vmConfig
```

## <a name="connect-toovirtual-machine"></a><span data-ttu-id="59360-132">Toovirtual 機器連線</span><span class="sxs-lookup"><span data-stu-id="59360-132">Connect toovirtual machine</span></span>

<span data-ttu-id="59360-133">Hello 部署已完成之後，請使用 hello 的虛擬機器建立遠端桌面連線。</span><span class="sxs-lookup"><span data-stu-id="59360-133">After hello deployment has completed, create a remote desktop connection with hello virtual machine.</span></span>

<span data-ttu-id="59360-134">使用 hello [Get AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress)命令 tooreturn hello 公用 IP 位址的 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="59360-134">Use hello [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) command tooreturn hello public IP address of hello virtual machine.</span></span> <span data-ttu-id="59360-135">記下此 IP 位址，讓您能連接 tooit 與您的瀏覽器 tootest web 連線，在未來的步驟。</span><span class="sxs-lookup"><span data-stu-id="59360-135">Take note of this IP Address so you can connect tooit with your browser tootest web connectivity in a future step.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup | Select IpAddress
```

<span data-ttu-id="59360-136">使用 hello 下列命令 toocreate 與 hello 虛擬機器的遠端桌面工作階段。</span><span class="sxs-lookup"><span data-stu-id="59360-136">Use hello following command toocreate a remote desktop session with hello virtual machine.</span></span> <span data-ttu-id="59360-137">Hello IP 位址取代成 hello *publicIPAddress*的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="59360-137">Replace hello IP address with hello *publicIPAddress* of your virtual machine.</span></span> <span data-ttu-id="59360-138">出現提示時，輸入 hello 建立 hello 虛擬機器時使用的認證。</span><span class="sxs-lookup"><span data-stu-id="59360-138">When prompted, enter hello credentials used when creating hello virtual machine.</span></span>

```bash 
mstsc /v:<publicIpAddress>
```

## <a name="install-iis-via-powershell"></a><span data-ttu-id="59360-139">透過 PowerShell 安裝 IIS</span><span class="sxs-lookup"><span data-stu-id="59360-139">Install IIS via PowerShell</span></span>

<span data-ttu-id="59360-140">既然您已登入 toohello Azure VM，您可以使用單行 PowerShell tooinstall IIS，並啟用 hello 本機防火牆規則 tooallow web 流量。</span><span class="sxs-lookup"><span data-stu-id="59360-140">Now that you have logged in toohello Azure VM, you can use a single line of PowerShell tooinstall IIS and enable hello local firewall rule tooallow web traffic.</span></span> <span data-ttu-id="59360-141">開啟 PowerShell 命令提示字元並執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="59360-141">Open a PowerShell prompt and run hello following command:</span></span>

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

## <a name="view-hello-iis-welcome-page"></a><span data-ttu-id="59360-142">檢視 hello IIS [歡迎使用] 頁面</span><span class="sxs-lookup"><span data-stu-id="59360-142">View hello IIS welcome page</span></span>

<span data-ttu-id="59360-143">安裝 IIS 和現在 hello 網際網路從 VM 上開啟連接埠 80，您可以使用網頁瀏覽器，您的選擇 tooview hello 預設 IIS 歡迎使用頁面。</span><span class="sxs-lookup"><span data-stu-id="59360-143">With IIS installed and port 80 now open on your VM from hello Internet, you can use a web browser of your choice tooview hello default IIS welcome page.</span></span> <span data-ttu-id="59360-144">要確定 toouse hello *publicIpAddress*您 toovisit hello 預設頁面上面所記載。</span><span class="sxs-lookup"><span data-stu-id="59360-144">Be sure toouse hello *publicIpAddress* you documented above toovisit hello default page.</span></span> 

![IIS 預設網站](./media/quick-create-powershell/default-iis-website.png) 

## <a name="clean-up-resources"></a><span data-ttu-id="59360-146">清除資源</span><span class="sxs-lookup"><span data-stu-id="59360-146">Clean up resources</span></span>

<span data-ttu-id="59360-147">當不再需要您可以使用 hello[移除 AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup)命令 tooremove hello 資源群組、 VM 和所有相關的資源。</span><span class="sxs-lookup"><span data-stu-id="59360-147">When no longer needed, you can use hello [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="59360-148">後續步驟</span><span class="sxs-lookup"><span data-stu-id="59360-148">Next steps</span></span>

<span data-ttu-id="59360-149">在此快速入門中，您已部署簡單的虛擬機器、網路安全性群組規則，並已安裝 Web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="59360-149">In this quick start, you’ve deployed a simple virtual machine, a network security group rule, and installed a web server.</span></span> <span data-ttu-id="59360-150">進一步了解 Azure 虛擬機器，toolearn 繼續 toohello 教學課程適用於 Windows Vm。</span><span class="sxs-lookup"><span data-stu-id="59360-150">toolearn more about Azure virtual machines, continue toohello tutorial for Windows VMs.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="59360-151">Azure Windows 虛擬機器教學課程</span><span class="sxs-lookup"><span data-stu-id="59360-151">Azure Windows virtual machine tutorials</span></span>](./tutorial-manage-vm.md)
