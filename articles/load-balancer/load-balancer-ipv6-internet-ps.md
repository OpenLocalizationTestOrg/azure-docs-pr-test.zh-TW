---
title: "IPv6-PowerShell 的 Azure 網際網路對向 aaaCreate 負載平衡器 |Microsoft 文件"
description: "了解如何 toocreate 面對網際網路的負載平衡器使用 IPv6 使用資源管理員的 PowerShell"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
keywords: "ipv6, azure load balancer, 雙重堆疊, 公用 ip, 原生 ipv6, 行動, iot"
ms.assetid: d4c649e3-84ad-4343-8b6a-0e89f0b9e518
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 6ebb108399b070e06dddc33b7a774481eb44d717
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-with-ipv6-using-powershell-for-resource-manager"></a><span data-ttu-id="efc7a-104">開始使用 PowerShell 在 Resource Manager 中建立配置有 IPv6 的網際網路面向負載平衡器</span><span class="sxs-lookup"><span data-stu-id="efc7a-104">Get started creating an Internet facing load balancer with IPv6 using PowerShell for Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="efc7a-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="efc7a-105">PowerShell</span></span>](load-balancer-ipv6-internet-ps.md)
> * [<span data-ttu-id="efc7a-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="efc7a-106">Azure CLI</span></span>](load-balancer-ipv6-internet-cli.md)
> * [<span data-ttu-id="efc7a-107">範本</span><span class="sxs-lookup"><span data-stu-id="efc7a-107">Template</span></span>](load-balancer-ipv6-internet-template.md)

<span data-ttu-id="efc7a-108">Azure 負載平衡器是第 4 層 (TCP、UDP) 負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="efc7a-108">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer.</span></span> <span data-ttu-id="efc7a-109">hello 負載平衡器連入流量的各項雲端服務中的狀況良好的服務執行個體或虛擬機器中負載平衡器集可提供高可用性。</span><span class="sxs-lookup"><span data-stu-id="efc7a-109">hello load balancer provides high availability by distributing incoming traffic among healthy service instances in cloud services or virtual machines in a load balancer set.</span></span> <span data-ttu-id="efc7a-110">Azure Load Balancer 也會在多個連接埠、多個 IP 位址或兩者上顯示這些服務。</span><span class="sxs-lookup"><span data-stu-id="efc7a-110">Azure Load Balancer can also present those services on multiple ports, multiple IP addresses, or both.</span></span>

## <a name="example-deployment-scenario"></a><span data-ttu-id="efc7a-111">範例部署案例</span><span class="sxs-lookup"><span data-stu-id="efc7a-111">Example deployment scenario</span></span>

<span data-ttu-id="efc7a-112">hello 下列圖表說明 hello 負載平衡解決方案部署在本文中。</span><span class="sxs-lookup"><span data-stu-id="efc7a-112">hello following diagram illustrates hello load balancing solution being deployed in this article.</span></span>

![負載平衡器案例](./media/load-balancer-ipv6-internet-ps/lb-ipv6-scenario.png)

<span data-ttu-id="efc7a-114">在此案例中，您將建立下列 Azure 資源的 hello:</span><span class="sxs-lookup"><span data-stu-id="efc7a-114">In this scenario you will create hello following Azure resources:</span></span>

* <span data-ttu-id="efc7a-115">配置有 IPv4 和 IPv6 公用 IP 位址的網際網路面向負載平衡器</span><span class="sxs-lookup"><span data-stu-id="efc7a-115">an Internet-facing Load Balancer with an IPv4 and an IPv6 Public IP address</span></span>
* <span data-ttu-id="efc7a-116">兩個負載平衡規則 toomap hello 公用 Vip toohello 私用端點</span><span class="sxs-lookup"><span data-stu-id="efc7a-116">two load balancing rules toomap hello public VIPs toohello private endpoints</span></span>
* <span data-ttu-id="efc7a-117">可用性設定組的 toothat 包含 hello 兩個 Vm</span><span class="sxs-lookup"><span data-stu-id="efc7a-117">an Availability Set toothat contains hello two VMs</span></span>
* <span data-ttu-id="efc7a-118">兩部虛擬機器 (VM)</span><span class="sxs-lookup"><span data-stu-id="efc7a-118">two virtual machines (VMs)</span></span>
* <span data-ttu-id="efc7a-119">虛擬網路介面，用於每個已指派 IPv4 和 IPv6 位址的 VM</span><span class="sxs-lookup"><span data-stu-id="efc7a-119">a virtual network interface for each VM with both IPv4 and IPv6 addresses assigned</span></span>

## <a name="deploying-hello-solution-using-hello-azure-powershell"></a><span data-ttu-id="efc7a-120">使用 Azure PowerShell hello hello 方案部署</span><span class="sxs-lookup"><span data-stu-id="efc7a-120">Deploying hello solution using hello Azure PowerShell</span></span>

<span data-ttu-id="efc7a-121">下列步驟的 hello 顯示 toocreate 網際網路向負載平衡器使用 PowerShell 的 Azure 資源管理員的方式。</span><span class="sxs-lookup"><span data-stu-id="efc7a-121">hello following steps show how toocreate an Internet facing load balancer using Azure Resource Manager with PowerShell.</span></span> <span data-ttu-id="efc7a-122">使用 Azure 資源管理員中，建立每個資源，並個別設定，然後放在一起 toocreate 資源。</span><span class="sxs-lookup"><span data-stu-id="efc7a-122">With Azure Resource Manager, each resource is created and configured individually, then put together toocreate a resource.</span></span>

<span data-ttu-id="efc7a-123">toodeploy 負載平衡器，建立並設定 hello 下列物件：</span><span class="sxs-lookup"><span data-stu-id="efc7a-123">toodeploy a load balancer, you create and configure hello following objects:</span></span>

* <span data-ttu-id="efc7a-124">前端 IP 組態 - 包含傳入網路流量的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="efc7a-124">Front-end IP configuration - contains public IP addresses for incoming network traffic.</span></span>
* <span data-ttu-id="efc7a-125">後端位址集區-包含 hello 虛擬機器 tooreceive 從 hello 負載平衡器的網路流量的網路介面 (Nic)。</span><span class="sxs-lookup"><span data-stu-id="efc7a-125">Back-end address pool - contains network interfaces (NICs) for hello virtual machines tooreceive network traffic from hello load balancer.</span></span>
* <span data-ttu-id="efc7a-126">負載平衡規則-包含對應 hello 負載平衡器 tooport hello 後端位址集區中的公用連接埠的規則。</span><span class="sxs-lookup"><span data-stu-id="efc7a-126">Load balancing rules - contains rules mapping a public port on hello load balancer tooport in hello back-end address pool.</span></span>
* <span data-ttu-id="efc7a-127">輸入 NAT 規則-包含 hello 負載平衡器 tooa 通訊埠上的特定虛擬機器 hello 後端位址集區中的公用通訊埠對應規則。</span><span class="sxs-lookup"><span data-stu-id="efc7a-127">Inbound NAT rules - contains rules mapping a public port on hello load balancer tooa port for a specific virtual machine in hello back-end address pool.</span></span>
* <span data-ttu-id="efc7a-128">探查-包含 hello 後端位址集區中的虛擬機器執行個體的健全狀況探查使用 toocheck 可用性。</span><span class="sxs-lookup"><span data-stu-id="efc7a-128">Probes - contains health probes used toocheck availability of virtual machines instances in hello back-end address pool.</span></span>

<span data-ttu-id="efc7a-129">如需詳細資料，請參閱 [Azure Resource Manager 的負載平衡器支援](load-balancer-arm.md)。</span><span class="sxs-lookup"><span data-stu-id="efc7a-129">For more information, see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-powershell-toouse-resource-manager"></a><span data-ttu-id="efc7a-130">設定 PowerShell toouse 資源管理員</span><span class="sxs-lookup"><span data-stu-id="efc7a-130">Set up PowerShell toouse Resource Manager</span></span>

<span data-ttu-id="efc7a-131">請確定您的 PowerShell hello Azure 資源管理員模組的 hello 最新實際執行版本。</span><span class="sxs-lookup"><span data-stu-id="efc7a-131">Make sure you have hello latest production version of hello Azure Resource Manager module for PowerShell.</span></span>

1. <span data-ttu-id="efc7a-132">登入 Azure</span><span class="sxs-lookup"><span data-stu-id="efc7a-132">Sign into Azure</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

    <span data-ttu-id="efc7a-133">出現提示時，請輸入您的認證。</span><span class="sxs-lookup"><span data-stu-id="efc7a-133">Enter your credentials when prompted.</span></span>

2. <span data-ttu-id="efc7a-134">檢查 hello 訂閱 hello 帳戶</span><span class="sxs-lookup"><span data-stu-id="efc7a-134">Check hello subscriptions for hello account</span></span>

    ```powershell
    Get-AzureRmSubscription
    ```

3. <span data-ttu-id="efc7a-135">選擇 Azure 訂用帳戶 toouse。</span><span class="sxs-lookup"><span data-stu-id="efc7a-135">Choose which of your Azure subscriptions toouse.</span></span>

    ```powershell
    Select-AzureRmSubscription -SubscriptionId 'GUID of subscription'
    ```

4. <span data-ttu-id="efc7a-136">建立資源群組 (如果是使用現有的資源群組，請略過此步驟)</span><span class="sxs-lookup"><span data-stu-id="efc7a-136">Create a resource group (skip this step if using an existing resource group)</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name NRP-RG -location "West US"
    ```

## <a name="create-a-virtual-network-and-a-public-ip-address-for-hello-front-end-ip-pool"></a><span data-ttu-id="efc7a-137">建立虛擬網路和 hello 前端 IP 集區的公用 IP 位址</span><span class="sxs-lookup"><span data-stu-id="efc7a-137">Create a virtual network and a public IP address for hello front-end IP pool</span></span>

1. <span data-ttu-id="efc7a-138">建立具有子網路的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="efc7a-138">Create a virtual network with a subnet.</span></span>

    ```powershell
    $backendSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -AddressPrefix 10.0.2.0/24
    $vnet = New-AzureRmvirtualNetwork -Name VNet -ResourceGroupName NRP-RG -Location 'West US' -AddressPrefix 10.0.0.0/16 -Subnet $backendSubnet
    ```

2. <span data-ttu-id="efc7a-139">建立 Azure 公用 IP 位址 (PIP) hello 前端 IP 位址集區的資源。</span><span class="sxs-lookup"><span data-stu-id="efc7a-139">Create Azure Public IP address (PIP) resources for hello front-end IP address pool.</span></span>

    ```powershell
    $publicIPv4 = New-AzureRmPublicIpAddress -Name 'pub-ipv4' -ResourceGroupName NRP-RG -Location 'West US' -AllocationMethod Static -IpAddressVersion IPv4 -DomainNameLabel lbnrpipv4
    $publicIPv6 = New-AzureRmPublicIpAddress -Name 'pub-ipv6' -ResourceGroupName NRP-RG -Location 'West US' -AllocationMethod Dynamic -IpAddressVersion IPv6 -DomainNameLabel lbnrpipv6
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="efc7a-140">hello 負載平衡器會使用做為前置詞的 hello 公用 IP 的 hello 網域標籤，其 fqdn。</span><span class="sxs-lookup"><span data-stu-id="efc7a-140">hello load balancer uses hello domain label of hello public IP as prefix for its FQDN.</span></span> <span data-ttu-id="efc7a-141">在此範例中，是 hello Fqdn *lbnrpipv4.westus.cloudapp.azure.com*和*lbnrpipv6.westus.cloudapp.azure.com*。</span><span class="sxs-lookup"><span data-stu-id="efc7a-141">In this example, hello FQDNs are *lbnrpipv4.westus.cloudapp.azure.com* and *lbnrpipv6.westus.cloudapp.azure.com*.</span></span>

## <a name="create-a-front-end-ip-configurations-and-a-back-end-address-pool"></a><span data-ttu-id="efc7a-142">建立前端 IP 組態和後端位址集區</span><span class="sxs-lookup"><span data-stu-id="efc7a-142">Create a Front-End IP configurations and a Back-End Address Pool</span></span>

1. <span data-ttu-id="efc7a-143">建立使用您所建立的 hello 公用 IP 位址的前端位址設定。</span><span class="sxs-lookup"><span data-stu-id="efc7a-143">Create front-end address configuration that uses hello Public IP addresses you created.</span></span>

    ```powershell
    $FEIPConfigv4 = New-AzureRmLoadBalancerFrontendIpConfig -Name "LB-Frontendv4" -PublicIpAddress $publicIPv4
    $FEIPConfigv6 = New-AzureRmLoadBalancerFrontendIpConfig -Name "LB-Frontendv6" -PublicIpAddress $publicIPv6
    ```

2. <span data-ttu-id="efc7a-144">建立後端位址集區。</span><span class="sxs-lookup"><span data-stu-id="efc7a-144">Create back-end address pools.</span></span>

    ```powershell
    $backendpoolipv4 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "BackendPoolIPv4"
    $backendpoolipv6 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "BackendPoolIPv6"
    ```

## <a name="create-lb-rules-nat-rules-a-probe-and-a-load-balancer"></a><span data-ttu-id="efc7a-145">建立 LB 規則、NAT 規則、探查及負載平衡器</span><span class="sxs-lookup"><span data-stu-id="efc7a-145">Create LB rules, NAT rules, a probe, and a load balancer</span></span>

<span data-ttu-id="efc7a-146">這個範例會建立下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="efc7a-146">This example creates hello following items:</span></span>

* <span data-ttu-id="efc7a-147">NAT 規則 tootranslate 連接埠 443 tooport 4443 上的所有傳入流量</span><span class="sxs-lookup"><span data-stu-id="efc7a-147">a NAT rule tootranslate all incoming traffic on port 443 tooport 4443</span></span>
* <span data-ttu-id="efc7a-148">負載平衡器規則 toobalance hello 連接埠 80 tooport 80 上的所有連入流量 hello 後端集區中的位址。</span><span class="sxs-lookup"><span data-stu-id="efc7a-148">a load balancer rule toobalance all incoming traffic on port 80 tooport 80 on hello addresses in hello back-end pool.</span></span>
* <span data-ttu-id="efc7a-149">負載平衡器規則 tooallow RDP 連線 toohello 上連接埠 3389 的 Vm。</span><span class="sxs-lookup"><span data-stu-id="efc7a-149">a load balancer rule tooallow RDP connection toohello VMs on port 3389.</span></span>
* <span data-ttu-id="efc7a-150">探查規則 toocheck hello 健全狀況狀態上名為的頁面*HealthProbe.aspx*或連接埠 8080 上的服務</span><span class="sxs-lookup"><span data-stu-id="efc7a-150">a probe rule toocheck hello health status on a page named *HealthProbe.aspx* or a service on port 8080</span></span>
* <span data-ttu-id="efc7a-151">會使用上述所有物件的負載平衡器</span><span class="sxs-lookup"><span data-stu-id="efc7a-151">a load balancer that uses all these objects</span></span>

1. <span data-ttu-id="efc7a-152">建立 hello NAT 規則。</span><span class="sxs-lookup"><span data-stu-id="efc7a-152">Create hello NAT rules.</span></span>

    ```powershell
    $inboundNATRule1v4 = New-AzureRmLoadBalancerInboundNatRuleConfig -Name "NicNatRulev4" -FrontendIpConfiguration $FEIPConfigv4 -Protocol TCP -FrontendPort 443 -BackendPort 4443
    $inboundNATRule1v6 = New-AzureRmLoadBalancerInboundNatRuleConfig -Name "NicNatRulev6" -FrontendIpConfiguration $FEIPConfigv6 -Protocol TCP -FrontendPort 443 -BackendPort 4443
    ```

2. <span data-ttu-id="efc7a-153">建立健全狀況探查。</span><span class="sxs-lookup"><span data-stu-id="efc7a-153">Create a health probe.</span></span> <span data-ttu-id="efc7a-154">有兩種方式 tooconfigure 探查：</span><span class="sxs-lookup"><span data-stu-id="efc7a-154">There are two ways tooconfigure a probe:</span></span>

    <span data-ttu-id="efc7a-155">HTTP 探查</span><span class="sxs-lookup"><span data-stu-id="efc7a-155">HTTP probe</span></span>

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name 'HealthProbe-v4v6' -RequestPath 'HealthProbe.aspx' -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2
    ```

    <span data-ttu-id="efc7a-156">或 TCP 探查</span><span class="sxs-lookup"><span data-stu-id="efc7a-156">or TCP probe</span></span>

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name 'HealthProbe-v4v6' -Protocol Tcp -Port 8080 -IntervalInSeconds 15 -ProbeCount 2
    $RDPprobe = New-AzureRmLoadBalancerProbeConfig -Name 'RDPprobe' -Protocol Tcp -Port 3389 -IntervalInSeconds 15 -ProbeCount 2
    ```

    <span data-ttu-id="efc7a-157">此範例中，我們會 toouse hello TCP 探查。</span><span class="sxs-lookup"><span data-stu-id="efc7a-157">For this example, we are going toouse hello TCP probes.</span></span>

3. <span data-ttu-id="efc7a-158">建立負載平衡器規則。</span><span class="sxs-lookup"><span data-stu-id="efc7a-158">Create a load balancer rule.</span></span>

    ```powershell
    $lbrule1v4 = New-AzureRmLoadBalancerRuleConfig -Name "HTTPv4" -FrontendIpConfiguration $FEIPConfigv4 -BackendAddressPool $backendpoolipv4 -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 8080
    $lbrule1v6 = New-AzureRmLoadBalancerRuleConfig -Name "HTTPv6" -FrontendIpConfiguration $FEIPConfigv6 -BackendAddressPool $backendpoolipv6 -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 8080
    $RDPrule = New-AzureRmLoadBalancerRuleConfig -Name "RDPrule" -FrontendIpConfiguration $FEIPConfigv4 -BackendAddressPool $backendpoolipv4 -Probe $RDPprobe -Protocol Tcp -FrontendPort 3389 -BackendPort 3389
    ```

4. <span data-ttu-id="efc7a-159">建立 hello 負載平衡器使用 hello 先前建立的物件。</span><span class="sxs-lookup"><span data-stu-id="efc7a-159">Create hello load balancer using hello previously created objects.</span></span>

    ```powershell
    $NRPLB = New-AzureRmLoadBalancer -ResourceGroupName NRP-RG -Name 'myNrpIPv6LB' -Location 'West US' -FrontendIpConfiguration $FEIPConfigv4,$FEIPConfigv6 -InboundNatRule $inboundNATRule1v6,$inboundNATRule1v4 -BackendAddressPool $backendpoolipv4,$backendpoolipv6 -Probe $healthProbe,$RDPprobe -LoadBalancingRule $lbrule1v4,$lbrule1v6,$RDPrule
    ```

## <a name="create-nics-for-hello-back-end-vms"></a><span data-ttu-id="efc7a-160">建立 hello 後端 Vm Nic</span><span class="sxs-lookup"><span data-stu-id="efc7a-160">Create NICs for hello back-end VMs</span></span>

1. <span data-ttu-id="efc7a-161">取得 hello 虛擬網路與虛擬網路子網路，hello Nic 需要 toobe 建立的位置。</span><span class="sxs-lookup"><span data-stu-id="efc7a-161">Get hello Virtual Network and Virtual Network Subnet, where hello NICs need toobe created.</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -Name VNet -ResourceGroupName NRP-RG
    $backendSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -VirtualNetwork $vnet
    ```

2. <span data-ttu-id="efc7a-162">建立 hello Vm 的 IP 組態和 Nic。</span><span class="sxs-lookup"><span data-stu-id="efc7a-162">Create IP configurations and NICs for hello VMs.</span></span>

    ```powershell
    $nic1IPv4 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv4IPConfig" -PrivateIpAddressVersion "IPv4" -Subnet $backendSubnet -LoadBalancerBackendAddressPool $backendpoolipv4 -LoadBalancerInboundNatRule $inboundNATRule1v4
    $nic1IPv6 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv6IPConfig" -PrivateIpAddressVersion "IPv6" -LoadBalancerBackendAddressPool $backendpoolipv6 -LoadBalancerInboundNatRule $inboundNATRule1v6
    $nic1 = New-AzureRmNetworkInterface -Name 'myNrpIPv6Nic0' -IpConfiguration $nic1IPv4,$nic1IPv6 -ResourceGroupName NRP-RG -Location 'West US'

    $nic2IPv4 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv4IPConfig" -PrivateIpAddressVersion "IPv4" -Subnet $backendSubnet -LoadBalancerBackendAddressPool $backendpoolipv4
    $nic2IPv6 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv6IPConfig" -PrivateIpAddressVersion "IPv6" -LoadBalancerBackendAddressPool $backendpoolipv6
    $nic2 = New-AzureRmNetworkInterface -Name 'myNrpIPv6Nic1' -IpConfiguration $nic2IPv4,$nic2IPv6 -ResourceGroupName NRP-RG -Location 'West US'
    ```

## <a name="create-virtual-machines-and-assign-hello-newly-created-nics"></a><span data-ttu-id="efc7a-163">建立虛擬機器，並指派新建立的 Nic 的 hello</span><span class="sxs-lookup"><span data-stu-id="efc7a-163">Create virtual machines and assign hello newly created NICs</span></span>

<span data-ttu-id="efc7a-164">如需有關建立 VM 的詳細資訊，請參閱 [使用 Resource Manager 和 Azure PowerShell 建立及預先設定 Windows 虛擬機器](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="efc7a-164">For more information about creating a VM, see [Create and preconfigure a Windows Virtual Machine with Resource Manager and Azure PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)</span></span>

1. <span data-ttu-id="efc7a-165">建立可用性設定組和儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="efc7a-165">Create an Availability Set and Storage account</span></span>

    ```powershell
    New-AzureRmAvailabilitySet -Name 'myNrpIPv6AvSet' -ResourceGroupName NRP-RG -location 'West US'
    $availabilitySet = Get-AzureRmAvailabilitySet -Name 'myNrpIPv6AvSet' -ResourceGroupName NRP-RG
    New-AzureRmStorageAccount -ResourceGroupName NRP-RG -Name 'mynrpipv6stacct' -Location 'West US' -SkuName "Standard_LRS"
    $CreatedStorageAccount = Get-AzureRmStorageAccount -ResourceGroupName NRP-RG -Name 'mynrpipv6stacct'
    ```

2. <span data-ttu-id="efc7a-166">建立每個 VM，並指派 hello 先前建立 Nic</span><span class="sxs-lookup"><span data-stu-id="efc7a-166">Create each VM and assign hello previous created NICs</span></span>

    ```powershell
    $mySecureCredentials= Get-Credential -Message "Type hello username and password of hello local administrator account."

    $vm1 = New-AzureRmVMConfig -VMName 'myNrpIPv6VM0' -VMSize 'Standard_G1' -AvailabilitySetId $availabilitySet.Id
    $vm1 = Set-AzureRmVMOperatingSystem -VM $vm1 -Windows -ComputerName 'myNrpIPv6VM0' -Credential $mySecureCredentials -ProvisionVMAgent -EnableAutoUpdate
    $vm1 = Set-AzureRmVMSourceImage -VM $vm1 -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
    $vm1 = Add-AzureRmVMNetworkInterface -VM $vm1 -Id $nic1.Id -Primary
    $osDisk1Uri = $CreatedStorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/myNrpIPv6VM0osdisk.vhd"
    $vm1 = Set-AzureRmVMOSDisk -VM $vm1 -Name 'myNrpIPv6VM0osdisk' -VhdUri $osDisk1Uri -CreateOption FromImage
    New-AzureRmVM -ResourceGroupName NRP-RG -Location 'West US' -VM $vm1

    $vm2 = New-AzureRmVMConfig -VMName 'myNrpIPv6VM1' -VMSize 'Standard_G1' -AvailabilitySetId $availabilitySet.Id
    $vm2 = Set-AzureRmVMOperatingSystem -VM $vm2 -Windows -ComputerName 'myNrpIPv6VM1' -Credential $mySecureCredentials -ProvisionVMAgent -EnableAutoUpdate
    $vm2 = Set-AzureRmVMSourceImage -VM $vm2 -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
    $vm2 = Add-AzureRmVMNetworkInterface -VM $vm2 -Id $nic2.Id -Primary
    $osDisk2Uri = $CreatedStorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/myNrpIPv6VM1osdisk.vhd"
    $vm2 = Set-AzureRmVMOSDisk -VM $vm2 -Name 'myNrpIPv6VM1osdisk' -VhdUri $osDisk2Uri -CreateOption FromImage
    New-AzureRmVM -ResourceGroupName NRP-RG -Location 'West US' -VM $vm2
    ```

## <a name="next-steps"></a><span data-ttu-id="efc7a-167">後續步驟</span><span class="sxs-lookup"><span data-stu-id="efc7a-167">Next steps</span></span>

[<span data-ttu-id="efc7a-168">開始設定內部負載平衡器</span><span class="sxs-lookup"><span data-stu-id="efc7a-168">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="efc7a-169">設定負載平衡器分配模式</span><span class="sxs-lookup"><span data-stu-id="efc7a-169">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="efc7a-170">設定負載平衡器的閒置 TCP 逾時設定</span><span class="sxs-lookup"><span data-stu-id="efc7a-170">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
