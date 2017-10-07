---
title: "aaaTutorial-建置 Azure Vm 上的高可用性應用程式 |Microsoft 文件"
description: "深入了解如何 toocreate 與負載平衡器，在 Azure 中的三個 Windows Vm 之間的高度可用且安全的應用程式"
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
ms.date: 03/30/2017
ms.author: davidmu
ms.openlocfilehash: f9eff96be4f3999651c4108f0334e4eaa1a39c0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-load-balanced-highly-available-application-on-windows-virtual-machines-in-azure"></a><span data-ttu-id="c96a2-103">在 Azure 中的 Windows 虛擬機器上，建置已負載平衡的高可用性應用程式</span><span class="sxs-lookup"><span data-stu-id="c96a2-103">Build a load balanced, highly available application on Windows virtual machines in Azure</span></span>

<span data-ttu-id="c96a2-104">在本教學課程中，您可以建立具有恢復功能 toomaintenance 事件的高可用性應用程式。</span><span class="sxs-lookup"><span data-stu-id="c96a2-104">In this tutorial, you create a highly available application that is resilient toomaintenance events.</span></span> <span data-ttu-id="c96a2-105">hello 應用程式使用負載平衡器、 可用性設定組和三個 Windows 虛擬機器 (Vm)。</span><span class="sxs-lookup"><span data-stu-id="c96a2-105">hello app uses a load balancer, an availability set, and three Windows virtual machines (VMs).</span></span> <span data-ttu-id="c96a2-106">本教學課程會安裝 IIS，但您可以使用不同的應用程式架構，使用此教學課程 toodeploy hello 相同的高可用性元件和指導方針。</span><span class="sxs-lookup"><span data-stu-id="c96a2-106">This tutorial installs IIS, though you can use this tutorial toodeploy a different application framework using hello same high availability components and guidelines.</span></span> 

## <a name="step-1---azure-prerequisites"></a><span data-ttu-id="c96a2-107">步驟 1 - Azure 必要條件</span><span class="sxs-lookup"><span data-stu-id="c96a2-107">Step 1 - Azure prerequisites</span></span>

<span data-ttu-id="c96a2-108">toocomplete 本教學課程，請確定您有最新安裝 hello [Azure PowerShell](/powershell/azure/overview)模組。</span><span class="sxs-lookup"><span data-stu-id="c96a2-108">toocomplete this tutorial, make sure that you have installed hello latest [Azure PowerShell](/powershell/azure/overview) module.</span></span>

