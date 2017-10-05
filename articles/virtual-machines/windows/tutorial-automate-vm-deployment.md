---
title: "自訂 Azure 中的 Windows VM | Microsoft Docs"
description: "了解如何使用自訂指令碼擴充功能和 Key Vault 來自訂 Azure 中的 Windows VM"
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
ms.openlocfilehash: 3be58bf8afbcff018b2b0d69a0e08c2c9ab1fca7
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-customize-a-windows-virtual-machine-in-azure"></a><span data-ttu-id="ec0ed-103">如何自訂 Azure 中的 Windows 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="ec0ed-103">How to customize a Windows virtual machine in Azure</span></span>
<span data-ttu-id="ec0ed-104">若要以快速且一致的方式設定虛擬機器 (VM)，通常需要某種形式的自動化。</span><span class="sxs-lookup"><span data-stu-id="ec0ed-104">To configure virtual machines (VMs) in a quick and consistent manner, some form of automation is typically desired.</span></span> <span data-ttu-id="ec0ed-105">自訂 Windows VM 的常見方法是使用 [Windows 的自訂指令碼擴充功能](extensions-customscript.md)。</span><span class="sxs-lookup"><span data-stu-id="ec0ed-105">A common approach to customize a Windows VM is to use [Custom Script Extension for Windows](extensions-customscript.md).</span></span> <span data-ttu-id="ec0ed-106">在本教學課程中，您將了解如何：</span><span class="sxs-lookup"><span data-stu-id="ec0ed-106">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ec0ed-107">使用自訂指令碼擴充功能安裝 IIS</span><span class="sxs-lookup"><span data-stu-id="ec0ed-107">Use the Custom Script Extension to install IIS</span></span>
> * <span data-ttu-id="ec0ed-108">使用自訂指令碼擴充功能建立 VM</span><span class="sxs-lookup"><span data-stu-id="ec0ed-108">Create a VM that uses the Custom Script Extension</span></span>
> * <span data-ttu-id="ec0ed-109">套用擴充功能之後檢視執行中的 IIS 網站</span><span class="sxs-lookup"><span data-stu-id="ec0ed-109">View a running IIS site after the extension is applied</span></span>

<span data-ttu-id="ec0ed-110">本教學課程需要 Azure PowerShell 模組 3.6 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="ec0ed-110">This tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="ec0ed-111">執行 ` Get-Module -ListAvailable AzureRM` 以尋找版本。</span><span class="sxs-lookup"><span data-stu-id="ec0ed-111">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="ec0ed-112">如果您需要升級，請參閱[安裝 Azure PowerShell 模組](/powershell/azure/install-azurerm-ps)。</span><span class="sxs-lookup"><span data-stu-id="ec0ed-112">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>


## <a name="custom-script-extension-overview"></a><span data-ttu-id="ec0ed-113">自訂指令碼擴充功能概觀</span><span class="sxs-lookup"><span data-stu-id="ec0ed-113">Custom script extension overview</span></span>
<span data-ttu-id="ec0ed-114">自訂指令碼擴充功能會在 Azure VM 上下載並執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="ec0ed-114">The Custom Script Extension downloads and executes scripts on Azure VMs.</span></span> <span data-ttu-id="ec0ed-115">此擴充功能適用於部署後組態、軟體安裝或其他任何組態/管理工作。</span><span class="sxs-lookup"><span data-stu-id="ec0ed-115">This extension is useful for post deployment configuration, software installation, or any other configuration / management task.</span></span> <span data-ttu-id="ec0ed-116">您可以從 Azure 儲存體或 GitHub 下載指令碼，或是在擴充功能執行階段將指令碼提供給 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="ec0ed-116">Scripts can be downloaded from Azure storage or GitHub, or provided to the Azure portal at extension run time.</span></span>

<span data-ttu-id="ec0ed-117">「自訂指令碼擴充功能」會與 Azure Resource Manager 範本整合，您也可以使用 Azure CLI、PowerShell、Azure 入口網站或「Azure 虛擬機器 REST API」來執行它。</span><span class="sxs-lookup"><span data-stu-id="ec0ed-117">The Custom Script extension integrates with Azure Resource Manager templates, and can also be run using the Azure CLI, PowerShell, Azure portal, or the Azure Virtual Machine REST API.</span></span>

<span data-ttu-id="ec0ed-118">您可以搭配 Windows 和 Linux VM 使用自訂指令碼擴充功能。</span><span class="sxs-lookup"><span data-stu-id="ec0ed-118">You can use the Custom Script Extension with both Windows and Linux VMs.</span></span>


