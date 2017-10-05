---
title: "教學課程 - 在 Azure VM 上建立高可用性應用程式 | Microsoft Docs"
description: "了解如何使用 Azure 中的負載平衡器，建立跨三部 Windows VM 且高度可用的安全應用程式"
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
ms.openlocfilehash: 4b8690a11ec0e711782a112622e1193c24292289
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="build-a-load-balanced-highly-available-application-on-windows-virtual-machines-in-azure"></a><span data-ttu-id="950e9-103">在 Azure 中的 Windows 虛擬機器上，建置已負載平衡的高可用性應用程式</span><span class="sxs-lookup"><span data-stu-id="950e9-103">Build a load balanced, highly available application on Windows virtual machines in Azure</span></span>

<span data-ttu-id="950e9-104">在本教學課程中，您可以建立高度可用且對維護事件具有彈性的應用程式。</span><span class="sxs-lookup"><span data-stu-id="950e9-104">In this tutorial, you create a highly available application that is resilient to maintenance events.</span></span> <span data-ttu-id="950e9-105">應用程式會使用負載平衡器、可用性設定組和三部 Windows 虛擬機器 (VM)。</span><span class="sxs-lookup"><span data-stu-id="950e9-105">The app uses a load balancer, an availability set, and three Windows virtual machines (VMs).</span></span> <span data-ttu-id="950e9-106">本教學課程會安裝 IIS，但您可以在本教學課程中使用相同高可用性元件和指導方針來部署不同的應用程式架構。</span><span class="sxs-lookup"><span data-stu-id="950e9-106">This tutorial installs IIS, though you can use this tutorial to deploy a different application framework using the same high availability components and guidelines.</span></span> 

## <a name="step-1---azure-prerequisites"></a><span data-ttu-id="950e9-107">步驟 1 - Azure 必要條件</span><span class="sxs-lookup"><span data-stu-id="950e9-107">Step 1 - Azure prerequisites</span></span>

<span data-ttu-id="950e9-108">若要完成本教學課程，請確定您已安裝最新的 [Azure PowerShell](/powershell/azure/overview) 模組。</span><span class="sxs-lookup"><span data-stu-id="950e9-108">To complete this tutorial, make sure that you have installed the latest [Azure PowerShell](/powershell/azure/overview) module.</span></span>

<span data-ttu-id="950e9-109">首先，使用 Login-AzureRmAccount 命令登入 Azure 訂用帳戶並遵循畫面上的指示。</span><span class="sxs-lookup"><span data-stu-id="950e9-109">First, log in to your Azure subscription with the Login-AzureRmAccount command and follow the on-screen directions.</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="950e9-110">Azure 資源群組是在其中部署與管理 Azure 資源的邏輯容器。</span><span class="sxs-lookup"><span data-stu-id="950e9-110">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="950e9-111">您必須先使用 [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) 建立資源群組，才可以建立任何其他 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="950e9-111">Before you can create any other Azure resources, you need to create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="950e9-112">下列範例會在 `westeurope` 區域建立名為 `myResourceGroup` 的資源群組：</span><span class="sxs-lookup"><span data-stu-id="950e9-112">The following example creates a resource group named `myResourceGroup` in the `westeurope` region:</span></span> 

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroup -Location westeurope
```

## <a name="step-2---create-availability-set"></a><span data-ttu-id="950e9-113">步驟 2 - 建立可用性設定組</span><span class="sxs-lookup"><span data-stu-id="950e9-113">Step 2 - Create availability set</span></span>

<span data-ttu-id="950e9-114">可以跨越邏輯容錯和更新網域建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="950e9-114">Virtual machines can be created across logical fault and update domains.</span></span> <span data-ttu-id="950e9-115">每個邏輯網域都代表基礎 Azure 資料中心硬體的一部分。</span><span class="sxs-lookup"><span data-stu-id="950e9-115">Each logical domain represents a portion of hardware in the underlying Azure datacenter.</span></span> <span data-ttu-id="950e9-116">當您建立兩部或多部 VM 時，您的計算和儲存體資源會分散於這些網域。</span><span class="sxs-lookup"><span data-stu-id="950e9-116">When you create two or more VMs, your compute and storage resources are distributed across these domains.</span></span> <span data-ttu-id="950e9-117">如果需要維護硬體元件，此分佈會維護您應用程式的可用性。</span><span class="sxs-lookup"><span data-stu-id="950e9-117">This distribution maintains the availability of your app if a hardware component needs maintenance.</span></span> <span data-ttu-id="950e9-118">可用性設定組可讓您定義這些邏輯容錯和更新網域。</span><span class="sxs-lookup"><span data-stu-id="950e9-118">Availability sets let you define these logical fault and update domains.</span></span>

<span data-ttu-id="950e9-119">使用 [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset) 建立可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="950e9-119">Create an availability set with [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span></span> <span data-ttu-id="950e9-120">下列範例會建立名為 `myAvailabilitySet` 的可用性設定組：</span><span class="sxs-lookup"><span data-stu-id="950e9-120">The following example creates an availability set named `myAvailabilitySet`:</span></span>

```powershell
$availabilitySet = New-AzureRmAvailabilitySet `
  -ResourceGroupName myResourceGroup `
  -Name myAvailabilitySet `
  -Location westeurope `
  -Managed `
  -PlatformFaultDomainCount 3 `
  -PlatformUpdateDomainCount 2