<span data-ttu-id="c96a2-109">首先，登入 tooyour hello 登入 AzureRmAccount 命令與 Azure 訂用帳戶，並遵循螢幕上指示 hello。</span><span class="sxs-lookup"><span data-stu-id="c96a2-109">First, log in tooyour Azure subscription with hello Login-AzureRmAccount command and follow hello on-screen directions.</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="c96a2-110">Azure 資源群組是在其中部署與管理 Azure 資源的邏輯容器。</span><span class="sxs-lookup"><span data-stu-id="c96a2-110">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="c96a2-111">您可以建立其他的 Azure 資源之前，您需要 toocreate 的資源群組與[新增 AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup)。</span><span class="sxs-lookup"><span data-stu-id="c96a2-111">Before you can create any other Azure resources, you need toocreate a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="c96a2-112">hello 下列範例會建立名為的資源群組`myResourceGroup`在 hello`westeurope`區域：</span><span class="sxs-lookup"><span data-stu-id="c96a2-112">hello following example creates a resource group named `myResourceGroup` in hello `westeurope` region:</span></span> 

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroup -Location westeurope
```

## <a name="step-2---create-availability-set"></a><span data-ttu-id="c96a2-113">步驟 2 - 建立可用性設定組</span><span class="sxs-lookup"><span data-stu-id="c96a2-113">Step 2 - Create availability set</span></span>

<span data-ttu-id="c96a2-114">可以跨越邏輯容錯和更新網域建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="c96a2-114">Virtual machines can be created across logical fault and update domains.</span></span> <span data-ttu-id="c96a2-115">每個邏輯網域代表 hello 基礎的 Azure 資料中心內的硬體的一部分。</span><span class="sxs-lookup"><span data-stu-id="c96a2-115">Each logical domain represents a portion of hardware in hello underlying Azure datacenter.</span></span> <span data-ttu-id="c96a2-116">當您建立兩部或多部 VM 時，您的計算和儲存體資源會分散於這些網域。</span><span class="sxs-lookup"><span data-stu-id="c96a2-116">When you create two or more VMs, your compute and storage resources are distributed across these domains.</span></span> <span data-ttu-id="c96a2-117">如果硬體元件需要維護，此分佈會維護應用程式的 hello 可用性。</span><span class="sxs-lookup"><span data-stu-id="c96a2-117">This distribution maintains hello availability of your app if a hardware component needs maintenance.</span></span> <span data-ttu-id="c96a2-118">可用性設定組可讓您定義這些邏輯容錯和更新網域。</span><span class="sxs-lookup"><span data-stu-id="c96a2-118">Availability sets let you define these logical fault and update domains.</span></span>

<span data-ttu-id="c96a2-119">使用 [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset) 建立可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="c96a2-119">Create an availability set with [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span></span> <span data-ttu-id="c96a2-120">hello 下列範例會建立可用性設定組具名`myAvailabilitySet`:</span><span class="sxs-lookup"><span data-stu-id="c96a2-120">hello following example creates an availability set named `myAvailabilitySet`:</span></span>

```powershell
$availabilitySet = New-AzureRmAvailabilitySet `
  -ResourceGroupName myResourceGroup `
  -Name myAvailabilitySet `
  -Location westeurope `
  -Managed `
  -PlatformFaultDomainCount 3 `
  -PlatformUpdateDomainCount 2
```

## <a name="step-3---create-load-balancer"></a><span data-ttu-id="c96a2-121">步驟 3 - 建立負載平衡器</span><span class="sxs-lookup"><span data-stu-id="c96a2-121">Step 3 - Create load balancer</span></span>

<span data-ttu-id="c96a2-122">Azure Load Balancer 會使用負載平衡器規則，將流量分散於一組定義的 VM。</span><span class="sxs-lookup"><span data-stu-id="c96a2-122">An Azure load balancer distributes traffic across a set of defined VMs using load balancer rules.</span></span> <span data-ttu-id="c96a2-123">健全狀況探查監視每個 VM 上指定的連接埠，並只會發佈流量 tooan 操作的 VM。</span><span class="sxs-lookup"><span data-stu-id="c96a2-123">A health probe monitors a given port on each VM and only distributes traffic tooan operational VM.</span></span>

### <a name="create-public-ip-address"></a><span data-ttu-id="c96a2-124">建立公用 IP 位址</span><span class="sxs-lookup"><span data-stu-id="c96a2-124">Create public IP address</span></span>

<span data-ttu-id="c96a2-125">tooaccess hello 網際網路上的應用程式指派的公用 IP 位址 toohello 負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="c96a2-125">tooaccess your app on hello Internet, assign a public IP address toohello load balancer.</span></span> <span data-ttu-id="c96a2-126">使用 [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) 建立公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="c96a2-126">Create a public IP address with [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span></span> <span data-ttu-id="c96a2-127">hello 下列範例會建立名為的公用 IP 位址`myPublicIP`:</span><span class="sxs-lookup"><span data-stu-id="c96a2-127">hello following example creates a public IP address named `myPublicIP`:</span></span>

```powershell
$pip = New-AzureRmPublicIpAddress `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -AllocationMethod Static `
  -Name myPublicIP
```

### <a name="create-load-balancer"></a><span data-ttu-id="c96a2-128">建立負載平衡器</span><span class="sxs-lookup"><span data-stu-id="c96a2-128">Create load balancer</span></span>

<span data-ttu-id="c96a2-129">使用 [New-AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig) 建立前端 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="c96a2-129">Create a frontend IP address with [New-AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig).</span></span> <span data-ttu-id="c96a2-130">hello 下列範例會建立名為的前端 IP 位址`myFrontEndPool`:</span><span class="sxs-lookup"><span data-stu-id="c96a2-130">hello following example creates a frontend IP address named `myFrontEndPool`:</span></span> 

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name myFrontEndPool -PublicIpAddress $pip
```

