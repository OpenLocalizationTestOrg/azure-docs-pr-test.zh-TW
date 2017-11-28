---
title: "aaaHow tooload 平衡在 Azure 中的 Windows 虛擬機器 |Microsoft 文件"
description: "了解如何 toouse hello Azure 跨越三個 Windows Vm 的負載平衡器 toocreate 高度可用且安全的應用程式"
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
ms.openlocfilehash: bfbd6a24e90a33e60d7d4f7b0c471af5d4e71f45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooload-balance-windows-virtual-machines-in-azure-toocreate-a-highly-available-application"></a><span data-ttu-id="5b445-103">如何 tooload 會平衡 Azure toocreate 中的 Windows 虛擬機器的高可用性的應用程式</span><span class="sxs-lookup"><span data-stu-id="5b445-103">How tooload balance Windows virtual machines in Azure toocreate a highly available application</span></span>
<span data-ttu-id="5b445-104">負載平衡會將傳入要求分散到多部虛擬機器，藉此提供高可用性。</span><span class="sxs-lookup"><span data-stu-id="5b445-104">Load balancing provides a higher level of availability by spreading incoming requests across multiple virtual machines.</span></span> <span data-ttu-id="5b445-105">在本教學課程中，您會了解 hello 的不同元件 hello Azure 負載平衡器會將流量，以及提供高可用性。</span><span class="sxs-lookup"><span data-stu-id="5b445-105">In this tutorial, you learn about hello different components of hello Azure load balancer that distribute traffic and provide high availability.</span></span> <span data-ttu-id="5b445-106">您會了解如何：</span><span class="sxs-lookup"><span data-stu-id="5b445-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="5b445-107">建立 Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="5b445-107">Create an Azure load balancer</span></span>
> * <span data-ttu-id="5b445-108">建立負載平衡器健全狀況探查</span><span class="sxs-lookup"><span data-stu-id="5b445-108">Create a load balancer health probe</span></span>
> * <span data-ttu-id="5b445-109">建立負載平衡器流量規則</span><span class="sxs-lookup"><span data-stu-id="5b445-109">Create load balancer traffic rules</span></span>
> * <span data-ttu-id="5b445-110">使用 hello 自訂指令碼擴充 toocreate 基本的 IIS 站台</span><span class="sxs-lookup"><span data-stu-id="5b445-110">Use hello Custom Script Extension toocreate a basic IIS site</span></span>
> * <span data-ttu-id="5b445-111">建立虛擬機器，並附加 tooa 負載平衡器</span><span class="sxs-lookup"><span data-stu-id="5b445-111">Create virtual machines and attach tooa load balancer</span></span>
> * <span data-ttu-id="5b445-112">檢視作用中的負載平衡器</span><span class="sxs-lookup"><span data-stu-id="5b445-112">View a load balancer in action</span></span>
> * <span data-ttu-id="5b445-113">新增和移除虛擬機器的負載平衡器</span><span class="sxs-lookup"><span data-stu-id="5b445-113">Add and remove VMs from a load balancer</span></span>

<span data-ttu-id="5b445-114">本教學課程需要 hello Azure PowerShell 模組版本 3.6 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="5b445-114">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="5b445-115">執行` Get-Module -ListAvailable AzureRM`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="5b445-115">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="5b445-116">如果您需要 tooupgrade，請參閱[安裝 Azure PowerShell 模組](/powershell/azure/install-azurerm-ps)。</span><span class="sxs-lookup"><span data-stu-id="5b445-116">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>


## <a name="azure-load-balancer-overview"></a><span data-ttu-id="5b445-117">Azure Load Balancer 概觀</span><span class="sxs-lookup"><span data-stu-id="5b445-117">Azure load balancer overview</span></span>
<span data-ttu-id="5b445-118">Azure Load Balancer 是 Layer-4 (TCP、UDP) 負載平衡器，可將連入流量分散於狀況良好的 VM 來提供高可用性。</span><span class="sxs-lookup"><span data-stu-id="5b445-118">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer that provides high availability by distributing incoming traffic among healthy VMs.</span></span> <span data-ttu-id="5b445-119">負載平衡器健全狀況探查監視每個 VM 上指定的連接埠，並只會發佈流量 tooan 操作的 VM。</span><span class="sxs-lookup"><span data-stu-id="5b445-119">A load balancer health probe monitors a given port on each VM and only distributes traffic tooan operational VM.</span></span>