```

## <a name="step-3---create-load-balancer"></a><span data-ttu-id="950e9-121">步驟 3 - 建立負載平衡器</span><span class="sxs-lookup"><span data-stu-id="950e9-121">Step 3 - Create load balancer</span></span>

<span data-ttu-id="950e9-122">Azure Load Balancer 會使用負載平衡器規則，將流量分散於一組定義的 VM。</span><span class="sxs-lookup"><span data-stu-id="950e9-122">An Azure load balancer distributes traffic across a set of defined VMs using load balancer rules.</span></span> <span data-ttu-id="950e9-123">健康狀態探查會監視每部 VM 上指定的連接埠，而且只會將流量分散至操作 VM。</span><span class="sxs-lookup"><span data-stu-id="950e9-123">A health probe monitors a given port on each VM and only distributes traffic to an operational VM.</span></span>

### <a name="create-public-ip-address"></a><span data-ttu-id="950e9-124">建立公用 IP 位址</span><span class="sxs-lookup"><span data-stu-id="950e9-124">Create public IP address</span></span>

<span data-ttu-id="950e9-125">若要存取網際網路上您的應用程式，請將公用 IP 位址指派給負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="950e9-125">To access your app on the Internet, assign a public IP address to the load balancer.</span></span> <span data-ttu-id="950e9-126">使用 [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) 建立公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="950e9-126">Create a public IP address with [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span></span> <span data-ttu-id="950e9-127">下列範例會建立名為 `myPublicIP` 的公用 IP 位址：</span><span class="sxs-lookup"><span data-stu-id="950e9-127">The following example creates a public IP address named `myPublicIP`:</span></span>

```powershell
$pip = New-AzureRmPublicIpAddress `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -AllocationMethod Static `
  -Name myPublicIP
```

### <a name="create-load-balancer"></a><span data-ttu-id="950e9-128">建立負載平衡器</span><span class="sxs-lookup"><span data-stu-id="950e9-128">Create load balancer</span></span>

<span data-ttu-id="950e9-129">使用 [New-AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig) 建立前端 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="950e9-129">Create a frontend IP address with [New-AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig).</span></span> <span data-ttu-id="950e9-130">下列範例會建立名為 `myFrontEndPool` 的前端 IP 位址：</span><span class="sxs-lookup"><span data-stu-id="950e9-130">The following example creates a frontend IP address named `myFrontEndPool`:</span></span> 

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name myFrontEndPool -PublicIpAddress $pip
```

<span data-ttu-id="950e9-131">使用 [New-AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig) 建立後端位址集區。</span><span class="sxs-lookup"><span data-stu-id="950e9-131">Create a backend address pool with [New-AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig).</span></span> <span data-ttu-id="950e9-132">下列範例會建立名為 `myBackEndPool` 的後端位址集區：</span><span class="sxs-lookup"><span data-stu-id="950e9-132">The following example creates a backend address pool named `myBackEndPool`:</span></span>

