---
title: "aaaAzure 虛擬網路和 Windows 虛擬機器 |Microsoft 文件"
description: "教學課程 - 使用 Azure PowerShell 來管理 Azure 虛擬網路和 Windows 虛擬機器"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: davidmu
ms.custom: mvc
ms.openlocfilehash: ed77d9d5873e849fcb2aaf15e41899d7ad8c781a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-virtual-networks-and-windows-virtual-machines-with-azure-powershell"></a><span data-ttu-id="6d06a-103">使用 Azure PowerShell 來管理 Azure 虛擬網路和 Windows 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="6d06a-103">Manage Azure Virtual Networks and Windows Virtual Machines with Azure PowerShell</span></span>

<span data-ttu-id="6d06a-104">Azure 虛擬機器會使用 Azure 網路進行內部和外部的網路通訊。</span><span class="sxs-lookup"><span data-stu-id="6d06a-104">Azure virtual machines use Azure networking for internal and external network communication.</span></span> <span data-ttu-id="6d06a-105">在本教學課程中，您會在虛擬網路中建立多部虛擬機器 (VM)，並設定這些機器間的網路連線。</span><span class="sxs-lookup"><span data-stu-id="6d06a-105">In this tutorial, you create multiple virtual machines (VMs) in a virtual network and configure network connectivity between them.</span></span> <span data-ttu-id="6d06a-106">您會了解如何：</span><span class="sxs-lookup"><span data-stu-id="6d06a-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6d06a-107">建立虛擬網路</span><span class="sxs-lookup"><span data-stu-id="6d06a-107">Create a virtual network</span></span>
> * <span data-ttu-id="6d06a-108">建立虛擬網路子網路</span><span class="sxs-lookup"><span data-stu-id="6d06a-108">Create virtual network subnets</span></span>
> * <span data-ttu-id="6d06a-109">使用網路安全性群組來控制網路流量</span><span class="sxs-lookup"><span data-stu-id="6d06a-109">Control network traffic with Network Security Groups</span></span>
> * <span data-ttu-id="6d06a-110">檢視作用中的流量規則</span><span class="sxs-lookup"><span data-stu-id="6d06a-110">View traffic rules in action</span></span>

<span data-ttu-id="6d06a-111">本教學課程需要 hello Azure PowerShell 模組版本 3.6 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="6d06a-111">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="6d06a-112">執行` Get-Module -ListAvailable AzureRM`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="6d06a-112">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="6d06a-113">如果您需要 tooupgrade，請參閱[安裝 Azure PowerShell 模組](/powershell/azure/install-azurerm-ps)。</span><span class="sxs-lookup"><span data-stu-id="6d06a-113">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="create-vnet"></a><span data-ttu-id="6d06a-114">建立 VNet</span><span class="sxs-lookup"><span data-stu-id="6d06a-114">Create VNet</span></span>

<span data-ttu-id="6d06a-115">VNet 是網路的您自己 hello 雲端中的表示法。</span><span class="sxs-lookup"><span data-stu-id="6d06a-115">A VNet is a representation of your own network in hello cloud.</span></span> <span data-ttu-id="6d06a-116">VNet 是 hello 的隔離的邏輯專用的 Azure 雲端 tooyour 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="6d06a-116">A VNet is a logical isolation of hello Azure cloud dedicated tooyour subscription.</span></span> <span data-ttu-id="6d06a-117">在 VNet 中，您可以找到子網路，連線 toothose 子網路和來自 hello Vm toohello 子網路連線的規則。</span><span class="sxs-lookup"><span data-stu-id="6d06a-117">Within a VNet, you find subnets, rules for connectivity toothose subnets, and connections from hello VMs toohello subnets.</span></span>

<span data-ttu-id="6d06a-118">您可以建立其他的 Azure 資源之前，您需要 toocreate 的資源群組與[新增 AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup)。</span><span class="sxs-lookup"><span data-stu-id="6d06a-118">Before you can create any other Azure resources, you need toocreate a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="6d06a-119">hello 下列範例會建立名為的資源群組*myRGNetwork*在 hello *EastUS*位置：</span><span class="sxs-lookup"><span data-stu-id="6d06a-119">hello following example creates a resource group named *myRGNetwork* in hello *EastUS* location:</span></span>

```powershell
New-AzureRmResourceGroup -ResourceGroupName myRGNetwork -Location EastUS
```