<span data-ttu-id="5b445-120">您可定義含有一或多個公用 IP 位址的前端 IP 組態。</span><span class="sxs-lookup"><span data-stu-id="5b445-120">You define a front-end IP configuration that contains one or more public IP addresses.</span></span> <span data-ttu-id="5b445-121">此前端 IP 組態可讓您的負載平衡器和應用程式 toobe 存取透過 hello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="5b445-121">This front-end IP configuration allows your load balancer and applications toobe accessible over hello Internet.</span></span> 

<span data-ttu-id="5b445-122">虛擬機器連接 tooa 負載平衡器使用他們的虛擬網路介面卡 (NIC)。</span><span class="sxs-lookup"><span data-stu-id="5b445-122">Virtual machines connect tooa load balancer using their virtual network interface card (NIC).</span></span> <span data-ttu-id="5b445-123">toodistribute 流量 toohello Vm 後, 端位址集區包含 hello hello 虛擬 (Nic) 連線的 toohello 負載平衡器的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="5b445-123">toodistribute traffic toohello VMs, a back-end address pool contains hello IP addresses of hello virtual (NICs) connected toohello load balancer.</span></span>

<span data-ttu-id="5b445-124">toocontrol hello 流量的流量，您會定義特定連接埠和通訊協定對應 tooyour Vm 的負載平衡器規則。</span><span class="sxs-lookup"><span data-stu-id="5b445-124">toocontrol hello flow of traffic, you define load balancer rules for specific ports and protocols that map tooyour VMs.</span></span>


## <a name="create-azure-load-balancer"></a><span data-ttu-id="5b445-125">建立 Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="5b445-125">Create Azure load balancer</span></span>
<span data-ttu-id="5b445-126">本節將詳細說明如何建立及設定 hello 負載平衡器的每個元件。</span><span class="sxs-lookup"><span data-stu-id="5b445-126">This section details how you can create and configure each component of hello load balancer.</span></span> <span data-ttu-id="5b445-127">請先使用 [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) 來建立資源群組，才可建立負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="5b445-127">Before you can create your load balancer, create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="5b445-128">hello 下列範例會建立名為的資源群組*myResourceGroupLoadBalancer*在 hello *EastUS*位置：</span><span class="sxs-lookup"><span data-stu-id="5b445-128">hello following example creates a resource group named *myResourceGroupLoadBalancer* in hello *EastUS* location:</span></span>

```powershell
New-AzureRmResourceGroup `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS
```

### <a name="create-a-public-ip-address"></a><span data-ttu-id="5b445-129">建立公用 IP 位址</span><span class="sxs-lookup"><span data-stu-id="5b445-129">Create a public IP address</span></span>
<span data-ttu-id="5b445-130">tooaccess 上的應用程式 hello 網際網路，您就需要公用 IP 位址 hello 負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="5b445-130">tooaccess your app on hello Internet, you need a public IP address for hello load balancer.</span></span> <span data-ttu-id="5b445-131">使用 [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) 建立公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="5b445-131">Create a public IP address with [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span></span> <span data-ttu-id="5b445-132">hello 下列範例會建立名為的公用 IP 位址*myPublicIP*在 hello *myResourceGroupLoadBalancer*資源群組：</span><span class="sxs-lookup"><span data-stu-id="5b445-132">hello following example creates a public IP address named *myPublicIP* in hello *myResourceGroupLoadBalancer* resource group:</span></span>

```powershell
$publicIP = New-AzureRmPublicIpAddress `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS `
  -AllocationMethod Static `
  -Name myPublicIP
```

### <a name="create-a-load-balancer"></a><span data-ttu-id="5b445-133">建立負載平衡器</span><span class="sxs-lookup"><span data-stu-id="5b445-133">Create a load balancer</span></span>
<span data-ttu-id="5b445-134">使用 [New-AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig) 建立前端 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="5b445-134">Create a frontend IP address with [New-AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig).</span></span> <span data-ttu-id="5b445-135">hello 下列範例會建立名為的前端 IP 位址*myFrontEndPool*:</span><span class="sxs-lookup"><span data-stu-id="5b445-135">hello following example creates a frontend IP address named *myFrontEndPool*:</span></span> 

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig `
  -Name myFrontEndPool `
  -PublicIpAddress $publicIP