## <a name="create-virtual-machine"></a><span data-ttu-id="ec0ed-119">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="ec0ed-119">Create virtual machine</span></span>
<span data-ttu-id="ec0ed-120">建立 VM 之前，請先使用 [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) 來建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="ec0ed-120">Before you can create a VM, create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="ec0ed-121">下列範例會在 EastUS 位置建立名為 myResourceGroupAutomate 的資源群組：</span><span class="sxs-lookup"><span data-stu-id="ec0ed-121">The following example creates a resource group named *myResourceGroupAutomate* in the *EastUS* location:</span></span>

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroupAutomate -Location EastUS
```

<span data-ttu-id="ec0ed-122">使用 [Get-credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential) 來設定 VM 的系統管理員使用者名稱和密碼：</span><span class="sxs-lookup"><span data-stu-id="ec0ed-122">Set an administrator username and password for the VMs with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="ec0ed-123">現在您可以使用 [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) 建立 VM。</span><span class="sxs-lookup"><span data-stu-id="ec0ed-123">Now you can create the VM with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="ec0ed-124">下列範例會建立必要的虛擬網路元件、作業系統設定，然後建立名為 myVM 的 VM：</span><span class="sxs-lookup"><span data-stu-id="ec0ed-124">The following example creates the required virtual network components, the OS configuration, and then creates a VM named *myVM*:</span></span>

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

<span data-ttu-id="ec0ed-125">系統需要花幾分鐘的時間來建立資源和 VM。</span><span class="sxs-lookup"><span data-stu-id="ec0ed-125">It takes a few minutes for the resources and VM to be created.</span></span>


## <a name="automate-iis-install"></a><span data-ttu-id="ec0ed-126">自動安裝 IIS</span><span class="sxs-lookup"><span data-stu-id="ec0ed-126">Automate IIS install</span></span>
<span data-ttu-id="ec0ed-127">使用 [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) 來安裝自訂指令碼擴充功能。</span><span class="sxs-lookup"><span data-stu-id="ec0ed-127">Use [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) to install the Custom Script Extension.</span></span> <span data-ttu-id="ec0ed-128">擴充功能會執行 `powershell Add-WindowsFeature Web-Server` 以安裝 IIS Web 伺服器，然後更新 Default.htm 頁面以顯示 VM 的主機名稱：</span><span class="sxs-lookup"><span data-stu-id="ec0ed-128">The extension runs `powershell Add-WindowsFeature Web-Server` to install the IIS webserver and then updates the *Default.htm* page to show the hostname of the VM:</span></span>

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


## <a name="test-web-site"></a><span data-ttu-id="ec0ed-129">測試網站</span><span class="sxs-lookup"><span data-stu-id="ec0ed-129">Test web site</span></span>
<span data-ttu-id="ec0ed-130">使用 [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) 取得負載平衡器的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="ec0ed-130">Obtain the public IP address of your load balancer with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="ec0ed-131">下列範例會取得稍早建立的 myPublicIP IP 位址︰</span><span class="sxs-lookup"><span data-stu-id="ec0ed-131">The following example obtains the IP address for *myPublicIP* created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress `
    -ResourceGroupName myResourceGroupAutomate `
    -Name myPublicIP | select IpAddress
```

<span data-ttu-id="ec0ed-132">接著，您可以在 Web 瀏覽器中輸入公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="ec0ed-132">You can then enter the public IP address in to a web browser.</span></span> <span data-ttu-id="ec0ed-133">網站隨即顯示，包括負載平衡器分散流量之 VM 的主機名稱，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="ec0ed-133">The website is displayed, including the hostname of the VM that the load balancer distributed traffic to as in the following example:</span></span>

![執行中的 IIS 網站](./media/tutorial-automate-vm-deployment/running-iis-website.png)


## <a name="next-steps"></a><span data-ttu-id="ec0ed-135">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ec0ed-135">Next steps</span></span>

<span data-ttu-id="ec0ed-136">在本教學課程中，您將 VM 上的 IIS 安裝自動化。</span><span class="sxs-lookup"><span data-stu-id="ec0ed-136">In this tutorial, you automated the IIS install on a VM.</span></span> <span data-ttu-id="ec0ed-137">您已了解如何︰</span><span class="sxs-lookup"><span data-stu-id="ec0ed-137">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ec0ed-138">使用自訂指令碼擴充功能安裝 IIS</span><span class="sxs-lookup"><span data-stu-id="ec0ed-138">Use the Custom Script Extension to install IIS</span></span>
> * <span data-ttu-id="ec0ed-139">使用自訂指令碼擴充功能建立 VM</span><span class="sxs-lookup"><span data-stu-id="ec0ed-139">Create a VM that uses the Custom Script Extension</span></span>
> * <span data-ttu-id="ec0ed-140">套用擴充功能之後檢視執行中的 IIS 網站</span><span class="sxs-lookup"><span data-stu-id="ec0ed-140">View a running IIS site after the extension is applied</span></span>

<span data-ttu-id="ec0ed-141">前進至下一個教學課程，以了解如何建立自訂的 VM 映像。</span><span class="sxs-lookup"><span data-stu-id="ec0ed-141">Advance to the next tutorial to learn how to create custom VM images.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ec0ed-142">建立自訂的 VM 映像</span><span class="sxs-lookup"><span data-stu-id="ec0ed-142">Create custom VM images</span></span>](./tutorial-custom-images.md)