```powershell
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name myBackEndPool
```

<span data-ttu-id="950e9-133">現在，使用 [New-AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer) 建立負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="950e9-133">Now, create the load balancer with [New-AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer).</span></span> <span data-ttu-id="950e9-134">下列範例會使用 `myPublicIP` 位址建立名為 `myLoadBalancer` 的負載平衡器：</span><span class="sxs-lookup"><span data-stu-id="950e9-134">The following example creates a load balancer named `myLoadBalancer` using the `myPublicIP` address:</span></span>

```powershell
$lb = New-AzureRmLoadBalancer `
  -ResourceGroupName myResourceGroup `
  -Name myLoadBalancer `
  -Location westeurope `
  -FrontendIpConfiguration $frontendIP `
  -BackendAddressPool $backendPool
```

### <a name="create-health-probe"></a><span data-ttu-id="950e9-135">建立健全狀況探查</span><span class="sxs-lookup"><span data-stu-id="950e9-135">Create health probe</span></span>

<span data-ttu-id="950e9-136">若要讓負載平衡器監視您應用程式的狀態，請使用健康狀態探查。</span><span class="sxs-lookup"><span data-stu-id="950e9-136">To allow the load balancer to monitor the status of your app, you use a health probe.</span></span> <span data-ttu-id="950e9-137">健康狀態探查會根據 VM 對健康狀態檢查的回應，以動態方式從負載平衡器輪替中新增或移除 VM。</span><span class="sxs-lookup"><span data-stu-id="950e9-137">The health probe dynamically adds or removes VMs from the load balancer rotation based on their response to health checks.</span></span> <span data-ttu-id="950e9-138">根據預設，在 15 秒的間隔內連續發生兩次失敗後，VM 就會從負載平衡器分配中移除。</span><span class="sxs-lookup"><span data-stu-id="950e9-138">By default, a VM is removed from the load balancer distribution after two consecutive failures at 15-second intervals.</span></span>

<span data-ttu-id="950e9-139">使用 [Add-AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig) 建立健全狀況探查。</span><span class="sxs-lookup"><span data-stu-id="950e9-139">Create a health probe with [Add-AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig).</span></span> <span data-ttu-id="950e9-140">下列範例會建立名為 `myHealthProbe` 的健康狀態探查，以監視每部 VM：</span><span class="sxs-lookup"><span data-stu-id="950e9-140">The following example creates a health probe named `myHealthProbe` that monitors each VM:</span></span>

```powershell
Add-AzureRmLoadBalancerProbeConfig -Name myHealthProbe `
  -LoadBalancer $lb `
  -Protocol tcp `
  -Port 80 `
  -IntervalInSeconds 15 `
  -ProbeCount 2
```

### <a name="create-load-balancer-rule"></a><span data-ttu-id="950e9-141">建立負載平衡器規則</span><span class="sxs-lookup"><span data-stu-id="950e9-141">Create load balancer rule</span></span>

<span data-ttu-id="950e9-142">負載平衡器規則用來定義如何將流量分散至 VM。</span><span class="sxs-lookup"><span data-stu-id="950e9-142">A load balancer rule is used to define how traffic is distributed to the VMs.</span></span>

<span data-ttu-id="950e9-143">使用 [Add-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig) 建立負載平衡器規則。</span><span class="sxs-lookup"><span data-stu-id="950e9-143">Create a load balancer rule with [Add-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig).</span></span> <span data-ttu-id="950e9-144">下列範例會建立名為 `myLoadBalancerRule` 的負載平衡器規則，並平衡連接埠 `80` 上的流量：</span><span class="sxs-lookup"><span data-stu-id="950e9-144">The following example creates a load balancer rule named `myLoadBalancerRule` and balances traffic on port `80`:</span></span>

```powershell
Add-AzureRmLoadBalancerRuleConfig -Name myLoadBalancerRule `
  -LoadBalancer $lb `
  -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
  -BackendAddressPool $lb.BackendAddressPools[0] `
  -Protocol Tcp `
  -FrontendPort 80 `
  -BackendPort 80