```

<span data-ttu-id="5b445-136">使用 [New-AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig) 建立後端位址集區。</span><span class="sxs-lookup"><span data-stu-id="5b445-136">Create a backend address pool with [New-AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig).</span></span> <span data-ttu-id="5b445-137">hello 下列範例會建立名為後端位址集區*myBackEndPool*:</span><span class="sxs-lookup"><span data-stu-id="5b445-137">hello following example creates a backend address pool named *myBackEndPool*:</span></span>

```powershell
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name myBackEndPool
```

<span data-ttu-id="5b445-138">現在，建立 hello 的負載平衡器[新增 AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer)。</span><span class="sxs-lookup"><span data-stu-id="5b445-138">Now, create hello load balancer with [New-AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer).</span></span> <span data-ttu-id="5b445-139">hello 下列範例會建立名為負載平衡器*myLoadBalancer*使用 hello *myPublicIP*位址：</span><span class="sxs-lookup"><span data-stu-id="5b445-139">hello following example creates a load balancer named *myLoadBalancer* using hello *myPublicIP* address:</span></span>

```powershell
$lb = New-AzureRmLoadBalancer `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myLoadBalancer `
  -Location EastUS `
  -FrontendIpConfiguration $frontendIP `
  -BackendAddressPool $backendPool
```

### <a name="create-a-health-probe"></a><span data-ttu-id="5b445-140">建立健康狀態探查</span><span class="sxs-lookup"><span data-stu-id="5b445-140">Create a health probe</span></span>
<span data-ttu-id="5b445-141">tooallow hello 負載平衡器 toomonitor hello 狀態的應用程式，您可以使用健全狀況探查。</span><span class="sxs-lookup"><span data-stu-id="5b445-141">tooallow hello load balancer toomonitor hello status of your app, you use a health probe.</span></span> <span data-ttu-id="5b445-142">hello 健全狀況探查以動態方式加入或移除 hello 負載平衡器輪替根據其回應 toohealth 檢查 Vm。</span><span class="sxs-lookup"><span data-stu-id="5b445-142">hello health probe dynamically adds or removes VMs from hello load balancer rotation based on their response toohealth checks.</span></span> <span data-ttu-id="5b445-143">根據預設，VM 會移除從 15 秒的間隔的兩個連續多次失敗後的 hello 負載平衡器發佈。</span><span class="sxs-lookup"><span data-stu-id="5b445-143">By default, a VM is removed from hello load balancer distribution after two consecutive failures at 15-second intervals.</span></span> <span data-ttu-id="5b445-144">您可根據通訊協定或您應用程式的特定健康狀態檢查頁面，建立健康狀態探查。</span><span class="sxs-lookup"><span data-stu-id="5b445-144">You create a health probe based on a protocol or a specific health check page for your app.</span></span> 

<span data-ttu-id="5b445-145">hello 下列範例會建立 TCP 探查。</span><span class="sxs-lookup"><span data-stu-id="5b445-145">hello following example creates a TCP probe.</span></span> <span data-ttu-id="5b445-146">您也可以建立自訂 HTTP 探查，以進行更精細的健康狀態檢查。</span><span class="sxs-lookup"><span data-stu-id="5b445-146">You can also create custom HTTP probes for more fine grained health checks.</span></span> <span data-ttu-id="5b445-147">時使用自訂的 HTTP 探查，您必須建立 hello 健康情況檢查 頁面上，例如*healthcheck.aspx*。</span><span class="sxs-lookup"><span data-stu-id="5b445-147">When using a custom HTTP probe, you must create hello health check page, such as *healthcheck.aspx*.</span></span> <span data-ttu-id="5b445-148">必須傳回 hello 探查**HTTP 200 「 確定**回應 hello 負載平衡器 tookeep hello 中主機的旋轉。</span><span class="sxs-lookup"><span data-stu-id="5b445-148">hello probe must return an **HTTP 200 OK** response for hello load balancer tookeep hello host in rotation.</span></span>

<span data-ttu-id="5b445-149">您使用 toocreate TCP 健全狀況探查，[新增 AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig)。</span><span class="sxs-lookup"><span data-stu-id="5b445-149">toocreate a TCP health probe, you use [Add-AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig).</span></span> <span data-ttu-id="5b445-150">hello 下列範例會建立名為健全狀況探查*myHealthProbe* ，監視每個 VM:</span><span class="sxs-lookup"><span data-stu-id="5b445-150">hello following example creates a health probe named *myHealthProbe* that monitors each VM:</span></span>

```powershell
Add-AzureRmLoadBalancerProbeConfig `
  -Name myHealthProbe `
  -LoadBalancer $lb `
  -Protocol tcp `
  -Port 80 `
  -IntervalInSeconds 15 `
  -ProbeCount 2
