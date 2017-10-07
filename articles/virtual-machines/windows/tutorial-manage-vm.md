---
title: "aaaCreate 和管理 Windows Vm hello Azure PowerShell 模組 |Microsoft 文件"
description: "教學課程-建立和管理 Windows Vm 與 hello Azure PowerShell 模組"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 20adcb673ef4de683e6ad82d048a9625a1dc838c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-windows-vms-with-hello-azure-powershell-module"></a><span data-ttu-id="caeff-103">建立和管理 Windows Vm 與 hello Azure PowerShell 模組</span><span class="sxs-lookup"><span data-stu-id="caeff-103">Create and Manage Windows VMs with hello Azure PowerShell module</span></span>

<span data-ttu-id="caeff-104">Azure 虛擬機器提供完全可設定且彈性的計算環境。</span><span class="sxs-lookup"><span data-stu-id="caeff-104">Azure virtual machines provide a fully configurable and flexible computing environment.</span></span> <span data-ttu-id="caeff-105">本教學課程涵蓋基本的「Azure 虛擬機器」部署項目，例如選取 VM 大小、選取 VM 映像、部署 VM。</span><span class="sxs-lookup"><span data-stu-id="caeff-105">This tutorial covers basic Azure virtual machine deployment items such as selecting a VM size, selecting a VM image, and deploying a VM.</span></span> <span data-ttu-id="caeff-106">您會了解如何：</span><span class="sxs-lookup"><span data-stu-id="caeff-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="caeff-107">建立和連線 tooa VM</span><span class="sxs-lookup"><span data-stu-id="caeff-107">Create and connect tooa VM</span></span>
> * <span data-ttu-id="caeff-108">選取及使用 VM 映像</span><span class="sxs-lookup"><span data-stu-id="caeff-108">Select and use VM images</span></span>
> * <span data-ttu-id="caeff-109">檢視及使用特定 VM 大小</span><span class="sxs-lookup"><span data-stu-id="caeff-109">View and use specific VM sizes</span></span>
> * <span data-ttu-id="caeff-110">調整 VM 的大小</span><span class="sxs-lookup"><span data-stu-id="caeff-110">Resize a VM</span></span>
> * <span data-ttu-id="caeff-111">檢視及了解 VM 狀態</span><span class="sxs-lookup"><span data-stu-id="caeff-111">View and understand VM state</span></span>

<span data-ttu-id="caeff-112">本教學課程需要 hello Azure PowerShell 模組版本 3.6 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="caeff-112">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="caeff-113">執行` Get-Module -ListAvailable AzureRM`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="caeff-113">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="caeff-114">如果您需要 tooupgrade，請參閱[安裝 Azure PowerShell 模組](/powershell/azure/install-azurerm-ps)。</span><span class="sxs-lookup"><span data-stu-id="caeff-114">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="create-resource-group"></a><span data-ttu-id="caeff-115">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="caeff-115">Create resource group</span></span>

<span data-ttu-id="caeff-116">建立資源群組以 hello[新增 AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup)命令。</span><span class="sxs-lookup"><span data-stu-id="caeff-116">Create a resource group with hello [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) command.</span></span> 

<span data-ttu-id="caeff-117">Azure 資源群組是在其中部署與管理 Azure 資源的邏輯容器。</span><span class="sxs-lookup"><span data-stu-id="caeff-117">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="caeff-118">資源群組必須在虛擬機器之前建立。</span><span class="sxs-lookup"><span data-stu-id="caeff-118">A resource group must be created before a virtual machine.</span></span> <span data-ttu-id="caeff-119">在此範例中，資源群組命名為*myResourceGroupVM*會建立在 hello *EastUS*區域。</span><span class="sxs-lookup"><span data-stu-id="caeff-119">In this example, a resource group named *myResourceGroupVM* is created in hello *EastUS* region.</span></span> 

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroupVM -Location EastUS
```

<span data-ttu-id="caeff-120">建立或修改 VM，能看到本教學課程時，所指定 hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="caeff-120">hello resource group is specified when creating or modifying a VM, which can be seen throughout this tutorial.</span></span>

## <a name="create-virtual-machine"></a><span data-ttu-id="caeff-121">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="caeff-121">Create virtual machine</span></span>

<span data-ttu-id="caeff-122">虛擬機器必須連接的 tooa 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="caeff-122">A virtual machine must be connected tooa virtual network.</span></span> <span data-ttu-id="caeff-123">您與 hello 透過網路介面卡使用的公用 IP 位址的虛擬機器進行通訊。</span><span class="sxs-lookup"><span data-stu-id="caeff-123">You communicate with hello virtual machine using a public IP address through a network interface card.</span></span>

### <a name="create-virtual-network"></a><span data-ttu-id="caeff-124">建立虛擬網路</span><span class="sxs-lookup"><span data-stu-id="caeff-124">Create virtual network</span></span>

<span data-ttu-id="caeff-125">使用 [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) 建立子網路：</span><span class="sxs-lookup"><span data-stu-id="caeff-125">Create a subnet with [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig):</span></span>

```powershell
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24
```

<span data-ttu-id="caeff-126">使用 [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) 建立虛擬網路：</span><span class="sxs-lookup"><span data-stu-id="caeff-126">Create a virtual network with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork):</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroupVM `
  -Location EastUS `
  -Name myVnet `
  -AddressPrefix 192.168.0.0/16 ` 
  -Subnet $subnetConfig
```
### <a name="create-public-ip-address"></a><span data-ttu-id="caeff-127">建立公用 IP 位址</span><span class="sxs-lookup"><span data-stu-id="caeff-127">Create public IP address</span></span>