<span data-ttu-id="6d06a-120">子網路是 VNET 的子資源，而且有助於使用 IP 位址首碼來定義 CIDR 區塊內位址空間的區段。</span><span class="sxs-lookup"><span data-stu-id="6d06a-120">A subnet is a child resource of a VNet, and helps define segments of address spaces within a CIDR block, using IP address prefixes.</span></span> <span data-ttu-id="6d06a-121">Nic 可以加入 toosubnets，並已連線的 tooVMs，提供各種工作負載的連線。</span><span class="sxs-lookup"><span data-stu-id="6d06a-121">NICs can be added toosubnets, and connected tooVMs, providing connectivity for various workloads.</span></span>

<span data-ttu-id="6d06a-122">使用 [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) 來建立子網路：</span><span class="sxs-lookup"><span data-stu-id="6d06a-122">Create a subnet with [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig):</span></span>

```powershell
$frontendSubnet = New-AzureRmVirtualNetworkSubnetConfig `
  -Name myFrontendSubnet `
  -AddressPrefix 10.0.0.0/24
```

<span data-ttu-id="6d06a-123">使用 myFrontendSubnet 和 [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) 建立一個名為 *myVNet* 的 VNET：</span><span class="sxs-lookup"><span data-stu-id="6d06a-123">Create a VNET named *myVNet* using *myFrontendSubnet* with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork):</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myVNet `
  -AddressPrefix 10.0.0.0/16 `
  -Subnet $frontendSubnet
```

## <a name="create-front-end-vm"></a><span data-ttu-id="6d06a-124">建立前端 VM</span><span class="sxs-lookup"><span data-stu-id="6d06a-124">Create front-end VM</span></span>

<span data-ttu-id="6d06a-125">在 VNet 中 VM toocommunicate，它必須在虛擬網路介面 (NIC)。</span><span class="sxs-lookup"><span data-stu-id="6d06a-125">For a VM toocommunicate in a VNet, it needs a virtual network interface (NIC).</span></span> <span data-ttu-id="6d06a-126">hello *myFrontendVM*從 hello 存取網際網路，因此也需要公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="6d06a-126">hello *myFrontendVM* is accessed from hello internet, so it also needs a public IP address.</span></span> 

<span data-ttu-id="6d06a-127">使用 [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) 來建立公用 IP 位址：</span><span class="sxs-lookup"><span data-stu-id="6d06a-127">Create a public IP address with [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress):</span></span>

```powershell
$pip = New-AzureRmPublicIpAddress `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -AllocationMethod Static `
  -Name myPublicIPAddress
```

<span data-ttu-id="6d06a-128">使用 [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) 來建立 NIC：</span><span class="sxs-lookup"><span data-stu-id="6d06a-128">Create a NIC with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface):</span></span>


```powershell
$frontendNic = New-AzureRmNetworkInterface `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myFrontendNic `
  -SubnetId $vnet.Subnets[0].Id `
  -PublicIpAddressId $pip.Id
```