```

<span data-ttu-id="5b445-151">更新與 hello 負載平衡器[組 AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):</span><span class="sxs-lookup"><span data-stu-id="5b445-151">Update hello load balancer with [Set-AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):</span></span>

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```

### <a name="create-a-load-balancer-rule"></a><span data-ttu-id="5b445-152">建立負載平衡器規則</span><span class="sxs-lookup"><span data-stu-id="5b445-152">Create a load balancer rule</span></span>
<span data-ttu-id="5b445-153">負載平衡器規則是使用的 toodefine 流量的分散式的 toohello Vm 的方式。</span><span class="sxs-lookup"><span data-stu-id="5b445-153">A load balancer rule is used toodefine how traffic is distributed toohello VMs.</span></span> <span data-ttu-id="5b445-154">您定義 hello 連入流量和 hello 後端 IP 集區 tooreceive hello 流量，以及 hello 必要的來源和目的地連接埠 hello 前端 IP 組態。</span><span class="sxs-lookup"><span data-stu-id="5b445-154">You define hello front-end IP configuration for hello incoming traffic and hello back-end IP pool tooreceive hello traffic, along with hello required source and destination port.</span></span> <span data-ttu-id="5b445-155">toomake 確定只有狀況良好的 Vm 接收流量，您也定義 hello 健全狀況探查 toouse。</span><span class="sxs-lookup"><span data-stu-id="5b445-155">toomake sure only healthy VMs receive traffic, you also define hello health probe toouse.</span></span>

<span data-ttu-id="5b445-156">使用 [Add-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig) 建立負載平衡器規則。</span><span class="sxs-lookup"><span data-stu-id="5b445-156">Create a load balancer rule with [Add-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig).</span></span> <span data-ttu-id="5b445-157">hello 下列範例會建立名為的負載平衡器規則*myLoadBalancerRule*平衡連接埠上的流量和*80*:</span><span class="sxs-lookup"><span data-stu-id="5b445-157">hello following example creates a load balancer rule named *myLoadBalancerRule* and balances traffic on port *80*:</span></span>

```powershell
$probe = Get-AzureRmLoadBalancerProbeConfig -LoadBalancer $lb -Name myHealthProbe

Add-AzureRmLoadBalancerRuleConfig `
  -Name myLoadBalancerRule `
  -LoadBalancer $lb `
  -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
  -BackendAddressPool $lb.BackendAddressPools[0] `
  -Protocol Tcp `
  -FrontendPort 80 `
  -BackendPort 80 `
  -Probe $probe
```

<span data-ttu-id="5b445-158">更新與 hello 負載平衡器[組 AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):</span><span class="sxs-lookup"><span data-stu-id="5b445-158">Update hello load balancer with [Set-AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):</span></span>

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```


## <a name="configure-virtual-network"></a><span data-ttu-id="5b445-159">設定虛擬網路</span><span class="sxs-lookup"><span data-stu-id="5b445-159">Configure virtual network</span></span>
<span data-ttu-id="5b445-160">您將一些 Vm 部署，並可以測試您平衡器之前，先建立 hello 支援的虛擬網路資源。</span><span class="sxs-lookup"><span data-stu-id="5b445-160">Before you deploy some VMs and can test your balancer, create hello supporting virtual network resources.</span></span> <span data-ttu-id="5b445-161">如需有關虛擬網路的詳細資訊，請參閱 hello[管理 Azure 虛擬網路](tutorial-virtual-network.md)教學課程。</span><span class="sxs-lookup"><span data-stu-id="5b445-161">For more information about virtual networks, see hello [Manage Azure Virtual Networks](tutorial-virtual-network.md) tutorial.</span></span>

