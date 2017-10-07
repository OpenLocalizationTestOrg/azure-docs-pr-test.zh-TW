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
# <a name="how-toocustomize-a-windows-virtual-machine-in-azure"></a><span data-ttu-id="235a4-103">如何 toocustomize Azure 中的 Windows 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="235a4-103">How toocustomize a Windows virtual machine in Azure</span></span>
<span data-ttu-id="235a4-104">通常需要快速且一致的方式，某種形式的自動化 tooconfigure 虛擬機器 (Vm)。</span><span class="sxs-lookup"><span data-stu-id="235a4-104">tooconfigure virtual machines (VMs) in a quick and consistent manner, some form of automation is typically desired.</span></span> <span data-ttu-id="235a4-105">常見的方法 toocustomize Windows VM 是 toouse[自訂指令碼延伸的視窗](extensions-customscript.md)。</span><span class="sxs-lookup"><span data-stu-id="235a4-105">A common approach toocustomize a Windows VM is toouse [Custom Script Extension for Windows](extensions-customscript.md).</span></span> <span data-ttu-id="235a4-106">在本教學課程中，您了解如何：</span><span class="sxs-lookup"><span data-stu-id="235a4-106">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="235a4-107">使用 hello 自訂指令碼擴充 tooinstall IIS</span><span class="sxs-lookup"><span data-stu-id="235a4-107">Use hello Custom Script Extension tooinstall IIS</span></span>
> * <span data-ttu-id="235a4-108">建立 VM 使用 hello 自訂指令碼擴充</span><span class="sxs-lookup"><span data-stu-id="235a4-108">Create a VM that uses hello Custom Script Extension</span></span>
> * <span data-ttu-id="235a4-109">套用 hello 延伸之後，檢視正在執行的 IIS 站台</span><span class="sxs-lookup"><span data-stu-id="235a4-109">View a running IIS site after hello extension is applied</span></span>

<span data-ttu-id="235a4-110">本教學課程需要 hello Azure PowerShell 模組版本 3.6 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="235a4-110">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="235a4-111">執行` Get-Module -ListAvailable AzureRM`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="235a4-111">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="235a4-112">如果您需要 tooupgrade，請參閱[安裝 Azure PowerShell 模組](/powershell/azure/install-azurerm-ps)。</span><span class="sxs-lookup"><span data-stu-id="235a4-112">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>


## <a name="custom-script-extension-overview"></a><span data-ttu-id="235a4-113">自訂指令碼擴充功能概觀</span><span class="sxs-lookup"><span data-stu-id="235a4-113">Custom script extension overview</span></span>
<span data-ttu-id="235a4-114">hello 自訂指令碼擴充功能下載並在 Azure Vm 上執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="235a4-114">hello Custom Script Extension downloads and executes scripts on Azure VMs.</span></span> <span data-ttu-id="235a4-115">此擴充功能適用於部署後組態、軟體安裝或其他任何組態/管理工作。</span><span class="sxs-lookup"><span data-stu-id="235a4-115">This extension is useful for post deployment configuration, software installation, or any other configuration / management task.</span></span> <span data-ttu-id="235a4-116">可以從 Azure 儲存體或 GitHub 下載指令碼，或提供 toohello 在執行階段的延伸模組的 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="235a4-116">Scripts can be downloaded from Azure storage or GitHub, or provided toohello Azure portal at extension run time.</span></span>

<span data-ttu-id="235a4-117">hello 自訂指令碼擴充功能與整合 Azure 資源管理員範本，並也可以執行使用 hello Azure CLI、 PowerShell、 Azure 入口網站或 hello Azure 虛擬機器 REST API。</span><span class="sxs-lookup"><span data-stu-id="235a4-117">hello Custom Script extension integrates with Azure Resource Manager templates, and can also be run using hello Azure CLI, PowerShell, Azure portal, or hello Azure Virtual Machine REST API.</span></span>

<span data-ttu-id="235a4-118">您可以使用 Windows 和 Linux Vm 建立 hello 自訂指令碼擴充。</span><span class="sxs-lookup"><span data-stu-id="235a4-118">You can use hello Custom Script Extension with both Windows and Linux VMs.</span></span>