<span data-ttu-id="6d06a-129">設定 hello 使用者名稱和密碼所需的 hello hello VM 上的系統管理員帳戶與[Get-credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="6d06a-129">Set hello username and password needed for hello administrator account on hello VM with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="6d06a-130">建立與 hello Vm[新增 AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig)，[組 AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem)，[組 AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage)，[組 AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk)，[新增 AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface)，和[新 AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm)。</span><span class="sxs-lookup"><span data-stu-id="6d06a-130">Create hello VMs with [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig), [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem), [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage), [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk), [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface), and [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> 

```powershell
$frontendVM = New-AzureRmVMConfig `
    -VMName myFrontendVM `
    -VMSize Standard_D1
$frontendVM = Set-AzureRmVMOperatingSystem `
    -VM $frontendVM `
    -Windows `
    -ComputerName myFrontendVM `
    -Credential $cred `
    -ProvisionVMAgent `
    -EnableAutoUpdate
$frontendVM = Set-AzureRmVMSourceImage `
    -VM $frontendVM `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter `
    -Version latest
$frontendVM = Set-AzureRmVMOSDisk `
    -VM $frontendVM `
    -Name myFrontendOSDisk `
    -DiskSizeInGB 128 `
    -CreateOption FromImage `
    -Caching ReadWrite
$frontendVM = Add-AzureRmVMNetworkInterface `
    -VM $frontendVM `
    -Id $frontendNic.Id
New-AzureRmVM `
    -ResourceGroupName myRGNetwork `
    -Location EastUS `
    -VM $frontendVM
```

## <a name="install-web-server"></a><span data-ttu-id="6d06a-131">安裝 Web 伺服器</span><span class="sxs-lookup"><span data-stu-id="6d06a-131">Install web server</span></span>

<span data-ttu-id="6d06a-132">您可以使用遠端桌面工作階段在 myFrontendVM 上安裝 IIS。</span><span class="sxs-lookup"><span data-stu-id="6d06a-132">You can install IIS on *myFrontendVM* by using a remote desktop session.</span></span> <span data-ttu-id="6d06a-133">您需要 tooget hello 公用 IP 位址的 hello VM tooaccess 它。</span><span class="sxs-lookup"><span data-stu-id="6d06a-133">You need tooget hello public IP address of hello VM tooaccess it.</span></span>

<span data-ttu-id="6d06a-134">您可以取得 hello 公用 IP 位址*myFrontendVM*與[Get AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress)。</span><span class="sxs-lookup"><span data-stu-id="6d06a-134">You can get hello public IP address of *myFrontendVM* with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="6d06a-135">hello 下列範例會取得 IP 位址 hello *myPublicIPAddress*稍早建立：</span><span class="sxs-lookup"><span data-stu-id="6d06a-135">hello following example obtains hello IP address for *myPublicIPAddress* created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress `
    -ResourceGroupName myRGNetwork `
    -Name myPublicIPAddress | select IpAddress
```

<span data-ttu-id="6d06a-136">請記下此 IP 位址，以便在未來的步驟中使用它。</span><span class="sxs-lookup"><span data-stu-id="6d06a-136">Take note of this IP Address so you can use it in future steps.</span></span>

<span data-ttu-id="6d06a-137">使用 hello 下列命令與遠端桌面工作階段的 toocreate *myFrontendVM*。</span><span class="sxs-lookup"><span data-stu-id="6d06a-137">Use hello following command toocreate a remote desktop session with *myFrontendVM*.</span></span> <span data-ttu-id="6d06a-138">取代 *<publicIPAddress>*  hello 位址，您先前記錄的密碼。</span><span class="sxs-lookup"><span data-stu-id="6d06a-138">Replace *<publicIPAddress>* with hello address that you previously recorded.</span></span> <span data-ttu-id="6d06a-139">出現提示時，輸入 hello 建立 hello VM 時所使用的認證。</span><span class="sxs-lookup"><span data-stu-id="6d06a-139">When prompted, enter hello credentials used when you created hello VM.</span></span>

```
mstsc /v:<publicIpAddress>
``` 

<span data-ttu-id="6d06a-140">既然已登入太*myFrontendVM*，您可以使用單行 PowerShell tooinstall IIS 並啟用 hello 本機防火牆規則 tooallow web 流量。</span><span class="sxs-lookup"><span data-stu-id="6d06a-140">Now that you have logged in too*myFrontendVM*, you can use a single line of PowerShell tooinstall IIS and enable hello local firewall rule tooallow web traffic.</span></span> <span data-ttu-id="6d06a-141">開啟 PowerShell 命令提示字元並執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="6d06a-141">Open a PowerShell prompt and run hello following command:</span></span>

<span data-ttu-id="6d06a-142">使用[Install-windowsfeature](https://technet.microsoft.com/itpro/powershell/windows/servermanager/install-windowsfeature) toorun hello 自訂指令碼延伸安裝 hello IIS web 伺服器：</span><span class="sxs-lookup"><span data-stu-id="6d06a-142">Use [Install-WindowsFeature](https://technet.microsoft.com/itpro/powershell/windows/servermanager/install-windowsfeature) toorun hello custom script extension that installs hello IIS webserver:</span></span>

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

<span data-ttu-id="6d06a-143">現在您可以使用 hello 公用 IP 位址 toobrowse toohello VM toosee hello IIS 站台。</span><span class="sxs-lookup"><span data-stu-id="6d06a-143">Now you can use hello public IP address toobrowse toohello VM toosee hello IIS site.</span></span>

![IIS 預設網站](./media/tutorial-virtual-network/iis.png)

## <a name="manage-internal-traffic"></a><span data-ttu-id="6d06a-145">管理內部網路流量</span><span class="sxs-lookup"><span data-stu-id="6d06a-145">Manage internal traffic</span></span>

<span data-ttu-id="6d06a-146">網路安全性群組 (NSG) 包含一份安全性規則，允許或拒絕網路流量連線的 tooresources tooa VNet。</span><span class="sxs-lookup"><span data-stu-id="6d06a-146">A network security group (NSG) contains a list of security rules that allow or deny network traffic tooresources connected tooa VNet.</span></span> <span data-ttu-id="6d06a-147">Nsg 可以是相關聯的 toosubnets 或個別的 Nic 附加 tooVMs。</span><span class="sxs-lookup"><span data-stu-id="6d06a-147">NSGs can be associated toosubnets or individual NICs attached tooVMs.</span></span> <span data-ttu-id="6d06a-148">開啟或關閉存取 tooVMs 透過連接埠是使用 NSG 規則。</span><span class="sxs-lookup"><span data-stu-id="6d06a-148">Opening or closing access tooVMs through ports is done using NSG rules.</span></span> <span data-ttu-id="6d06a-149">建立 myFrontendVM 時，會自動開啟輸入連接埠 3389 以供 RDP 連線使用。</span><span class="sxs-lookup"><span data-stu-id="6d06a-149">When you created *myFrontendVM*, inbound port 3389 was automatically opened for RDP connectivity.</span></span>

<span data-ttu-id="6d06a-150">您可以使用 NSG 來設定 VM 的內部通訊。</span><span class="sxs-lookup"><span data-stu-id="6d06a-150">Internal communication of VMs can be configured using an NSG.</span></span> <span data-ttu-id="6d06a-151">在本節中，您學會如何 toocreate hello 中的其他子網路的網路並指派 NSG tooit tooallow 從連接*myFrontendVM*太*myBackendVM*通訊埠 1433年上。</span><span class="sxs-lookup"><span data-stu-id="6d06a-151">In this section, you learn how toocreate an additional subnet in hello network and assign an NSG tooit tooallow a connection from *myFrontendVM* too*myBackendVM* on port 1433.</span></span> <span data-ttu-id="6d06a-152">hello 指派子網路是然後 toohello VM 建立時。</span><span class="sxs-lookup"><span data-stu-id="6d06a-152">hello subnet is then assigned toohello VM when it is created.</span></span>

<span data-ttu-id="6d06a-153">您可以限制內部流量太*myBackendVM*僅從*myFrontendVM*藉由建立 hello 後端子網路的 NSG。</span><span class="sxs-lookup"><span data-stu-id="6d06a-153">You can limit internal traffic too*myBackendVM* from only *myFrontendVM* by creating an NSG for hello back-end subnet.</span></span> <span data-ttu-id="6d06a-154">hello 下列範例會建立名為 NSG 規則*myBackendNSGRule*與[新增 AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig):</span><span class="sxs-lookup"><span data-stu-id="6d06a-154">hello following example creates an NSG rule named *myBackendNSGRule* with [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig):</span></span>

```powershell
$nsgBackendRule = New-AzureRmNetworkSecurityRuleConfig `
  -Name myBackendNSGRule `
  -Protocol Tcp `
  -Direction Inbound `
  -Priority 100 `
  -SourceAddressPrefix 10.0.0.0/24 `
  -SourcePortRange * `
  -DestinationAddressPrefix * `
  -DestinationPortRange 1433 `
  -Access Allow
```

<span data-ttu-id="6d06a-155">使用 [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) 來新增名為 myBackendNSG 的網路安全性群組：</span><span class="sxs-lookup"><span data-stu-id="6d06a-155">Add a network security group named *myBackendNSG* with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup):</span></span>

```powershell
$nsgBackend = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myBackendNSG `
  -SecurityRules $nsgBackendRule
```
## <a name="add-back-end-subnet"></a><span data-ttu-id="6d06a-156">新增後端子網路</span><span class="sxs-lookup"><span data-stu-id="6d06a-156">Add back-end subnet</span></span>

<span data-ttu-id="6d06a-157">新增*myBackEndSubnet*太*myVNet*與[新增 AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig):</span><span class="sxs-lookup"><span data-stu-id="6d06a-157">Add *myBackEndSubnet* too*myVNet* with [Add-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig):</span></span>

```powershell
Add-AzureRmVirtualNetworkSubnetConfig `
  -Name myBackendSubnet `
  -VirtualNetwork $vnet `
  -AddressPrefix 10.0.1.0/24 `
  -NetworkSecurityGroup $nsgBackend
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
$vnet = Get-AzureRmVirtualNetwork `
  -ResourceGroupName myRGNetwork `
  -Name myVNet
```

## <a name="create-back-end-vm"></a><span data-ttu-id="6d06a-158">建立後端 VM</span><span class="sxs-lookup"><span data-stu-id="6d06a-158">Create back-end VM</span></span>

<span data-ttu-id="6d06a-159">最簡單方式 toocreate hello hello 後端 VM 是使用 SQL Server 映像。</span><span class="sxs-lookup"><span data-stu-id="6d06a-159">hello easiest way toocreate hello back-end VM is by using a SQL Server image.</span></span> <span data-ttu-id="6d06a-160">本教學課程只會 hello VM 建立 hello 資料庫伺服器，但不會提供有關存取 hello 資料庫資訊。</span><span class="sxs-lookup"><span data-stu-id="6d06a-160">This tutorial only creates hello VM with hello database server, but doesn't provide information about accessing hello database.</span></span>

<span data-ttu-id="6d06a-161">建立 myBackendNic：</span><span class="sxs-lookup"><span data-stu-id="6d06a-161">Create *myBackendNic*:</span></span>

```powershell
$backendNic = New-AzureRmNetworkInterface `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myBackendNic `
  -SubnetId $vnet.Subnets[1].Id
```

<span data-ttu-id="6d06a-162">Hello 使用者名稱和密碼所需的 hello hello Get-credential 與 VM 上的系統管理員帳戶設定：</span><span class="sxs-lookup"><span data-stu-id="6d06a-162">Set hello username and password needed for hello administrator account on hello VM with Get-Credential:</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="6d06a-163">建立 myBackendVM：</span><span class="sxs-lookup"><span data-stu-id="6d06a-163">Create *myBackendVM*:</span></span>

```powershell
$backendVM = New-AzureRmVMConfig `
  -VMName myBackendVM `
  -VMSize Standard_D1
$backendVM = Set-AzureRmVMOperatingSystem `
  -VM $backendVM `
  -Windows `
  -ComputerName myBackendVM `
  -Credential $cred `
  -ProvisionVMAgent `
  -EnableAutoUpdate
$backendVM = Set-AzureRmVMSourceImage `
  -VM $backendVM `
  -PublisherName MicrosoftSQLServer `
  -Offer SQL2016SP1-WS2016 `
  -Skus Enterprise `
  -Version latest
$backendVM = Set-AzureRmVMOSDisk `
  -VM $backendVM `
  -Name myBackendOSDisk `
  -DiskSizeInGB 128 `
  -CreateOption FromImage `
  -Caching ReadWrite
$backendVM = Add-AzureRmVMNetworkInterface `
  -VM $backendVM `
  -Id $backendNic.Id
New-AzureRmVM `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -VM $backendVM
```

<span data-ttu-id="6d06a-164">hello 映像使用有 SQL Server 安裝，而不是在本教學課程。</span><span class="sxs-lookup"><span data-stu-id="6d06a-164">hello image that is used has SQL Server installed, but is not used in this tutorial.</span></span> <span data-ttu-id="6d06a-165">它是包含的 tooshow 您如何設定 VM toohandle 網路流量和 VM toohandle 資料庫管理。</span><span class="sxs-lookup"><span data-stu-id="6d06a-165">It is included tooshow you how you can configure a VM toohandle web traffic and a VM toohandle database management.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6d06a-166">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6d06a-166">Next steps</span></span>

<span data-ttu-id="6d06a-167">在本教學課程中，您可以建立並保護做為相關的 toovirtual 機器的 Azure 網路。</span><span class="sxs-lookup"><span data-stu-id="6d06a-167">In this tutorial, you created and secured Azure networks as related toovirtual machines.</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="6d06a-168">建立虛擬網路</span><span class="sxs-lookup"><span data-stu-id="6d06a-168">Create a virtual network</span></span>
> * <span data-ttu-id="6d06a-169">建立虛擬網路子網路</span><span class="sxs-lookup"><span data-stu-id="6d06a-169">Create virtual network subnets</span></span>
> * <span data-ttu-id="6d06a-170">使用網路安全性群組來控制網路流量</span><span class="sxs-lookup"><span data-stu-id="6d06a-170">Control network traffic with Network Security Groups</span></span>
> * <span data-ttu-id="6d06a-171">檢視作用中的流量規則</span><span class="sxs-lookup"><span data-stu-id="6d06a-171">View traffic rules in action</span></span>

<span data-ttu-id="6d06a-172">前進 toohello 下一個教學課程的 toolearn 有關監視使用 Azure 備份的虛擬機器上的保護資料。</span><span class="sxs-lookup"><span data-stu-id="6d06a-172">Advance toohello next tutorial toolearn about monitoring securing data on virtual machines using Azure backup.</span></span> <span data-ttu-id="6d06a-173">.</span><span class="sxs-lookup"><span data-stu-id="6d06a-173">.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6d06a-174">備份 Azure 中的 Windows 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="6d06a-174">Back up Windows virtual machines in Azure</span></span>](./tutorial-backup-vms.md)