<span data-ttu-id="caeff-128">使用 [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) 建立公用 IP 位址：</span><span class="sxs-lookup"><span data-stu-id="caeff-128">Create a public IP address with [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress):</span></span>

```powershell
$pip = New-AzureRmPublicIpAddress ` 
  -ResourceGroupName myResourceGroupVM `
  -Location EastUS ` 
  -AllocationMethod Static `
  -Name myPublicIPAddress
```

### <a name="create-network-interface-card"></a><span data-ttu-id="caeff-129">建立網路介面卡</span><span class="sxs-lookup"><span data-stu-id="caeff-129">Create network interface card</span></span>

<span data-ttu-id="caeff-130">使用 [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) 建立網路介面卡：</span><span class="sxs-lookup"><span data-stu-id="caeff-130">Create a network interface card with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface):</span></span>

```powershell
$nic = New-AzureRmNetworkInterface `
  -ResourceGroupName myResourceGroupVM  `
  -Location EastUS `
  -Name myNic `
  -SubnetId $vnet.Subnets[0].Id `
  -PublicIpAddressId $pip.Id
```

### <a name="create-network-security-group"></a><span data-ttu-id="caeff-131">建立網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="caeff-131">Create network security group</span></span>

<span data-ttu-id="caeff-132">Azure [網路安全性群組](../../virtual-network/virtual-networks-nsg.md) (NSG) 控制一或多部虛擬機器的輸入和傳出流量。</span><span class="sxs-lookup"><span data-stu-id="caeff-132">An Azure [network security group](../../virtual-network/virtual-networks-nsg.md) (NSG) controls inbound and outbound traffic for one or many virtual machines.</span></span> <span data-ttu-id="caeff-133">網路安全性群組規則可允許或拒絕特定連接埠或連接埠範圍上的網路流量。</span><span class="sxs-lookup"><span data-stu-id="caeff-133">Network security group rules allow or deny network traffic on a specific port or port range.</span></span> <span data-ttu-id="caeff-134">這些規則也可以包含來源位址首碼，所以只有在預先定義的來源產生的流量可以與虛擬機器通訊。</span><span class="sxs-lookup"><span data-stu-id="caeff-134">These rules can also include a source address prefix so that only traffic originating at a predefined source can communicate with a virtual machine.</span></span> <span data-ttu-id="caeff-135">tooaccess hello IIS web 伺服器上所安裝，您必須將輸入的 NSG 規則。</span><span class="sxs-lookup"><span data-stu-id="caeff-135">tooaccess hello IIS webserver that you are installing, you must add an inbound NSG rule.</span></span>

<span data-ttu-id="caeff-136">toocreate 輸入 NSG 規則，使用[新增 AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/add-azurermnetworksecurityruleconfig)。</span><span class="sxs-lookup"><span data-stu-id="caeff-136">toocreate an inbound NSG rule, use [Add-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/add-azurermnetworksecurityruleconfig).</span></span> <span data-ttu-id="caeff-137">hello 下列範例會建立名為 NSG 規則*myNSGRule*的開啟連接埠*3389* hello 虛擬機器：</span><span class="sxs-lookup"><span data-stu-id="caeff-137">hello following example creates an NSG rule named *myNSGRule* that opens port *3389* for hello virtual machine:</span></span>

```powershell
$nsgRule = New-AzureRmNetworkSecurityRuleConfig `
  -Name myNSGRule `
  -Protocol Tcp `
  -Direction Inbound `
  -Priority 1000 `
  -SourceAddressPrefix * `
  -SourcePortRange * `
  -DestinationAddressPrefix * `
  -DestinationPortRange 3389 `
  -Access Allow
```

<span data-ttu-id="caeff-138">建立 hello NSG 使用*myNSGRule*與[新增 AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup):</span><span class="sxs-lookup"><span data-stu-id="caeff-138">Create hello NSG using *myNSGRule* with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup):</span></span>

```powershell
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName myResourceGroupVM `
    -Location EastUS `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRule
```

<span data-ttu-id="caeff-139">Hello 虛擬網路中新增子網路-NSG toohello hello[組 AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig):</span><span class="sxs-lookup"><span data-stu-id="caeff-139">Add hello NSG toohello subnet in hello virtual network with [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig):</span></span>

```powershell
Set-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -VirtualNetwork $vnet `
    -NetworkSecurityGroup $nsg `
    -AddressPrefix 192.168.1.0/24
```