```

<span data-ttu-id="950e9-145">使用 [Set-AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer) 更新負載平衡器：</span><span class="sxs-lookup"><span data-stu-id="950e9-145">Update the load balancer with [Set-AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):</span></span>

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```

## <a name="step-4---configure-networking"></a><span data-ttu-id="950e9-146">步驟 4 - 設定網路功能</span><span class="sxs-lookup"><span data-stu-id="950e9-146">Step 4 - Configure networking</span></span>

<span data-ttu-id="950e9-147">每部 VM 都有一或多個虛擬網路介面卡 (NIC) 可連接至虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="950e9-147">Each VM has one or more virtual network interface cards (NICs) that connect to a virtual network.</span></span> <span data-ttu-id="950e9-148">此虛擬網路受到保護，可根據定義的存取規則來篩選流量。</span><span class="sxs-lookup"><span data-stu-id="950e9-148">This virtual network is secured to filter traffic based on defined access rules.</span></span>

### <a name="create-virtual-network"></a><span data-ttu-id="950e9-149">建立虛擬網路</span><span class="sxs-lookup"><span data-stu-id="950e9-149">Create virtual network</span></span>

<span data-ttu-id="950e9-150">首先，使用 [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) 設定子網路。</span><span class="sxs-lookup"><span data-stu-id="950e9-150">First, configure a subnet with [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span></span> <span data-ttu-id="950e9-151">下列範例會建立名為 `mySubnet`的子網路：</span><span class="sxs-lookup"><span data-stu-id="950e9-151">The following example creates a subnet named `mySubnet`:</span></span>

```powershell
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name mySubnet -AddressPrefix 192.168.1.0/24
```

<span data-ttu-id="950e9-152">若要提供您 VM 的網路連線能力，請使用 [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) 建立虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="950e9-152">To provide network connectivity to your VMs, create a virtual network with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span></span> <span data-ttu-id="950e9-153">下列範例會建立名為 `myVnet` 且包含 `mySubnet` 的虛擬網路：</span><span class="sxs-lookup"><span data-stu-id="950e9-153">The following example creates a virtual network named `myVnet` with `mySubnet`:</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -Name myVnet `
  -AddressPrefix 192.168.0.0/16 `
  -Subnet $subnetConfig
```

### <a name="configure-network-security"></a><span data-ttu-id="950e9-154">設定網路安全性</span><span class="sxs-lookup"><span data-stu-id="950e9-154">Configure network security</span></span>

<span data-ttu-id="950e9-155">Azure [網路安全性群組](../../virtual-network/virtual-networks-nsg.md) (NSG) 控制一或多部虛擬機器的輸入和傳出流量。</span><span class="sxs-lookup"><span data-stu-id="950e9-155">An Azure [network security group](../../virtual-network/virtual-networks-nsg.md) (NSG) controls inbound and outbound traffic for one or many virtual machines.</span></span> <span data-ttu-id="950e9-156">網路安全性群組規則可允許或拒絕特定連接埠或連接埠範圍上的網路流量。</span><span class="sxs-lookup"><span data-stu-id="950e9-156">Network security group rules allow or deny network traffic on a specific port or port range.</span></span> <span data-ttu-id="950e9-157">這些規則也可以包含來源位址首碼，所以只有在預先定義的來源產生的流量可以與虛擬機器通訊。</span><span class="sxs-lookup"><span data-stu-id="950e9-157">These rules can also include a source address prefix so that only traffic originating at a predefined source can communicate with a virtual machine.</span></span>

<span data-ttu-id="950e9-158">若要允許 Web 流量連到您的應用程式，請使用 [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) 建立網路安全性群組規則。</span><span class="sxs-lookup"><span data-stu-id="950e9-158">To allow web traffic to reach your app, create a network security group rule with [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig).</span></span> <span data-ttu-id="950e9-159">下列範例會建立名為 `myNetworkSecurityGroupRule` 的網路安全性群組規則：</span><span class="sxs-lookup"><span data-stu-id="950e9-159">The following example creates a network security group rule named `myNetworkSecurityGroupRule`:</span></span>

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

<span data-ttu-id="950e9-160">使用 [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) 建立網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="950e9-160">Create a network security group with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup).</span></span> <span data-ttu-id="950e9-161">下列範例會建立名為 `myNetworkSecurityGroup` 的 NSG：</span><span class="sxs-lookup"><span data-stu-id="950e9-161">The following example creates an NSG named `myNetworkSecurityGroup`:</span></span>

```powershell
$nsg = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -Name myNetworkSecurityGroup `
  -SecurityRules $nsgRule
```

<span data-ttu-id="950e9-162">使用 [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig) 將網路安全性群組新增至子網路：</span><span class="sxs-lookup"><span data-stu-id="950e9-162">Add the network security group to the subnet with [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig):</span></span>

```powershell
Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet `
  -Name mySubnet `
  -NetworkSecurityGroup $nsg `
  -AddressPrefix 192.168.1.0/24
```

<span data-ttu-id="950e9-163">使用 [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork) 更新虛擬網路：</span><span class="sxs-lookup"><span data-stu-id="950e9-163">Update the virtual network with [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork):</span></span>

```powershell
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```

### <a name="create-virtual-network-interface-cards"></a><span data-ttu-id="950e9-164">建立虛擬網路介面卡</span><span class="sxs-lookup"><span data-stu-id="950e9-164">Create virtual network interface cards</span></span>

<span data-ttu-id="950e9-165">負載平衡器會搭配虛擬 NIC 資源運作，而不是實際的 VM。</span><span class="sxs-lookup"><span data-stu-id="950e9-165">Load balancers function with the virtual NIC resource rather than the actual VM.</span></span> <span data-ttu-id="950e9-166">虛擬 NIC 已連結至負載平衡器，然後連結至 VM。</span><span class="sxs-lookup"><span data-stu-id="950e9-166">The virtual NIC is connected to the load balancer, and then attached to a VM.</span></span>

<span data-ttu-id="950e9-167">使用 [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) 建立虛擬 NIC。</span><span class="sxs-lookup"><span data-stu-id="950e9-167">Create a virtual NIC with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span></span> <span data-ttu-id="950e9-168">下列範例會建立三個虛擬 NIC。</span><span class="sxs-lookup"><span data-stu-id="950e9-168">The following example creates three virtual NICs.</span></span> <span data-ttu-id="950e9-169">(您在下列步驟中針對應用程式建立的每部 VM 都有一個虛擬 NIC)︰</span><span class="sxs-lookup"><span data-stu-id="950e9-169">(One virtual NIC for each VM you create for your app in the following steps):</span></span>


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

## <a name="step-5---create-virtual-machines"></a><span data-ttu-id="950e9-170">步驟 5 - 建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="950e9-170">Step 5 - Create virtual machines</span></span>

<span data-ttu-id="950e9-171">備妥所有基礎元件，您現在可以建立高度可用的 VM 來執行您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="950e9-171">With all the underlying components in place, you can now create highly available VMs to run your app.</span></span> 

<span data-ttu-id="950e9-172">使用 [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential) 取得虛擬機器上系統管理員帳戶所需的使用者名稱和密碼：</span><span class="sxs-lookup"><span data-stu-id="950e9-172">Get the username and password needed for the administrator account on the virtual machine with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="950e9-173">使用 [New-AzureRmVMConfig](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/new-azurermvmconfig)、[Set-AzureRmVMOperatingSystem](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmoperatingsystem)、[Set-AzureRmVMSourceImage](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmsourceimage)、[Set-AzureRmVMOSDisk](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmosdisk)、[Add-AzureRmVMNetworkInterface](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/add-azurermvmnetworkinterface) 和 [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) 來建立 VM。</span><span class="sxs-lookup"><span data-stu-id="950e9-173">Create the VMs with [New-AzureRmVMConfig](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/new-azurermvmconfig), [Set-AzureRmVMOperatingSystem](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmoperatingsystem), [Set-AzureRmVMSourceImage](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmsourceimage), [Set-AzureRmVMOSDisk](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmosdisk), [Add-AzureRmVMNetworkInterface](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/add-azurermvmnetworkinterface), and [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="950e9-174">下列範例會建立三個 VM：</span><span class="sxs-lookup"><span data-stu-id="950e9-174">The following example creates three VMs:</span></span>

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

<span data-ttu-id="950e9-175">建立和設定這三部 VM 需要數分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="950e9-175">It takes several minutes to create and configure all three VMs.</span></span> <span data-ttu-id="950e9-176">負載平衡器會自動偵測應用程式何時在每部 VM 上執行。</span><span class="sxs-lookup"><span data-stu-id="950e9-176">The load balancer health probe automatically detects when the app is running on each VM.</span></span> <span data-ttu-id="950e9-177">當應用程式正在執行時，負載平衡器規則就開始分配流量。</span><span class="sxs-lookup"><span data-stu-id="950e9-177">Once the app is running, the load balancer rule starts to distribute traffic.</span></span>

### <a name="install-the-app"></a><span data-ttu-id="950e9-178">安裝應用程式</span><span class="sxs-lookup"><span data-stu-id="950e9-178">Install the app</span></span> 

<span data-ttu-id="950e9-179">Azure 虛擬機器擴充功能是用來自動化虛擬機器組態工作，例如安裝應用程式和設定作業系統。</span><span class="sxs-lookup"><span data-stu-id="950e9-179">Azure virtual machine extensions are used to automate virtual machine configuration tasks such as installing applications and configuring the operating system.</span></span> <span data-ttu-id="950e9-180">[適用於 Windows 的自訂指令碼擴充功能](./../virtual-machines-windows-extensions-customscript.md)是用來在虛擬機器上執行任何 PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="950e9-180">The [custom script extension for Windows](./../virtual-machines-windows-extensions-customscript.md) is used to run any PowerShell script on the virtual machine.</span></span> <span data-ttu-id="950e9-181">指令碼可以儲存在 Azure 儲存體、任何可存取的 HTTP 端點，或內嵌在自訂指令碼擴充功能組態。</span><span class="sxs-lookup"><span data-stu-id="950e9-181">The script can be stored in Azure storage, any accessible HTTP endpoint, or embedded in the custom script extension configuration.</span></span> <span data-ttu-id="950e9-182">使用自訂指令碼擴充功能時，Azure VM 代理程式會管理指令碼執行。</span><span class="sxs-lookup"><span data-stu-id="950e9-182">When using the custom script extension, the Azure VM agent manages the script execution.</span></span>

<span data-ttu-id="950e9-183">使用 [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) 來安裝自訂指令碼擴充功能。</span><span class="sxs-lookup"><span data-stu-id="950e9-183">Use [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) to install the custom script extension.</span></span> <span data-ttu-id="950e9-184">擴充功能會執行 `powershell Add-WindowsFeature Web-Server` 以安裝 IIS Web 伺服器：</span><span class="sxs-lookup"><span data-stu-id="950e9-184">The extension runs `powershell Add-WindowsFeature Web-Server` to install the IIS webserver:</span></span>

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

### <a name="test-your-app"></a><span data-ttu-id="950e9-185">測試應用程式</span><span class="sxs-lookup"><span data-stu-id="950e9-185">Test your app</span></span>

<span data-ttu-id="950e9-186">使用 [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) 取得負載平衡器的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="950e9-186">Obtain the public IP address of your load balancer with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="950e9-187">下列範例會取得稍早建立之 `myPublicIP` 的 IP 位址︰</span><span class="sxs-lookup"><span data-stu-id="950e9-187">The following example obtains the IP address for `myPublicIP` created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress -ResourceGroupName myResourceGroup -Name myPublicIP | select IpAddress
```

<span data-ttu-id="950e9-188">在 Web 瀏覽器中輸入公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="950e9-188">Enter the public IP address in to a web browser.</span></span> <span data-ttu-id="950e9-189">備妥 NSG 規則，就會顯示預設 IIS 網站。</span><span class="sxs-lookup"><span data-stu-id="950e9-189">With the NSG rule in place, the default IIS website is displayed.</span></span> 

![IIS 預設網站](media/load-balanced-iis-tutorial/iis.png)

## <a name="step-6--management-tasks"></a><span data-ttu-id="950e9-191">步驟 6 - 管理工作</span><span class="sxs-lookup"><span data-stu-id="950e9-191">Step 6 – Management tasks</span></span>

<span data-ttu-id="950e9-192">您可能需要在執行您應用程式的 VM 上執行維護，例如安裝 OS 更新。</span><span class="sxs-lookup"><span data-stu-id="950e9-192">You may need to perform maintenance on the VMs running your app, such as installing OS updates.</span></span> <span data-ttu-id="950e9-193">若要處理您應用程式增加的流量，您可能需要新增額外的 VM。</span><span class="sxs-lookup"><span data-stu-id="950e9-193">To deal with increased traffic to your app, you may need to add additional VMs.</span></span> <span data-ttu-id="950e9-194">本節說明如何在負載平衡器中移除或新增 VM。</span><span class="sxs-lookup"><span data-stu-id="950e9-194">This section shows you how to remove or add a VM from the load balancer.</span></span> 

### <a name="remove-a-vm-from-the-load-balancer"></a><span data-ttu-id="950e9-195">從負載平衡器移除 VM</span><span class="sxs-lookup"><span data-stu-id="950e9-195">Remove a VM from the load balancer</span></span>

<span data-ttu-id="950e9-196">重設網路介面卡的 LoadBalancerBackendAddressPools 屬性，以從後端位址集區移除 VM。</span><span class="sxs-lookup"><span data-stu-id="950e9-196">Remove a VM from the backend address pool by resetting the LoadBalancerBackendAddressPools property of the network interface card.</span></span>

<span data-ttu-id="950e9-197">使用 [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface) 取得網路介面卡：</span><span class="sxs-lookup"><span data-stu-id="950e9-197">Get the network interface card with [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface):</span></span>

```powershell
$nic = Get-AzureRmNetworkInterface -ResourceGroupName myResourceGroup -Name myNic2
``` 

<span data-ttu-id="950e9-198">將網路介面卡的 LoadBalancerBackendAddressPools 屬性設為 $null：</span><span class="sxs-lookup"><span data-stu-id="950e9-198">Set the LoadBalancerBackendAddressPools property of the network interface card to $null:</span></span>

```powershell
$nic.Ipconfigurations[0].LoadBalancerBackendAddressPools=$null
```

<span data-ttu-id="950e9-199">更新網路介面卡：</span><span class="sxs-lookup"><span data-stu-id="950e9-199">Update the network interface card:</span></span>

```powershell
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

### <a name="add-a-vm-to-the-load-balancer"></a><span data-ttu-id="950e9-200">將 VM 新增至負載平衡器</span><span class="sxs-lookup"><span data-stu-id="950e9-200">Add a VM to the load balancer</span></span>

<span data-ttu-id="950e9-201">在執行 VM 維護之後，或者如果需要擴充容量，請將 VM 的 NIC 新增至負載平衡器的後端位址集區。</span><span class="sxs-lookup"><span data-stu-id="950e9-201">After performing VM maintenance, or if you need to expand capacity, adding the NIC of a VM to the backend address pool of the load balancer.</span></span>

<span data-ttu-id="950e9-202">取得負載平衡器：</span><span class="sxs-lookup"><span data-stu-id="950e9-202">Get the load balancer:</span></span>

```powershell
$lb = Get-AzureRMLoadBalancer -ResourceGroupName myResourceGroup -Name myLoadBalancer 
```

<span data-ttu-id="950e9-203">將負載平衡器的後端位址集區新增至網路介面卡：</span><span class="sxs-lookup"><span data-stu-id="950e9-203">Add the backend address pool of the load balancer to the network interface card:</span></span>

```powershell
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$lb.BackendAddressPools[0]
```

<span data-ttu-id="950e9-204">更新網路介面卡：</span><span class="sxs-lookup"><span data-stu-id="950e9-204">Update the network interface card:</span></span>

```powershell
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

## <a name="next-steps"></a><span data-ttu-id="950e9-205">後續步驟</span><span class="sxs-lookup"><span data-stu-id="950e9-205">Next Steps</span></span>

<span data-ttu-id="950e9-206">範例 – [Azure 虛擬機器 PowerShell 範例指令碼](./../virtual-machines-windows-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="950e9-206">Samples – [Azure Virtual Machine PowerShell sample scripts](./../virtual-machines-windows-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>