<span data-ttu-id="c96a2-131">使用 [New-AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig) 建立後端位址集區。</span><span class="sxs-lookup"><span data-stu-id="c96a2-131">Create a backend address pool with [New-AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig).</span></span> <span data-ttu-id="c96a2-132">hello 下列範例會建立名為後端位址集區`myBackEndPool`:</span><span class="sxs-lookup"><span data-stu-id="c96a2-132">hello following example creates a backend address pool named `myBackEndPool`:</span></span>

```powershell
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name myBackEndPool
```

<span data-ttu-id="c96a2-133">現在，建立 hello 的負載平衡器[新增 AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer)。</span><span class="sxs-lookup"><span data-stu-id="c96a2-133">Now, create hello load balancer with [New-AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer).</span></span> <span data-ttu-id="c96a2-134">hello 下列範例會建立名為負載平衡器`myLoadBalancer`使用 hello`myPublicIP`位址：</span><span class="sxs-lookup"><span data-stu-id="c96a2-134">hello following example creates a load balancer named `myLoadBalancer` using hello `myPublicIP` address:</span></span>

```powershell
$lb = New-AzureRmLoadBalancer `
  -ResourceGroupName myResourceGroup `
  -Name myLoadBalancer `
  -Location westeurope `
  -FrontendIpConfiguration $frontendIP `
  -BackendAddressPool $backendPool
```

### <a name="create-health-probe"></a><span data-ttu-id="c96a2-135">建立健全狀況探查</span><span class="sxs-lookup"><span data-stu-id="c96a2-135">Create health probe</span></span>

<span data-ttu-id="c96a2-136">tooallow hello 負載平衡器 toomonitor hello 狀態的應用程式，您可以使用健全狀況探查。</span><span class="sxs-lookup"><span data-stu-id="c96a2-136">tooallow hello load balancer toomonitor hello status of your app, you use a health probe.</span></span> <span data-ttu-id="c96a2-137">hello 健全狀況探查以動態方式加入或移除 hello 負載平衡器輪替根據其回應 toohealth 檢查 Vm。</span><span class="sxs-lookup"><span data-stu-id="c96a2-137">hello health probe dynamically adds or removes VMs from hello load balancer rotation based on their response toohealth checks.</span></span> <span data-ttu-id="c96a2-138">根據預設，VM 會移除從 15 秒的間隔的兩個連續多次失敗後的 hello 負載平衡器發佈。</span><span class="sxs-lookup"><span data-stu-id="c96a2-138">By default, a VM is removed from hello load balancer distribution after two consecutive failures at 15-second intervals.</span></span>

<span data-ttu-id="c96a2-139">使用 [Add-AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig) 建立健全狀況探查。</span><span class="sxs-lookup"><span data-stu-id="c96a2-139">Create a health probe with [Add-AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig).</span></span> <span data-ttu-id="c96a2-140">hello 下列範例會建立名為健全狀況探查`myHealthProbe`，監視每個 VM:</span><span class="sxs-lookup"><span data-stu-id="c96a2-140">hello following example creates a health probe named `myHealthProbe` that monitors each VM:</span></span>

```powershell
Add-AzureRmLoadBalancerProbeConfig -Name myHealthProbe `
  -LoadBalancer $lb `
  -Protocol tcp `
  -Port 80 `
  -IntervalInSeconds 15 `
  -ProbeCount 2
```

### <a name="create-load-balancer-rule"></a><span data-ttu-id="c96a2-141">建立負載平衡器規則</span><span class="sxs-lookup"><span data-stu-id="c96a2-141">Create load balancer rule</span></span>

<span data-ttu-id="c96a2-142">負載平衡器規則是使用的 toodefine 流量的分散式的 toohello Vm 的方式。</span><span class="sxs-lookup"><span data-stu-id="c96a2-142">A load balancer rule is used toodefine how traffic is distributed toohello VMs.</span></span>