## <a name="create-virtual-machine"></a><span data-ttu-id="235a4-119">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="235a4-119">Create virtual machine</span></span>
<span data-ttu-id="235a4-120">建立 VM 之前，請先使用 [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) 來建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="235a4-120">Before you can create a VM, create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="235a4-121">hello 下列範例會建立名為的資源群組*myResourceGroupAutomate*在 hello *EastUS*位置：</span><span class="sxs-lookup"><span data-stu-id="235a4-121">hello following example creates a resource group named *myResourceGroupAutomate* in hello *EastUS* location:</span></span>

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroupAutomate -Location EastUS
```

<span data-ttu-id="235a4-122">設定系統管理員使用者名稱和密碼具有 hello Vm [Get-credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="235a4-122">Set an administrator username and password for hello VMs with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="235a4-123">現在您可以建立 hello 與 VM[新增 AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm)。</span><span class="sxs-lookup"><span data-stu-id="235a4-123">Now you can create hello VM with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="235a4-124">hello 下列範例會建立所需的 hello 虛擬網路的元件，hello 作業系統組態，然後建立名為的 VM *myVM*:</span><span class="sxs-lookup"><span data-stu-id="235a4-124">hello following example creates hello required virtual network components, hello OS configuration, and then creates a VM named *myVM*:</span></span>

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

<span data-ttu-id="235a4-125">花幾分鐘，讓 hello 資源和 VM toobe 建立。</span><span class="sxs-lookup"><span data-stu-id="235a4-125">It takes a few minutes for hello resources and VM toobe created.</span></span>


## <a name="automate-iis-install"></a><span data-ttu-id="235a4-126">自動安裝 IIS</span><span class="sxs-lookup"><span data-stu-id="235a4-126">Automate IIS install</span></span>
<span data-ttu-id="235a4-127">使用[組 AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall hello 自訂指令碼擴充。</span><span class="sxs-lookup"><span data-stu-id="235a4-127">Use [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall hello Custom Script Extension.</span></span> <span data-ttu-id="235a4-128">hello 延伸模組執行`powershell Add-WindowsFeature Web-Server`tooinstall hello IIS 網頁伺服器，然後再更新 hello *Default.htm*頁面 tooshow hello 主機名稱的 hello VM:</span><span class="sxs-lookup"><span data-stu-id="235a4-128">hello extension runs `powershell Add-WindowsFeature Web-Server` tooinstall hello IIS webserver and then updates hello *Default.htm* page tooshow hello hostname of hello VM:</span></span>

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


## <a name="test-web-site"></a><span data-ttu-id="235a4-129">測試網站</span><span class="sxs-lookup"><span data-stu-id="235a4-129">Test web site</span></span>
<span data-ttu-id="235a4-130">取得您的負載平衡器的 hello 公用 IP 位址[Get AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress)。</span><span class="sxs-lookup"><span data-stu-id="235a4-130">Obtain hello public IP address of your load balancer with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="235a4-131">hello 下列範例會取得 IP 位址 hello *myPublicIP*稍早建立：</span><span class="sxs-lookup"><span data-stu-id="235a4-131">hello following example obtains hello IP address for *myPublicIP* created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress `
    -ResourceGroupName myResourceGroupAutomate `
    -Name myPublicIP | select IpAddress
```

<span data-ttu-id="235a4-132">然後，您就可以 tooa 網頁瀏覽器中輸入 hello 公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="235a4-132">You can then enter hello public IP address in tooa web browser.</span></span> <span data-ttu-id="235a4-133">hello 網站將會顯示，包括 hello hello VM 主機名稱的 hello 負載平衡器分散流量 tooas hello 下列範例中：</span><span class="sxs-lookup"><span data-stu-id="235a4-133">hello website is displayed, including hello hostname of hello VM that hello load balancer distributed traffic tooas in hello following example:</span></span>

![執行中的 IIS 網站](./media/tutorial-automate-vm-deployment/running-iis-website.png)


## <a name="next-steps"></a><span data-ttu-id="235a4-135">後續步驟</span><span class="sxs-lookup"><span data-stu-id="235a4-135">Next steps</span></span>

<span data-ttu-id="235a4-136">在本教學課程中，您可以自動化的 hello 在 VM 安裝 IIS。</span><span class="sxs-lookup"><span data-stu-id="235a4-136">In this tutorial, you automated hello IIS install on a VM.</span></span> <span data-ttu-id="235a4-137">您已了解如何︰</span><span class="sxs-lookup"><span data-stu-id="235a4-137">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="235a4-138">使用 hello 自訂指令碼擴充 tooinstall IIS</span><span class="sxs-lookup"><span data-stu-id="235a4-138">Use hello Custom Script Extension tooinstall IIS</span></span>
> * <span data-ttu-id="235a4-139">建立 VM 使用 hello 自訂指令碼擴充</span><span class="sxs-lookup"><span data-stu-id="235a4-139">Create a VM that uses hello Custom Script Extension</span></span>
> * <span data-ttu-id="235a4-140">套用 hello 延伸之後，檢視正在執行的 IIS 站台</span><span class="sxs-lookup"><span data-stu-id="235a4-140">View a running IIS site after hello extension is applied</span></span>

<span data-ttu-id="235a4-141">如何前進 toohello 下一個教學課程 toolearn toocreate 自訂 VM 映像。</span><span class="sxs-lookup"><span data-stu-id="235a4-141">Advance toohello next tutorial toolearn how toocreate custom VM images.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="235a4-142">建立自訂的 VM 映像</span><span class="sxs-lookup"><span data-stu-id="235a4-142">Create custom VM images</span></span>](./tutorial-custom-images.md)