### <a name="create-network-resources"></a><span data-ttu-id="5b445-162">建立網路資源</span><span class="sxs-lookup"><span data-stu-id="5b445-162">Create network resources</span></span>
<span data-ttu-id="5b445-163">使用 [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) 建立虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="5b445-163">Create a virtual network with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span></span> <span data-ttu-id="5b445-164">hello 下列範例會建立虛擬網路，名為*myVnet*與*mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="5b445-164">hello following example creates a virtual network named *myVnet* with *mySubnet*:</span></span>

```powershell
# Create subnet config
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
  -Name mySubnet `
  -AddressPrefix 192.168.1.0/24

# Create hello virtual network
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS `
  -Name myVnet `
  -AddressPrefix 192.168.0.0/16 `
  -Subnet $subnetConfig
```

<span data-ttu-id="5b445-165">使用 [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) 建立網路安全性群組規則，然後使用 [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) 建立網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="5b445-165">Create a network security group rule with [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig), then create a network security group with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup).</span></span> <span data-ttu-id="5b445-166">新增 hello 安全性群組 toohello 子網路與[組 AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig)然後再更新 hello 虛擬網路與[組 AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork)。</span><span class="sxs-lookup"><span data-stu-id="5b445-166">Add hello network security group toohello subnet with [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig) and then update hello virtual network with [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork).</span></span> 

<span data-ttu-id="5b445-167">hello 下列範例會建立網路安全性群組規則命名為*myNetworkSecurityGroup*並將其套用太*mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="5b445-167">hello following example creates a network security group rule named *myNetworkSecurityGroup* and applies it too*mySubnet*:</span></span>

```powershell
# Create security rule config
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

# Create hello network security group
$nsg = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS `
  -Name myNetworkSecurityGroup `
  -SecurityRules $nsgRule

# Apply hello network security group tooa subnet
Set-AzureRmVirtualNetworkSubnetConfig `
  -VirtualNetwork $vnet `
  -Name mySubnet `
  -NetworkSecurityGroup $nsg `
  -AddressPrefix 192.168.1.0/24

# Update hello virtual network
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```

<span data-ttu-id="5b445-168">使用 [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) 建立虛擬 NIC。</span><span class="sxs-lookup"><span data-stu-id="5b445-168">Virtual NICs are created with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span></span> <span data-ttu-id="5b445-169">hello 下列範例會建立三個虛擬 Nic。</span><span class="sxs-lookup"><span data-stu-id="5b445-169">hello following example creates three virtual NICs.</span></span> <span data-ttu-id="5b445-170">（每個 VM 的虛擬 NIC 建立 hello 下列中的應用程式的步驟）。</span><span class="sxs-lookup"><span data-stu-id="5b445-170">(One virtual NIC for each VM you create for your app in hello following steps).</span></span> <span data-ttu-id="5b445-171">您可以隨時建立其他虛擬 Nic 和 Vm，並將它們加入 toohello 負載平衡器：</span><span class="sxs-lookup"><span data-stu-id="5b445-171">You can create additional virtual NICs and VMs at any time and add them toohello load balancer:</span></span>

```powershell
for ($i=1; $i -le 3; $i++)
{
   New-AzureRmNetworkInterface `
     -ResourceGroupName myResourceGroupLoadBalancer `
     -Name myNic$i `
     -Location EastUS `
     -Subnet $vnet.Subnets[0] `
     -LoadBalancerBackendAddressPool $lb.BackendAddressPools[0]
}
```

## <a name="create-virtual-machines"></a><span data-ttu-id="5b445-172">建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="5b445-172">Create virtual machines</span></span>
<span data-ttu-id="5b445-173">tooimprove hello 高可用性的應用程式會將您的 Vm 放在可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="5b445-173">tooimprove hello high availability of your app, place your VMs in an availability set.</span></span>

<span data-ttu-id="5b445-174">使用 [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset) 建立可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="5b445-174">Create an availability set with [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span></span> <span data-ttu-id="5b445-175">hello 下列範例會建立可用性設定組具名*myAvailabilitySet*:</span><span class="sxs-lookup"><span data-stu-id="5b445-175">hello following example creates an availability set named *myAvailabilitySet*:</span></span>

```powershell
$availabilitySet = New-AzureRmAvailabilitySet `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myAvailabilitySet `
  -Location EastUS `
  -Managed `
  -PlatformFaultDomainCount 3 `
  -PlatformUpdateDomainCount 2
```