<span data-ttu-id="c96a2-143">使用 [Add-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig) 建立負載平衡器規則。</span><span class="sxs-lookup"><span data-stu-id="c96a2-143">Create a load balancer rule with [Add-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig).</span></span> <span data-ttu-id="c96a2-144">hello 下列範例會建立名為的負載平衡器規則`myLoadBalancerRule`平衡連接埠上的流量和`80`:</span><span class="sxs-lookup"><span data-stu-id="c96a2-144">hello following example creates a load balancer rule named `myLoadBalancerRule` and balances traffic on port `80`:</span></span>

```powershell
Add-AzureRmLoadBalancerRuleConfig -Name myLoadBalancerRule `
  -LoadBalancer $lb `
  -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
  -BackendAddressPool $lb.BackendAddressPools[0] `
  -Protocol Tcp `
  -FrontendPort 80 `
  -BackendPort 80
```

<span data-ttu-id="c96a2-145">更新與 hello 負載平衡器[組 AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):</span><span class="sxs-lookup"><span data-stu-id="c96a2-145">Update hello load balancer with [Set-AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):</span></span>

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```

## <a name="step-4---configure-networking"></a><span data-ttu-id="c96a2-146">步驟 4 - 設定網路功能</span><span class="sxs-lookup"><span data-stu-id="c96a2-146">Step 4 - Configure networking</span></span>

<span data-ttu-id="c96a2-147">每個 VM 有一或多個虛擬網路介面卡 (Nic) 的 tooa 虛擬網路連線。</span><span class="sxs-lookup"><span data-stu-id="c96a2-147">Each VM has one or more virtual network interface cards (NICs) that connect tooa virtual network.</span></span> <span data-ttu-id="c96a2-148">此虛擬網路被保護 toofilter 定義的存取規則為基礎的流量。</span><span class="sxs-lookup"><span data-stu-id="c96a2-148">This virtual network is secured toofilter traffic based on defined access rules.</span></span>

### <a name="create-virtual-network"></a><span data-ttu-id="c96a2-149">建立虛擬網路</span><span class="sxs-lookup"><span data-stu-id="c96a2-149">Create virtual network</span></span>

<span data-ttu-id="c96a2-150">首先，使用 [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) 設定子網路。</span><span class="sxs-lookup"><span data-stu-id="c96a2-150">First, configure a subnet with [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span></span> <span data-ttu-id="c96a2-151">hello 下列範例會建立名為的子網路`mySubnet`:</span><span class="sxs-lookup"><span data-stu-id="c96a2-151">hello following example creates a subnet named `mySubnet`:</span></span>

```powershell
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name mySubnet -AddressPrefix 192.168.1.0/24
```

<span data-ttu-id="c96a2-152">tooprovide 網路連線 tooyour Vm，建立虛擬網路與[新增 AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork)。</span><span class="sxs-lookup"><span data-stu-id="c96a2-152">tooprovide network connectivity tooyour VMs, create a virtual network with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span></span> <span data-ttu-id="c96a2-153">hello 下列範例會建立虛擬網路，名為`myVnet`與`mySubnet`:</span><span class="sxs-lookup"><span data-stu-id="c96a2-153">hello following example creates a virtual network named `myVnet` with `mySubnet`:</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -Name myVnet `
  -AddressPrefix 192.168.0.0/16 `
  -Subnet $subnetConfig
```

### <a name="configure-network-security"></a><span data-ttu-id="c96a2-154">設定網路安全性</span><span class="sxs-lookup"><span data-stu-id="c96a2-154">Configure network security</span></span>

<span data-ttu-id="c96a2-155">Azure [網路安全性群組](../../virtual-network/virtual-networks-nsg.md) (NSG) 控制一或多部虛擬機器的輸入和傳出流量。</span><span class="sxs-lookup"><span data-stu-id="c96a2-155">An Azure [network security group](../../virtual-network/virtual-networks-nsg.md) (NSG) controls inbound and outbound traffic for one or many virtual machines.</span></span> <span data-ttu-id="c96a2-156">網路安全性群組規則可允許或拒絕特定連接埠或連接埠範圍上的網路流量。</span><span class="sxs-lookup"><span data-stu-id="c96a2-156">Network security group rules allow or deny network traffic on a specific port or port range.</span></span> <span data-ttu-id="c96a2-157">這些規則也可以包含來源位址首碼，所以只有在預先定義的來源產生的流量可以與虛擬機器通訊。</span><span class="sxs-lookup"><span data-stu-id="c96a2-157">These rules can also include a source address prefix so that only traffic originating at a predefined source can communicate with a virtual machine.</span></span>

<span data-ttu-id="c96a2-158">tooallow web 流量 tooreach 您的應用程式，請建立網路安全性群組規則與[新增 AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig)。</span><span class="sxs-lookup"><span data-stu-id="c96a2-158">tooallow web traffic tooreach your app, create a network security group rule with [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig).</span></span> <span data-ttu-id="c96a2-159">hello 下列範例會建立網路安全性群組規則命名為`myNetworkSecurityGroupRule`:</span><span class="sxs-lookup"><span data-stu-id="c96a2-159">hello following example creates a network security group rule named `myNetworkSecurityGroupRule`:</span></span>

```powershell
$nsgRule = New-AzureRmNetworkSecurityRuleConfig `
  -Name myNetworkSecurityGroupRule `
  -Protocol Tcp `
  -Direction Inbound `
  -Priority 1001 `
  -SourceAddressPrefix * `
  -SourcePortRange * `
  -DestinationAddressPrefix * `
  -DestinationPortRange 80 `
  -Access Allow
```

<span data-ttu-id="c96a2-160">使用 [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) 建立網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="c96a2-160">Create a network security group with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup).</span></span> <span data-ttu-id="c96a2-161">hello 下列範例會建立名為 NSG `myNetworkSecurityGroup`:</span><span class="sxs-lookup"><span data-stu-id="c96a2-161">hello following example creates an NSG named `myNetworkSecurityGroup`:</span></span>