<span data-ttu-id="caeff-140">更新 hello 虛擬網路與[組 AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork):</span><span class="sxs-lookup"><span data-stu-id="caeff-140">Update hello virtual network with [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork):</span></span>

```powershell
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```

### <a name="create-virtual-machine"></a><span data-ttu-id="caeff-141">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="caeff-141">Create virtual machine</span></span>

<span data-ttu-id="caeff-142">建立虛擬機器時，有數個可用的選項，例如作業系統映像、磁碟大小及系統管理認證。</span><span class="sxs-lookup"><span data-stu-id="caeff-142">When creating a virtual machine, several options are available such as operating system image, disk sizing, and administrative credentials.</span></span> <span data-ttu-id="caeff-143">在此範例中，虛擬機器會建立名稱為*myVM*執行 hello 最新版本的 Windows Server 2016 資料中心。</span><span class="sxs-lookup"><span data-stu-id="caeff-143">In this example, a virtual machine is created with a name of *myVM* running hello latest version of Windows Server 2016 Datacenter.</span></span>

<span data-ttu-id="caeff-144">設定 hello 使用者名稱和密碼所需的 hello 與 hello 虛擬機器上的系統管理員帳戶[Get-credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="caeff-144">Set hello username and password needed for hello administrator account on hello virtual machine with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="caeff-145">建立 hello hello 的虛擬機器的初始設定[新增 AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig):</span><span class="sxs-lookup"><span data-stu-id="caeff-145">Create hello initial configuration for hello virtual machine with [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig):</span></span>

```powershell
$vm = New-AzureRmVMConfig -VMName myVM -VMSize Standard_D1
```

<span data-ttu-id="caeff-146">新增 hello 資訊 toohello 虛擬機器設定作業系統[組 AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem):</span><span class="sxs-lookup"><span data-stu-id="caeff-146">Add hello operating system information toohello virtual machine configuration with [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem):</span></span>

```powershell
$vm = Set-AzureRmVMOperatingSystem `
    -VM $vm `
    -Windows `
    -ComputerName myVM `
    -Credential $cred `
    -ProvisionVMAgent -EnableAutoUpdate
```

<span data-ttu-id="caeff-147">新增 hello 映像 toohello 虛擬機器組態資訊與[組 AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage):</span><span class="sxs-lookup"><span data-stu-id="caeff-147">Add hello image information toohello virtual machine configuration with [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage):</span></span>

```powershell
$vm = Set-AzureRmVMSourceImage `
    -VM $vm `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter `
    -Version latest
```

<span data-ttu-id="caeff-148">新增 hello 作業系統磁碟設定 toohello 虛擬機器組態[組 AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk):</span><span class="sxs-lookup"><span data-stu-id="caeff-148">Add hello operating system disk settings toohello virtual machine configuration with [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk):</span></span>

```powershell
$vm = Set-AzureRmVMOSDisk `
    -VM $vm `
    -Name myOsDisk `
    -DiskSizeInGB 128 `
    -CreateOption FromImage `
    -Caching ReadWrite
```

<span data-ttu-id="caeff-149">新增 hello 網路介面卡，您先前建立的虛擬機器組態 toohello[新增 AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="caeff-149">Add hello network interface card that you previously created toohello virtual machine configuration with [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span></span>

```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

<span data-ttu-id="caeff-150">建立虛擬機器 hello[新增 AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm)。</span><span class="sxs-lookup"><span data-stu-id="caeff-150">Create hello virtual machine with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span>

```powershell
New-AzureRmVM -ResourceGroupName myResourceGroupVM -Location EastUS -VM $vm
```

## <a name="connect-toovm"></a><span data-ttu-id="caeff-151">連接 tooVM</span><span class="sxs-lookup"><span data-stu-id="caeff-151">Connect tooVM</span></span>

<span data-ttu-id="caeff-152">Hello 部署已完成之後，請使用 hello 的虛擬機器建立遠端桌面連線。</span><span class="sxs-lookup"><span data-stu-id="caeff-152">After hello deployment has completed, create a remote desktop connection with hello virtual machine.</span></span>

<span data-ttu-id="caeff-153">執行下列命令 tooreturn hello 公用 IP 位址的 hello 虛擬機器的 hello。</span><span class="sxs-lookup"><span data-stu-id="caeff-153">Run hello following commands tooreturn hello public IP address of hello virtual machine.</span></span> <span data-ttu-id="caeff-154">記下此 IP 位址，讓您能連接 tooit 與您的瀏覽器 tootest web 連線，在未來的步驟。</span><span class="sxs-lookup"><span data-stu-id="caeff-154">Take note of this IP Address so you can connect tooit with your browser tootest web connectivity in a future step.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName myResourceGroupVM  | Select IpAddress
```

<span data-ttu-id="caeff-155">使用 hello 下列命令 toocreate 與 hello 虛擬機器的遠端桌面工作階段。</span><span class="sxs-lookup"><span data-stu-id="caeff-155">Use hello following command toocreate a remote desktop session with hello virtual machine.</span></span> <span data-ttu-id="caeff-156">Hello IP 位址取代成 hello *publicIPAddress*的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="caeff-156">Replace hello IP address with hello *publicIPAddress* of your virtual machine.</span></span> <span data-ttu-id="caeff-157">出現提示時，輸入 hello 建立 hello 虛擬機器時使用的認證。</span><span class="sxs-lookup"><span data-stu-id="caeff-157">When prompted, enter hello credentials used when creating hello virtual machine.</span></span>

```powershell
mstsc /v:<publicIpAddress>
```

## <a name="understand-vm-images"></a><span data-ttu-id="caeff-158">了解 VM 映像</span><span class="sxs-lookup"><span data-stu-id="caeff-158">Understand VM images</span></span>

<span data-ttu-id="caeff-159">hello Azure marketplace 包括許多可以使用的 toocreate 新的虛擬機器的虛擬機器映像。</span><span class="sxs-lookup"><span data-stu-id="caeff-159">hello Azure marketplace includes many virtual machine images that can be used toocreate a new virtual machine.</span></span> <span data-ttu-id="caeff-160">在 hello 先前步驟中，已使用 hello Windows Server 2016 資料中心映像建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="caeff-160">In hello previous steps, a virtual machine was created using hello Windows Server 2016-Datacenter image.</span></span> <span data-ttu-id="caeff-161">在此步驟中，會使用的 toosearch hello marketplace 中的其他 Windows 映像，適用於新的 Vm 也可以做為基底 hello PowerShell 模組。</span><span class="sxs-lookup"><span data-stu-id="caeff-161">In this step, hello PowerShell module is used toosearch hello marketplace for other Windows images, which can also as a base for new VMs.</span></span> <span data-ttu-id="caeff-162">這個程序包含尋找 hello 發行者、 提供項目和 hello 映像名稱 (Sku)。</span><span class="sxs-lookup"><span data-stu-id="caeff-162">This process consists of finding hello publisher, offer, and hello image name (Sku).</span></span> 

<span data-ttu-id="caeff-163">使用 hello [Get AzureRmVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher)命令 tooreturn 映像的發行者清單。</span><span class="sxs-lookup"><span data-stu-id="caeff-163">Use hello [Get-AzureRmVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher) command tooreturn a list of image publishers.</span></span>  

```powersehll
Get-AzureRmVMImagePublisher -Location "EastUS"
```

<span data-ttu-id="caeff-164">使用 hello [Get AzureRmVMImageOffer](/powershell/module/azurerm.compute/get-azurermvmimageoffer) tooreturn 映像優惠清單。</span><span class="sxs-lookup"><span data-stu-id="caeff-164">Use hello [Get-AzureRmVMImageOffer](/powershell/module/azurerm.compute/get-azurermvmimageoffer) tooreturn a list of image offers.</span></span> <span data-ttu-id="caeff-165">利用這個命令，hello 傳回 hello 指定 「 發行者 」 上篩選清單。</span><span class="sxs-lookup"><span data-stu-id="caeff-165">With this command, hello returned list is filtered on hello specified publisher.</span></span> 

```powershell
Get-AzureRmVMImageOffer -Location "EastUS" -PublisherName "MicrosoftWindowsServer"
```

```powershell
Offer             PublisherName          Location
-----             -------------          -------- 
Windows-HUB       MicrosoftWindowsServer EastUS 
WindowsServer     MicrosoftWindowsServer EastUS   
WindowsServer-HUB MicrosoftWindowsServer EastUS   
```

<span data-ttu-id="caeff-166">hello [Get AzureRmVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku)命令將會接著篩選 hello 發行者和供應項目名稱 tooreturn 上的映像名稱清單。</span><span class="sxs-lookup"><span data-stu-id="caeff-166">hello [Get-AzureRmVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku) command will then filter on hello publisher and offer name tooreturn a list of image names.</span></span>

```powershell
Get-AzureRmVMImageSku -Location "EastUS" -PublisherName "MicrosoftWindowsServer" -Offer "WindowsServer"
```

```powershell
Skus                            Offer         PublisherName          Location
----                            -----         -------------          --------
2008-R2-SP1                     WindowsServer MicrosoftWindowsServer EastUS  
2008-R2-SP1-BYOL                WindowsServer MicrosoftWindowsServer EastUS  
2012-Datacenter                 WindowsServer MicrosoftWindowsServer EastUS  
2012-Datacenter-BYOL            WindowsServer MicrosoftWindowsServer EastUS  
2012-R2-Datacenter              WindowsServer MicrosoftWindowsServer EastUS  
2012-R2-Datacenter-BYOL         WindowsServer MicrosoftWindowsServer EastUS  
2016-Datacenter                 WindowsServer MicrosoftWindowsServer EastUS  
2016-Datacenter-Server-Core     WindowsServer MicrosoftWindowsServer EastUS  
2016-Datacenter-with-Containers WindowsServer MicrosoftWindowsServer EastUS  
2016-Nano-Server                WindowsServer MicrosoftWindowsServer EastUS
```

<span data-ttu-id="caeff-167">這項資訊可以使用的 toodeploy 具有特定的映像的 VM。</span><span class="sxs-lookup"><span data-stu-id="caeff-167">This information can be used toodeploy a VM with a specific image.</span></span> <span data-ttu-id="caeff-168">這個範例 hello VM 物件上設定 hello 映像名稱。</span><span class="sxs-lookup"><span data-stu-id="caeff-168">This example sets hello image name on hello VM object.</span></span> <span data-ttu-id="caeff-169">在本教學課程的完整的部署步驟，請參閱 toohello 前面的範例。</span><span class="sxs-lookup"><span data-stu-id="caeff-169">Refer toohello previous examples in this tutorial for complete deployment steps.</span></span>

```powershell
$vm = Set-AzureRmVMSourceImage `
    -VM $vm `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter-with-Containers `
    -Version latest
```

## <a name="understand-vm-sizes"></a><span data-ttu-id="caeff-170">了解 VM 大小</span><span class="sxs-lookup"><span data-stu-id="caeff-170">Understand VM sizes</span></span>

<span data-ttu-id="caeff-171">虛擬機器大小會決定 hello 量，例如 CPU、 GPU，以及記憶體都會提供 toohello 虛擬機器的計算資源。</span><span class="sxs-lookup"><span data-stu-id="caeff-171">A virtual machine size determines hello amount of compute resources such as CPU, GPU, and memory that are made available toohello virtual machine.</span></span> <span data-ttu-id="caeff-172">虛擬機器必須 toobe 建立大小適當的 hello 預期工作負載。</span><span class="sxs-lookup"><span data-stu-id="caeff-172">Virtual machines need toobe created with a size appropriate for hello expect work load.</span></span> <span data-ttu-id="caeff-173">如果工作負載增加，可以調整現有虛擬機器的大小。</span><span class="sxs-lookup"><span data-stu-id="caeff-173">If workload increases, an existing virtual machine can be resized.</span></span>

### <a name="vm-sizes"></a><span data-ttu-id="caeff-174">VM 大小</span><span class="sxs-lookup"><span data-stu-id="caeff-174">VM Sizes</span></span>

<span data-ttu-id="caeff-175">下表中的 hello 將大小分類成使用案例。</span><span class="sxs-lookup"><span data-stu-id="caeff-175">hello following table categorizes sizes into use cases.</span></span>  

| <span data-ttu-id="caeff-176">類型</span><span class="sxs-lookup"><span data-stu-id="caeff-176">Type</span></span>                     | <span data-ttu-id="caeff-177">大小</span><span class="sxs-lookup"><span data-stu-id="caeff-177">Sizes</span></span>           |    <span data-ttu-id="caeff-178">說明</span><span class="sxs-lookup"><span data-stu-id="caeff-178">Description</span></span>       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="caeff-179">一般用途</span><span class="sxs-lookup"><span data-stu-id="caeff-179">General purpose</span></span>         |<span data-ttu-id="caeff-180">DSv2、Dv2、DS、D、Av2、A0-7</span><span class="sxs-lookup"><span data-stu-id="caeff-180">DSv2, Dv2, DS, D, Av2, A0-7</span></span>| <span data-ttu-id="caeff-181">平衡的 CPU 對記憶體。</span><span class="sxs-lookup"><span data-stu-id="caeff-181">Balanced CPU-to-memory.</span></span> <span data-ttu-id="caeff-182">適用於開發 / 測試及小型 toomedium 應用程式和資料解決方案。</span><span class="sxs-lookup"><span data-stu-id="caeff-182">Ideal for dev / test and small toomedium applications and data solutions.</span></span>  |
| <span data-ttu-id="caeff-183">計算最佳化</span><span class="sxs-lookup"><span data-stu-id="caeff-183">Compute optimized</span></span>      | <span data-ttu-id="caeff-184">Fs、F</span><span class="sxs-lookup"><span data-stu-id="caeff-184">Fs, F</span></span>             | <span data-ttu-id="caeff-185">CPU 與記憶體的比例高。</span><span class="sxs-lookup"><span data-stu-id="caeff-185">High CPU-to-memory.</span></span> <span data-ttu-id="caeff-186">適用於中流量應用程式、網路設備及批次處理。</span><span class="sxs-lookup"><span data-stu-id="caeff-186">Good for medium traffic applications, network appliances, and batch processes.</span></span>        |
| <span data-ttu-id="caeff-187">記憶體最佳化</span><span class="sxs-lookup"><span data-stu-id="caeff-187">Memory optimized</span></span>       | <span data-ttu-id="caeff-188">GS、G、DSv2、DS、Dv2、D</span><span class="sxs-lookup"><span data-stu-id="caeff-188">GS, G, DSv2, DS, Dv2, D</span></span>   | <span data-ttu-id="caeff-189">記憶體與核心的比例高。</span><span class="sxs-lookup"><span data-stu-id="caeff-189">High memory-to-core.</span></span> <span data-ttu-id="caeff-190">太棒了關聯式資料庫、 中度 toolarge 快取，以及記憶體中分析。</span><span class="sxs-lookup"><span data-stu-id="caeff-190">Great for relational databases, medium toolarge caches, and in-memory analytics.</span></span>                 |
| <span data-ttu-id="caeff-191">儲存體最佳化</span><span class="sxs-lookup"><span data-stu-id="caeff-191">Storage optimized</span></span>       | <span data-ttu-id="caeff-192">Ls</span><span class="sxs-lookup"><span data-stu-id="caeff-192">Ls</span></span>                | <span data-ttu-id="caeff-193">高磁碟輸送量及 IO。</span><span class="sxs-lookup"><span data-stu-id="caeff-193">High disk throughput and IO.</span></span> <span data-ttu-id="caeff-194">適用於巨量資料、SQL 及 NoSQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="caeff-194">Ideal for Big Data, SQL, and NoSQL databases.</span></span>                                                         |
| <span data-ttu-id="caeff-195">GPU</span><span class="sxs-lookup"><span data-stu-id="caeff-195">GPU</span></span>           | <span data-ttu-id="caeff-196">NV、NC</span><span class="sxs-lookup"><span data-stu-id="caeff-196">NV, NC</span></span>            | <span data-ttu-id="caeff-197">以大量圖形轉譯和影片編輯為目標的特製化 VM。</span><span class="sxs-lookup"><span data-stu-id="caeff-197">Specialized VMs targeted for heavy graphic rendering and video editing.</span></span>       |
| <span data-ttu-id="caeff-198">高效能</span><span class="sxs-lookup"><span data-stu-id="caeff-198">High performance</span></span> | <span data-ttu-id="caeff-199">H、A8-11</span><span class="sxs-lookup"><span data-stu-id="caeff-199">H, A8-11</span></span>          | <span data-ttu-id="caeff-200">我們的最強大 CPU VM，可搭配選用的高輸送量網路介面 (RDMA)。</span><span class="sxs-lookup"><span data-stu-id="caeff-200">Our most powerful CPU VMs with optional high-throughput network interfaces (RDMA).</span></span> 


### <a name="find-available-vm-sizes"></a><span data-ttu-id="caeff-201">尋找可用的 VM 大小</span><span class="sxs-lookup"><span data-stu-id="caeff-201">Find available VM sizes</span></span>

<span data-ttu-id="caeff-202">在特定區域大小可用 toosee VM 的清單，請使用 hello [Get AzureRmVMSize](/powershell/module/azurerm.compute/get-azurermvmsize)命令。</span><span class="sxs-lookup"><span data-stu-id="caeff-202">toosee a list of VM sizes available in a particular region, use hello [Get-AzureRmVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) command.</span></span>

```powershell
Get-AzureRmVMSize -Location EastUS
```

## <a name="resize-a-vm"></a><span data-ttu-id="caeff-203">調整 VM 的大小</span><span class="sxs-lookup"><span data-stu-id="caeff-203">Resize a VM</span></span>

<span data-ttu-id="caeff-204">已部署 VM 之後，它可以是調整過大小的 tooincrease 或減少資源配置。</span><span class="sxs-lookup"><span data-stu-id="caeff-204">After a VM has been deployed, it can be resized tooincrease or decrease resource allocation.</span></span>

<span data-ttu-id="caeff-205">之前調整 VM 大小時，請檢查 hello 所需的大小是否可以使用 hello 目前 VM 的叢集。</span><span class="sxs-lookup"><span data-stu-id="caeff-205">Before resizing a VM, check if hello desired size is available on hello current VM cluster.</span></span> <span data-ttu-id="caeff-206">hello [Get AzureRmVMSize](/powershell/module/azurerm.compute/get-azurermvmsize)命令會傳回大小的清單。</span><span class="sxs-lookup"><span data-stu-id="caeff-206">hello [Get-AzureRmVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) command returns a list of sizes.</span></span> 

```powershell
Get-AzureRmVMSize -ResourceGroupName myResourceGroupVM -VMName myVM 
```

<span data-ttu-id="caeff-207">如果 hello 所需的大小是可用，hello VM 可以調整大小，從開機的狀態，不過 hello 作業期間重新開機。</span><span class="sxs-lookup"><span data-stu-id="caeff-207">If hello desired size is available, hello VM can be resized from a powered-on state, however it is rebooted during hello operation.</span></span>

```powershell
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroupVM  -VMName myVM 
$vm.HardwareProfile.VmSize = "Standard_D4"
Update-AzureRmVM -VM $vm -ResourceGroupName myResourceGroupVM 
```

<span data-ttu-id="caeff-208">如果 hello 所需的大小不 hello 目前在叢集上，hello VM toobe hello 的調整大小作業之前取消配置可能會發生的需求。</span><span class="sxs-lookup"><span data-stu-id="caeff-208">If hello desired size is not on hello current cluster, hello VM needs toobe deallocated before hello resize operation can occur.</span></span> <span data-ttu-id="caeff-209">請注意，當 hello VM 開機回、 hello 暫存磁碟上的任何資料會遭到移除，並 hello 公用 IP 位址變更，除非正在使用的靜態 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="caeff-209">Note, when hello VM is powered back on, any data on hello temp disk are removed, and hello public IP address change unless a static IP address is being used.</span></span> 

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroupVM -Name "myVM" -Force
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroupVM  -VMName myVM
$vm.HardwareProfile.VmSize = "Standard_F4s"
Update-AzureRmVM -VM $vm -ResourceGroupName myResourceGroupVM 
Start-AzureRmVM -ResourceGroupName myResourceGroupVM  -Name $vm.name
```

## <a name="vm-power-states"></a><span data-ttu-id="caeff-210">VM 電源狀態</span><span class="sxs-lookup"><span data-stu-id="caeff-210">VM power states</span></span>

<span data-ttu-id="caeff-211">Azure VM 的電源狀態可以是許多電源狀態的其中一種。</span><span class="sxs-lookup"><span data-stu-id="caeff-211">An Azure VM can have one of many power states.</span></span> <span data-ttu-id="caeff-212">此狀態表示 hello 目前 hello VM 的狀態從 hello hypervisor hello 觀點來看。</span><span class="sxs-lookup"><span data-stu-id="caeff-212">This state represents hello current state of hello VM from hello standpoint of hello hypervisor.</span></span> 

### <a name="power-states"></a><span data-ttu-id="caeff-213">電源狀態</span><span class="sxs-lookup"><span data-stu-id="caeff-213">Power states</span></span>

| <span data-ttu-id="caeff-214">電源狀態</span><span class="sxs-lookup"><span data-stu-id="caeff-214">Power State</span></span> | <span data-ttu-id="caeff-215">說明</span><span class="sxs-lookup"><span data-stu-id="caeff-215">Description</span></span>
|----|----|
| <span data-ttu-id="caeff-216">啟動中</span><span class="sxs-lookup"><span data-stu-id="caeff-216">Starting</span></span> | <span data-ttu-id="caeff-217">指出正在啟動 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="caeff-217">Indicates hello virtual machine is being started.</span></span> |
| <span data-ttu-id="caeff-218">執行中</span><span class="sxs-lookup"><span data-stu-id="caeff-218">Running</span></span> | <span data-ttu-id="caeff-219">指出該 hello 虛擬機器正在執行。</span><span class="sxs-lookup"><span data-stu-id="caeff-219">Indicates that hello virtual machine is running.</span></span> |
| <span data-ttu-id="caeff-220">停止中</span><span class="sxs-lookup"><span data-stu-id="caeff-220">Stopping</span></span> | <span data-ttu-id="caeff-221">表示正在停止該 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="caeff-221">Indicates that hello virtual machine is being stopped.</span></span> | 
| <span data-ttu-id="caeff-222">已停止</span><span class="sxs-lookup"><span data-stu-id="caeff-222">Stopped</span></span> | <span data-ttu-id="caeff-223">表示該 hello 虛擬機器已停止。</span><span class="sxs-lookup"><span data-stu-id="caeff-223">Indicates that hello virtual machine is stopped.</span></span> <span data-ttu-id="caeff-224">請注意在 hello 停止狀態的虛擬機器仍會產生計算費用。</span><span class="sxs-lookup"><span data-stu-id="caeff-224">Note that virtual machines in hello stopped state still incur compute charges.</span></span>  |
| <span data-ttu-id="caeff-225">正在解除配置</span><span class="sxs-lookup"><span data-stu-id="caeff-225">Deallocating</span></span> | <span data-ttu-id="caeff-226">表示已解除配置該 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="caeff-226">Indicates that hello virtual machine is being deallocated.</span></span> |
| <span data-ttu-id="caeff-227">已解除配置</span><span class="sxs-lookup"><span data-stu-id="caeff-227">Deallocated</span></span> | <span data-ttu-id="caeff-228">表示從 hello hypervisor，但仍然可以使用 hello 控制平面中完全移除該 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="caeff-228">Indicates that hello virtual machine is completely removed from hello hypervisor but still available in hello control plane.</span></span> <span data-ttu-id="caeff-229">Hello 取消配置狀態中的虛擬機器不會產生計算費用。</span><span class="sxs-lookup"><span data-stu-id="caeff-229">Virtual machines in hello Deallocated state do not incur compute charges.</span></span> |
| - | <span data-ttu-id="caeff-230">表示 hello hello 虛擬機器的電源狀態不明。</span><span class="sxs-lookup"><span data-stu-id="caeff-230">Indicates that hello power state of hello virtual machine is unknown.</span></span> |

### <a name="find-power-state"></a><span data-ttu-id="caeff-231">尋找電源狀態</span><span class="sxs-lookup"><span data-stu-id="caeff-231">Find power state</span></span>

<span data-ttu-id="caeff-232">特定的 VM，使用 hello tooretrieve hello 狀態[Get AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm)命令。</span><span class="sxs-lookup"><span data-stu-id="caeff-232">tooretrieve hello state of a particular VM, use hello [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) command.</span></span> <span data-ttu-id="caeff-233">為確定 toospecify 虛擬機器與資源群組的有效名稱。</span><span class="sxs-lookup"><span data-stu-id="caeff-233">Be sure toospecify a valid name for a virtual machine and resource group.</span></span> 

```powershell
Get-AzureRmVM `
    -ResourceGroupName myResourceGroup `
    -Name myVM `
    -Status | Select @{n="Status"; e={$_.Statuses[1].Code}}
```

<span data-ttu-id="caeff-234">輸出：</span><span class="sxs-lookup"><span data-stu-id="caeff-234">Output:</span></span>

```powershell
Status
------
PowerState/running
```

## <a name="management-tasks"></a><span data-ttu-id="caeff-235">管理工作</span><span class="sxs-lookup"><span data-stu-id="caeff-235">Management tasks</span></span>

<span data-ttu-id="caeff-236">在虛擬機器的 hello 生命週期，您可能想 toorun 管理工作，例如啟動、 停止或刪除虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="caeff-236">During hello lifecycle of a virtual machine, you may want toorun management tasks such as starting, stopping, or deleting a virtual machine.</span></span> <span data-ttu-id="caeff-237">此外，您可能想 toocreate 指令碼 tooautomate 重複或複雜工作。</span><span class="sxs-lookup"><span data-stu-id="caeff-237">Additionally, you may want toocreate scripts tooautomate repetitive or complex tasks.</span></span> <span data-ttu-id="caeff-238">使用 Azure PowerShell，多的常見管理工作可以執行從 hello 命令列或指令碼中。</span><span class="sxs-lookup"><span data-stu-id="caeff-238">Using Azure PowerShell, many common management tasks can be run from hello command line or in scripts.</span></span>

### <a name="stop-virtual-machine"></a><span data-ttu-id="caeff-239">停止虛擬機器</span><span class="sxs-lookup"><span data-stu-id="caeff-239">Stop virtual machine</span></span>

<span data-ttu-id="caeff-240">使用 [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) 停止及解除配置虛擬機器：</span><span class="sxs-lookup"><span data-stu-id="caeff-240">Stop and deallocate a virtual machine with [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm):</span></span>

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroupVM -Name "myVM" -Force
```

<span data-ttu-id="caeff-241">如果您想 tookeep hello 中佈建狀態的虛擬機器，請使用 hello-StayProvisioned 參數。</span><span class="sxs-lookup"><span data-stu-id="caeff-241">If you want tookeep hello virtual machine in a provisioned state, use hello -StayProvisioned parameter.</span></span>

### <a name="start-virtual-machine"></a><span data-ttu-id="caeff-242">啟動虛擬機器</span><span class="sxs-lookup"><span data-stu-id="caeff-242">Start virtual machine</span></span>

```powershell
Start-AzureRmVM -ResourceGroupName myResourceGroupVM -Name myVM
```

### <a name="delete-resource-group"></a><span data-ttu-id="caeff-243">刪除資源群組</span><span class="sxs-lookup"><span data-stu-id="caeff-243">Delete resource group</span></span>

<span data-ttu-id="caeff-244">刪除資源群組同時會刪除其內含的所有資源。</span><span class="sxs-lookup"><span data-stu-id="caeff-244">Deleting a resource group also deletes all resources contained within.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroupVM -Force
```

## <a name="next-steps"></a><span data-ttu-id="caeff-245">後續步驟</span><span class="sxs-lookup"><span data-stu-id="caeff-245">Next steps</span></span>

<span data-ttu-id="caeff-246">在本教學課程中，您已了解基本的 VM 建立和管理，像是如何：</span><span class="sxs-lookup"><span data-stu-id="caeff-246">In this tutorial, you learned about basic VM creation and management such as how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="caeff-247">建立和連線 tooa VM</span><span class="sxs-lookup"><span data-stu-id="caeff-247">Create and connect tooa VM</span></span>
> * <span data-ttu-id="caeff-248">選取及使用 VM 映像</span><span class="sxs-lookup"><span data-stu-id="caeff-248">Select and use VM images</span></span>
> * <span data-ttu-id="caeff-249">檢視及使用特定 VM 大小</span><span class="sxs-lookup"><span data-stu-id="caeff-249">View and use specific VM sizes</span></span>
> * <span data-ttu-id="caeff-250">調整 VM 的大小</span><span class="sxs-lookup"><span data-stu-id="caeff-250">Resize a VM</span></span>
> * <span data-ttu-id="caeff-251">檢視及了解 VM 狀態</span><span class="sxs-lookup"><span data-stu-id="caeff-251">View and understand VM state</span></span>

<span data-ttu-id="caeff-252">前進 toohello 下一個教學課程的 toolearn 有關 VM 磁碟。</span><span class="sxs-lookup"><span data-stu-id="caeff-252">Advance toohello next tutorial toolearn about VM disks.</span></span>  

> [!div class="nextstepaction"]
> [<span data-ttu-id="caeff-253">建立和管理 VM 磁碟</span><span class="sxs-lookup"><span data-stu-id="caeff-253">Create and Manage VM disks</span></span>](./tutorial-manage-data-disk.md)