<span data-ttu-id="5b445-176">設定系統管理員使用者名稱和密碼具有 hello Vm [Get-credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="5b445-176">Set an administrator username and password for hello VMs with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="5b445-177">現在您可以建立與 hello Vm[新增 AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm)。</span><span class="sxs-lookup"><span data-stu-id="5b445-177">Now you can create hello VMs with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="5b445-178">hello 下列範例會建立三個 Vm:</span><span class="sxs-lookup"><span data-stu-id="5b445-178">hello following example creates three VMs:</span></span>

```powershell
for ($i=1; $i -le 3; $i++)
{
  $vm = New-AzureRmVMConfig `
    -VMName myVM$i `
    -VMSize Standard_D1 `
    -AvailabilitySetId $availabilitySet.Id
  $vm = Set-AzureRmVMOperatingSystem `
    -VM $vm `
    -Windows `
    -ComputerName myVM$i `
    -Credential $cred `
    -ProvisionVMAgent `
    -EnableAutoUpdate
  $vm = Set-AzureRmVMSourceImage `
    -VM $vm `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter `
    -Version latest
  $vm = Set-AzureRmVMOSDisk `
    -VM $vm `
    -Name myOsDisk$i `
    -DiskSizeInGB 128 `
    -CreateOption FromImage `
    -Caching ReadWrite
  $nic = Get-AzureRmNetworkInterface `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Name myNic$i
  $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
  New-AzureRmVM `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Location EastUS `
    -VM $vm
}
```

<span data-ttu-id="5b445-179">它會採用幾分鐘的時間 toocreate 並設定所有三個 Vm。</span><span class="sxs-lookup"><span data-stu-id="5b445-179">It takes a few minutes toocreate and configure all three VMs.</span></span>

### <a name="install-iis-with-custom-script-extension"></a><span data-ttu-id="5b445-180">安裝 IIS 與自訂指令碼擴充功能</span><span class="sxs-lookup"><span data-stu-id="5b445-180">Install IIS with Custom Script Extension</span></span>
<span data-ttu-id="5b445-181">在上一個教學課程中，在[如何 toocustomize Windows 虛擬機器](tutorial-automate-vm-deployment.md)，您學到如何與 tooautomate VM 自訂 hello 自訂指令碼延伸的視窗。</span><span class="sxs-lookup"><span data-stu-id="5b445-181">In a previous tutorial on [How toocustomize a Windows virtual machine](tutorial-automate-vm-deployment.md), you learned how tooautomate VM customization with hello Custom Script Extension for Windows.</span></span> <span data-ttu-id="5b445-182">您可以使用 hello 相同 tooinstall 會很接近，且您的 Vm 上設定 IIS。</span><span class="sxs-lookup"><span data-stu-id="5b445-182">You can use hello same approach tooinstall and configure IIS on your VMs.</span></span>

<span data-ttu-id="5b445-183">使用[組 AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall hello 自訂指令碼擴充。</span><span class="sxs-lookup"><span data-stu-id="5b445-183">Use [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall hello Custom Script Extension.</span></span> <span data-ttu-id="5b445-184">hello 延伸模組執行`powershell Add-WindowsFeature Web-Server`tooinstall hello IIS 網頁伺服器，然後再更新 hello *Default.htm*頁面 tooshow hello 主機名稱的 hello VM:</span><span class="sxs-lookup"><span data-stu-id="5b445-184">hello extension runs `powershell Add-WindowsFeature Web-Server` tooinstall hello IIS webserver and then updates hello *Default.htm* page tooshow hello hostname of hello VM:</span></span>

```powershell
for ($i=1; $i -le 3; $i++)
{
   Set-AzureRmVMExtension `
     -ResourceGroupName myResourceGroupLoadBalancer `
     -ExtensionName IIS `
     -VMName myVM$i `
     -Publisher Microsoft.Compute `
     -ExtensionType CustomScriptExtension `
     -TypeHandlerVersion 1.4 `
     -SettingString '{"commandToExecute":"powershell Add-WindowsFeature Web-Server; powershell Add-Content -Path \"C:\\inetpub\\wwwroot\\Default.htm\" -Value $($env:computername)"}' `
     -Location EastUS
}
```

## <a name="test-load-balancer"></a><span data-ttu-id="5b445-185">測試負載平衡器</span><span class="sxs-lookup"><span data-stu-id="5b445-185">Test load balancer</span></span>
<span data-ttu-id="5b445-186">取得您的負載平衡器的 hello 公用 IP 位址[Get AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress)。</span><span class="sxs-lookup"><span data-stu-id="5b445-186">Obtain hello public IP address of your load balancer with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="5b445-187">hello 下列範例會取得 IP 位址 hello *myPublicIP*稍早建立：</span><span class="sxs-lookup"><span data-stu-id="5b445-187">hello following example obtains hello IP address for *myPublicIP* created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myPublicIP | select IpAddress
```

<span data-ttu-id="5b445-188">然後，您就可以 tooa 網頁瀏覽器中輸入 hello 公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="5b445-188">You can then enter hello public IP address in tooa web browser.</span></span> <span data-ttu-id="5b445-189">hello 網站將會顯示，包括 hello hello VM 主機名稱的 hello 負載平衡器分散流量 tooas hello 下列範例中：</span><span class="sxs-lookup"><span data-stu-id="5b445-189">hello website is displayed, including hello hostname of hello VM that hello load balancer distributed traffic tooas in hello following example:</span></span>

![執行中的 IIS 網站](./media/tutorial-load-balancer/running-iis-website.png)

<span data-ttu-id="5b445-191">toosee hello 負載平衡器會將流量分散到執行您的應用程式的所有三個 Vm，您可以強制重新整理您的 web 瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="5b445-191">toosee hello load balancer distribute traffic across all three VMs running your app, you can force-refresh your web browser.</span></span>


## <a name="add-and-remove-vms"></a><span data-ttu-id="5b445-192">新增和移除 VM</span><span class="sxs-lookup"><span data-stu-id="5b445-192">Add and remove VMs</span></span>
<span data-ttu-id="5b445-193">您可能需要 tooperform hello 執行您的應用程式，例如安裝作業系統更新的 Vm 上的維護。</span><span class="sxs-lookup"><span data-stu-id="5b445-193">You may need tooperform maintenance on hello VMs running your app, such as installing OS updates.</span></span> <span data-ttu-id="5b445-194">toodeal 使用增加的流量 tooyour 應用程式，您可能需要 tooadd 其他 Vm。</span><span class="sxs-lookup"><span data-stu-id="5b445-194">toodeal with increased traffic tooyour app, you may need tooadd additional VMs.</span></span> <span data-ttu-id="5b445-195">這個區段會顯示如何 tooremove 或加入 VM 從 hello 負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="5b445-195">This section shows you how tooremove or add a VM from hello load balancer.</span></span>

### <a name="remove-a-vm-from-hello-load-balancer"></a><span data-ttu-id="5b445-196">從 hello 負載平衡器移除 VM</span><span class="sxs-lookup"><span data-stu-id="5b445-196">Remove a VM from hello load balancer</span></span>
<span data-ttu-id="5b445-197">取得與 hello 網路介面卡[Get AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface)，然後設定 hello*了 LoadBalancerBackendAddressPools*屬性太 hello 虛擬 NIC*$null*。</span><span class="sxs-lookup"><span data-stu-id="5b445-197">Get hello network interface card with [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface), then set hello *LoadBalancerBackendAddressPools* property of hello virtual NIC too*$null*.</span></span> <span data-ttu-id="5b445-198">最後，更新虛擬 nic。 hello:</span><span class="sxs-lookup"><span data-stu-id="5b445-198">Finally, update hello virtual NIC.:</span></span>

```powershell
$nic = Get-AzureRmNetworkInterface `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Name myNic2
$nic.Ipconfigurations[0].LoadBalancerBackendAddressPools=$null
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

<span data-ttu-id="5b445-199">toosee hello 負載平衡器會將流量分散到 hello 剩餘的兩個 Vm 執行您的應用程式您可以強制重新整理您的 web 瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="5b445-199">toosee hello load balancer distribute traffic across hello remaining two VMs running your app you can force-refresh your web browser.</span></span> <span data-ttu-id="5b445-200">您現在可以在 hello VM，如安裝作業系統更新，或執行 VM 重新啟動電腦上執行維護。</span><span class="sxs-lookup"><span data-stu-id="5b445-200">You can now perform maintenance on hello VM, such as installing OS updates or performing a VM reboot.</span></span>

### <a name="add-a-vm-toohello-load-balancer"></a><span data-ttu-id="5b445-201">新增 VM toohello 負載平衡器</span><span class="sxs-lookup"><span data-stu-id="5b445-201">Add a VM toohello load balancer</span></span>
<span data-ttu-id="5b445-202">之後，請執行 VM 維護，或如果您需要 tooexpand 產能，設定 hello*了 LoadBalancerBackendAddressPools* hello 虛擬 NIC toohello 屬性*BackendAddressPool*從[Get AzureRMLoadBalancer](/powershell/module/azurerm.network/get-azurermloadbalancer):</span><span class="sxs-lookup"><span data-stu-id="5b445-202">After performing VM maintenance, or if you need tooexpand capacity, set hello *LoadBalancerBackendAddressPools* property of hello virtual NIC toohello *BackendAddressPool* from [Get-AzureRMLoadBalancer](/powershell/module/azurerm.network/get-azurermloadbalancer):</span></span>

<span data-ttu-id="5b445-203">收到 hello 負載平衡器：</span><span class="sxs-lookup"><span data-stu-id="5b445-203">Get hello load balancer:</span></span>

```powershell
$lb = Get-AzureRMLoadBalancer `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Name myLoadBalancer 
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$lb.BackendAddressPools[0]
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

## <a name="next-steps"></a><span data-ttu-id="5b445-204">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5b445-204">Next steps</span></span>

<span data-ttu-id="5b445-205">在本教學課程中，您可以建立負載平衡器，並附加 Vm tooit。</span><span class="sxs-lookup"><span data-stu-id="5b445-205">In this tutorial, you created a load balancer and attached VMs tooit.</span></span> <span data-ttu-id="5b445-206">您已了解如何︰</span><span class="sxs-lookup"><span data-stu-id="5b445-206">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="5b445-207">建立 Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="5b445-207">Create an Azure load balancer</span></span>
> * <span data-ttu-id="5b445-208">建立負載平衡器健全狀況探查</span><span class="sxs-lookup"><span data-stu-id="5b445-208">Create a load balancer health probe</span></span>
> * <span data-ttu-id="5b445-209">建立負載平衡器流量規則</span><span class="sxs-lookup"><span data-stu-id="5b445-209">Create load balancer traffic rules</span></span>
> * <span data-ttu-id="5b445-210">使用 hello 自訂指令碼擴充 toocreate 基本的 IIS 站台</span><span class="sxs-lookup"><span data-stu-id="5b445-210">Use hello Custom Script Extension toocreate a basic IIS site</span></span>
> * <span data-ttu-id="5b445-211">建立虛擬機器，並附加 tooa 負載平衡器</span><span class="sxs-lookup"><span data-stu-id="5b445-211">Create virtual machines and attach tooa load balancer</span></span>
> * <span data-ttu-id="5b445-212">檢視作用中的負載平衡器</span><span class="sxs-lookup"><span data-stu-id="5b445-212">View a load balancer in action</span></span>
> * <span data-ttu-id="5b445-213">新增和移除虛擬機器的負載平衡器</span><span class="sxs-lookup"><span data-stu-id="5b445-213">Add and remove VMs from a load balancer</span></span>

<span data-ttu-id="5b445-214">如何前進 toohello 下一個教學課程 toolearn toomanage VM 網路。</span><span class="sxs-lookup"><span data-stu-id="5b445-214">Advance toohello next tutorial toolearn how toomanage VM networking.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="5b445-215">管理 VM 和虛擬網路</span><span class="sxs-lookup"><span data-stu-id="5b445-215">Manage VMs and virtual networks</span></span>](./tutorial-virtual-network.md)