```powershell
$nsg = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -Name myNetworkSecurityGroup `
  -SecurityRules $nsgRule
```

<span data-ttu-id="c96a2-162">新增 hello 安全性群組 toohello 子網路與[組 AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig):</span><span class="sxs-lookup"><span data-stu-id="c96a2-162">Add hello network security group toohello subnet with [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig):</span></span>

```powershell
Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet `
  -Name mySubnet `
  -NetworkSecurityGroup $nsg `
  -AddressPrefix 192.168.1.0/24
```

<span data-ttu-id="c96a2-163">更新 hello 虛擬網路與[組 AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork):</span><span class="sxs-lookup"><span data-stu-id="c96a2-163">Update hello virtual network with [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork):</span></span>

```powershell
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```

### <a name="create-virtual-network-interface-cards"></a><span data-ttu-id="c96a2-164">建立虛擬網路介面卡</span><span class="sxs-lookup"><span data-stu-id="c96a2-164">Create virtual network interface cards</span></span>

<span data-ttu-id="c96a2-165">負載平衡器函式與 hello 虛擬 NIC 資源，而不是 hello 實際的 VM。</span><span class="sxs-lookup"><span data-stu-id="c96a2-165">Load balancers function with hello virtual NIC resource rather than hello actual VM.</span></span> <span data-ttu-id="c96a2-166">hello 虛擬 NIC 連線的 toohello 的負載平衡，然後附加 tooa VM。</span><span class="sxs-lookup"><span data-stu-id="c96a2-166">hello virtual NIC is connected toohello load balancer, and then attached tooa VM.</span></span>

<span data-ttu-id="c96a2-167">使用 [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) 建立虛擬 NIC。</span><span class="sxs-lookup"><span data-stu-id="c96a2-167">Create a virtual NIC with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span></span> <span data-ttu-id="c96a2-168">hello 下列範例會建立三個虛擬 Nic。</span><span class="sxs-lookup"><span data-stu-id="c96a2-168">hello following example creates three virtual NICs.</span></span> <span data-ttu-id="c96a2-169">（每個 VM 的虛擬 NIC 建立 hello 下列中的應用程式的步驟）：</span><span class="sxs-lookup"><span data-stu-id="c96a2-169">(One virtual NIC for each VM you create for your app in hello following steps):</span></span>


```powershell
for ($i=1; $i -le 3; $i++)
{
   New-AzureRmNetworkInterface -ResourceGroupName myResourceGroup `
     -Name myNic$i `
     -Location westeurope `
     -Subnet $vnet.Subnets[0] `
     -LoadBalancerBackendAddressPool $lb.BackendAddressPools[0]
}

```

## <a name="step-5---create-virtual-machines"></a><span data-ttu-id="c96a2-170">步驟 5 - 建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="c96a2-170">Step 5 - Create virtual machines</span></span>

<span data-ttu-id="c96a2-171">以所有 hello 基礎就地元件，您現在可以建立高可用性 Vm toorun 您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="c96a2-171">With all hello underlying components in place, you can now create highly available VMs toorun your app.</span></span> 

<span data-ttu-id="c96a2-172">取得 hello 使用者名稱和密碼所需的 hello 與 hello 虛擬機器上的系統管理員帳戶[Get-credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="c96a2-172">Get hello username and password needed for hello administrator account on hello virtual machine with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="c96a2-173">建立與 hello Vm[新增 AzureRmVMConfig](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/new-azurermvmconfig)，[組 AzureRmVMOperatingSystem](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmoperatingsystem)，[組 AzureRmVMSourceImage](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmsourceimage)，[組 AzureRmVMOSDisk](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmosdisk)，[新增 AzureRmVMNetworkInterface](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/add-azurermvmnetworkinterface)，和[新 AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm)。</span><span class="sxs-lookup"><span data-stu-id="c96a2-173">Create hello VMs with [New-AzureRmVMConfig](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/new-azurermvmconfig), [Set-AzureRmVMOperatingSystem](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmoperatingsystem), [Set-AzureRmVMSourceImage](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmsourceimage), [Set-AzureRmVMOSDisk](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmosdisk), [Add-AzureRmVMNetworkInterface](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/add-azurermvmnetworkinterface), and [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="c96a2-174">hello 下列範例會建立三個 Vm:</span><span class="sxs-lookup"><span data-stu-id="c96a2-174">hello following example creates three VMs:</span></span>

```powershell
for ($i=1; $i -le 3; $i++)
{
   $vm = New-AzureRmVMConfig -VMName myVM$i -VMSize Standard_D1 -AvailabilitySetId $availabilitySet.Id
   $vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName myVM$i -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
   $vm = Set-AzureRmVMSourceImage -VM $vm -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2016-Datacenter -Version latest
   $vm = Set-AzureRmVMOSDisk -VM $vm -Name myOsDisk$i -StorageAccountType StandardLRS -DiskSizeInGB 128 -CreateOption FromImage -Caching ReadWrite
   $nic = Get-AzureRmNetworkInterface -ResourceGroupName myResourceGroup -Name myNic$i
   $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
   New-AzureRmVM -ResourceGroupName myResourceGroup -Location westeurope -VM $vm
}

```

<span data-ttu-id="c96a2-175">它會採用數個分鐘 toocreate 並設定所有三個 Vm。</span><span class="sxs-lookup"><span data-stu-id="c96a2-175">It takes several minutes toocreate and configure all three VMs.</span></span> <span data-ttu-id="c96a2-176">hello 負載平衡器健全狀況探查會自動偵測 hello 應用程式在每個 VM 上執行。</span><span class="sxs-lookup"><span data-stu-id="c96a2-176">hello load balancer health probe automatically detects when hello app is running on each VM.</span></span> <span data-ttu-id="c96a2-177">一旦 hello 應用程式正在執行，hello 負載平衡器規則會啟動 toodistribute 流量。</span><span class="sxs-lookup"><span data-stu-id="c96a2-177">Once hello app is running, hello load balancer rule starts toodistribute traffic.</span></span>

### <a name="install-hello-app"></a><span data-ttu-id="c96a2-178">安裝 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="c96a2-178">Install hello app</span></span> 

<span data-ttu-id="c96a2-179">Azure 虛擬機器擴充功能是使用的 tooautomate 虛擬機器組態工作，例如安裝應用程式和設定 hello 作業系統。</span><span class="sxs-lookup"><span data-stu-id="c96a2-179">Azure virtual machine extensions are used tooautomate virtual machine configuration tasks such as installing applications and configuring hello operating system.</span></span> <span data-ttu-id="c96a2-180">hello[適用於 Windows 的自訂指令碼延伸](./../virtual-machines-windows-extensions-customscript.md)是使用的 toorun hello 虛擬機器上的任何 PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="c96a2-180">hello [custom script extension for Windows](./../virtual-machines-windows-extensions-customscript.md) is used toorun any PowerShell script on hello virtual machine.</span></span> <span data-ttu-id="c96a2-181">hello 指令碼可以儲存在 Azure 儲存體，任何可存取的 HTTP 端點，或內嵌在 hello 自訂指令碼延伸模組組態。</span><span class="sxs-lookup"><span data-stu-id="c96a2-181">hello script can be stored in Azure storage, any accessible HTTP endpoint, or embedded in hello custom script extension configuration.</span></span> <span data-ttu-id="c96a2-182">當使用 hello 自訂指令碼延伸模組，hello Azure VM 代理程式管理 hello 指令碼執行。</span><span class="sxs-lookup"><span data-stu-id="c96a2-182">When using hello custom script extension, hello Azure VM agent manages hello script execution.</span></span>

<span data-ttu-id="c96a2-183">使用[組 AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall hello 自訂指令碼延伸。</span><span class="sxs-lookup"><span data-stu-id="c96a2-183">Use [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall hello custom script extension.</span></span> <span data-ttu-id="c96a2-184">hello 延伸模組執行`powershell Add-WindowsFeature Web-Server`tooinstall hello IIS web 伺服器：</span><span class="sxs-lookup"><span data-stu-id="c96a2-184">hello extension runs `powershell Add-WindowsFeature Web-Server` tooinstall hello IIS webserver:</span></span>

```powershell
for ($i=1; $i -le 3; $i++)
{
   Set-AzureRmVMExtension -ResourceGroupName myResourceGroup `
     -ExtensionName IIS `
     -VMName myVM$i `
     -Publisher Microsoft.Compute `
     -ExtensionType CustomScriptExtension `
     -TypeHandlerVersion 1.4 `
     -SettingString '{"commandToExecute":"powershell Add-WindowsFeature Web-Server"}' `
     -Location westeurope
}
```

### <a name="test-your-app"></a><span data-ttu-id="c96a2-185">測試應用程式</span><span class="sxs-lookup"><span data-stu-id="c96a2-185">Test your app</span></span>

<span data-ttu-id="c96a2-186">取得您的負載平衡器的 hello 公用 IP 位址[Get AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress)。</span><span class="sxs-lookup"><span data-stu-id="c96a2-186">Obtain hello public IP address of your load balancer with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="c96a2-187">hello 下列範例會取得 IP 位址 hello`myPublicIP`稍早建立：</span><span class="sxs-lookup"><span data-stu-id="c96a2-187">hello following example obtains hello IP address for `myPublicIP` created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress -ResourceGroupName myResourceGroup -Name myPublicIP | select IpAddress
```

<span data-ttu-id="c96a2-188">Tooa 網頁瀏覽器中輸入 hello 公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="c96a2-188">Enter hello public IP address in tooa web browser.</span></span> <span data-ttu-id="c96a2-189">與就地 hello NSG 規則，會顯示 hello 預設 IIS 網站。</span><span class="sxs-lookup"><span data-stu-id="c96a2-189">With hello NSG rule in place, hello default IIS website is displayed.</span></span> 

![IIS 預設網站](media/load-balanced-iis-tutorial/iis.png)

## <a name="step-6--management-tasks"></a><span data-ttu-id="c96a2-191">步驟 6 - 管理工作</span><span class="sxs-lookup"><span data-stu-id="c96a2-191">Step 6 – Management tasks</span></span>

<span data-ttu-id="c96a2-192">您可能需要 tooperform hello 執行您的應用程式，例如安裝作業系統更新的 Vm 上的維護。</span><span class="sxs-lookup"><span data-stu-id="c96a2-192">You may need tooperform maintenance on hello VMs running your app, such as installing OS updates.</span></span> <span data-ttu-id="c96a2-193">toodeal 使用增加的流量 tooyour 應用程式，您可能需要 tooadd 其他 Vm。</span><span class="sxs-lookup"><span data-stu-id="c96a2-193">toodeal with increased traffic tooyour app, you may need tooadd additional VMs.</span></span> <span data-ttu-id="c96a2-194">這個區段會顯示如何 tooremove 或加入 VM 從 hello 負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="c96a2-194">This section shows you how tooremove or add a VM from hello load balancer.</span></span> 

### <a name="remove-a-vm-from-hello-load-balancer"></a><span data-ttu-id="c96a2-195">從 hello 負載平衡器移除 VM</span><span class="sxs-lookup"><span data-stu-id="c96a2-195">Remove a VM from hello load balancer</span></span>

<span data-ttu-id="c96a2-196">藉由重設 hello 了 LoadBalancerBackendAddressPools 屬性 hello 網路介面卡移除 hello 後端位址集區的 VM。</span><span class="sxs-lookup"><span data-stu-id="c96a2-196">Remove a VM from hello backend address pool by resetting hello LoadBalancerBackendAddressPools property of hello network interface card.</span></span>

<span data-ttu-id="c96a2-197">取得與 hello 網路介面卡[Get AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="c96a2-197">Get hello network interface card with [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface):</span></span>

```powershell
$nic = Get-AzureRmNetworkInterface -ResourceGroupName myResourceGroup -Name myNic2
``` 

<span data-ttu-id="c96a2-198">Hello 網路介面卡 hello 了 LoadBalancerBackendAddressPools 屬性設定太 $null:</span><span class="sxs-lookup"><span data-stu-id="c96a2-198">Set hello LoadBalancerBackendAddressPools property of hello network interface card too$null:</span></span>

```powershell
$nic.Ipconfigurations[0].LoadBalancerBackendAddressPools=$null
```

<span data-ttu-id="c96a2-199">更新 hello 網路介面卡：</span><span class="sxs-lookup"><span data-stu-id="c96a2-199">Update hello network interface card:</span></span>

```powershell
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

### <a name="add-a-vm-toohello-load-balancer"></a><span data-ttu-id="c96a2-200">新增 VM toohello 負載平衡器</span><span class="sxs-lookup"><span data-stu-id="c96a2-200">Add a VM toohello load balancer</span></span>

<span data-ttu-id="c96a2-201">之後執行 VM 維護，或如果您需要 tooexpand 容量時，加入 hello NIC VM toohello 後端位址集區的 hello 負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="c96a2-201">After performing VM maintenance, or if you need tooexpand capacity, adding hello NIC of a VM toohello backend address pool of hello load balancer.</span></span>

<span data-ttu-id="c96a2-202">收到 hello 負載平衡器：</span><span class="sxs-lookup"><span data-stu-id="c96a2-202">Get hello load balancer:</span></span>

```powershell
$lb = Get-AzureRMLoadBalancer -ResourceGroupName myResourceGroup -Name myLoadBalancer 
```

<span data-ttu-id="c96a2-203">新增 hello hello 負載平衡器 toohello 網路介面卡的後端位址集區：</span><span class="sxs-lookup"><span data-stu-id="c96a2-203">Add hello backend address pool of hello load balancer toohello network interface card:</span></span>

```powershell
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$lb.BackendAddressPools[0]
```

<span data-ttu-id="c96a2-204">更新 hello 網路介面卡：</span><span class="sxs-lookup"><span data-stu-id="c96a2-204">Update hello network interface card:</span></span>

```powershell
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

## <a name="next-steps"></a><span data-ttu-id="c96a2-205">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c96a2-205">Next Steps</span></span>

<span data-ttu-id="c96a2-206">範例 – [Azure 虛擬機器 PowerShell 範例指令碼](./../virtual-machines-windows-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="c96a2-206">Samples – [Azure Virtual Machine PowerShell sample scripts](./../virtual-machines-windows-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>
