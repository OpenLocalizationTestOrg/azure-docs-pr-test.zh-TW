---
title: "建立配置有 IPv6 的 Azure 網際網路對向負載平衡器 - PowerShell | Microsoft Docs"
description: "了解如何使用 PowerShell 在 Resource Manager 中建立配置有 IPv6 的網際網路面向負載平衡器"
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
ms.openlocfilehash: 9d3cd37d3f2912301904b0a35f6fbc978d173079
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-with-ipv6-using-powershell-for-resource-manager"></a><span data-ttu-id="aa034-104">開始使用 PowerShell 在 Resource Manager 中建立配置有 IPv6 的網際網路面向負載平衡器</span><span class="sxs-lookup"><span data-stu-id="aa034-104">Get started creating an Internet facing load balancer with IPv6 using PowerShell for Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="aa034-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="aa034-105">PowerShell</span></span>](load-balancer-ipv6-internet-ps.md)
> * [<span data-ttu-id="aa034-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="aa034-106">Azure CLI</span></span>](load-balancer-ipv6-internet-cli.md)
> * [<span data-ttu-id="aa034-107">範本</span><span class="sxs-lookup"><span data-stu-id="aa034-107">Template</span></span>](load-balancer-ipv6-internet-template.md)

<span data-ttu-id="aa034-108">Azure 負載平衡器是第 4 層 (TCP、UDP) 負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="aa034-108">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer.</span></span> <span data-ttu-id="aa034-109">此負載平衡器可藉由在負載平衡器集合中，將連入流量分散於雲端服務或虛擬機器中狀況良好的服務執行個體之間，來提供高可用性。</span><span class="sxs-lookup"><span data-stu-id="aa034-109">The load balancer provides high availability by distributing incoming traffic among healthy service instances in cloud services or virtual machines in a load balancer set.</span></span> <span data-ttu-id="aa034-110">Azure Load Balancer 也會在多個連接埠、多個 IP 位址或兩者上顯示這些服務。</span><span class="sxs-lookup"><span data-stu-id="aa034-110">Azure Load Balancer can also present those services on multiple ports, multiple IP addresses, or both.</span></span>

## <a name="example-deployment-scenario"></a><span data-ttu-id="aa034-111">範例部署案例</span><span class="sxs-lookup"><span data-stu-id="aa034-111">Example deployment scenario</span></span>

<span data-ttu-id="aa034-112">下圖說明本文中部署的負載平衡解決方案。</span><span class="sxs-lookup"><span data-stu-id="aa034-112">The following diagram illustrates the load balancing solution being deployed in this article.</span></span>

![負載平衡器案例](./media/load-balancer-ipv6-internet-ps/lb-ipv6-scenario.png)

<span data-ttu-id="aa034-114">在此案例中，您將建立下列 Azure 資源：</span><span class="sxs-lookup"><span data-stu-id="aa034-114">In this scenario you will create the following Azure resources:</span></span>

* <span data-ttu-id="aa034-115">配置有 IPv4 和 IPv6 公用 IP 位址的網際網路面向負載平衡器</span><span class="sxs-lookup"><span data-stu-id="aa034-115">an Internet-facing Load Balancer with an IPv4 and an IPv6 Public IP address</span></span>
* <span data-ttu-id="aa034-116">兩個負載平衡規則，用以對應公用 VIP 至私人端點</span><span class="sxs-lookup"><span data-stu-id="aa034-116">two load balancing rules to map the public VIPs to the private endpoints</span></span>
* <span data-ttu-id="aa034-117">包含兩個 VM 的可用性設定組</span><span class="sxs-lookup"><span data-stu-id="aa034-117">an Availability Set to that contains the two VMs</span></span>
* <span data-ttu-id="aa034-118">兩部虛擬機器 (VM)</span><span class="sxs-lookup"><span data-stu-id="aa034-118">two virtual machines (VMs)</span></span>
* <span data-ttu-id="aa034-119">虛擬網路介面，用於每個已指派 IPv4 和 IPv6 位址的 VM</span><span class="sxs-lookup"><span data-stu-id="aa034-119">a virtual network interface for each VM with both IPv4 and IPv6 addresses assigned</span></span>

## <a name="deploying-the-solution-using-the-azure-powershell"></a><span data-ttu-id="aa034-120">使用 Azure PowerShell 部署解決方案</span><span class="sxs-lookup"><span data-stu-id="aa034-120">Deploying the solution using the Azure PowerShell</span></span>

<span data-ttu-id="aa034-121">下列步驟說明如何搭配 PowerShell 使用 Azure Resource Manager，來建立網際網路對向負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="aa034-121">The following steps show how to create an Internet facing load balancer using Azure Resource Manager with PowerShell.</span></span> <span data-ttu-id="aa034-122">使用 Azure Resource Manager 時，會個別建立並設定每項資源，然後放在一起來建立一項資源。</span><span class="sxs-lookup"><span data-stu-id="aa034-122">With Azure Resource Manager, each resource is created and configured individually, then put together to create a resource.</span></span>

<span data-ttu-id="aa034-123">若要部署負載平衡器，請建立並設定下列物件：</span><span class="sxs-lookup"><span data-stu-id="aa034-123">To deploy a load balancer, you create and configure the following objects:</span></span>

* <span data-ttu-id="aa034-124">前端 IP 組態 - 包含傳入網路流量的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="aa034-124">Front-end IP configuration - contains public IP addresses for incoming network traffic.</span></span>
* <span data-ttu-id="aa034-125">後端位址集區 - 包含虛擬機器的網路介面 (NIC)，可從負載平衡器接收網路流量。</span><span class="sxs-lookup"><span data-stu-id="aa034-125">Back-end address pool - contains network interfaces (NICs) for the virtual machines to receive network traffic from the load balancer.</span></span>
* <span data-ttu-id="aa034-126">負載平衡規則 - 包含將負載平衡器上的公用連接埠對應至後端位址集區中連接埠的規則。</span><span class="sxs-lookup"><span data-stu-id="aa034-126">Load balancing rules - contains rules mapping a public port on the load balancer to port in the back-end address pool.</span></span>
* <span data-ttu-id="aa034-127">輸入 NAT 規則 - 包含將負載平衡器上的公用連接埠對應至後端位址集區中特定虛擬機器之連接埠的規則。</span><span class="sxs-lookup"><span data-stu-id="aa034-127">Inbound NAT rules - contains rules mapping a public port on the load balancer to a port for a specific virtual machine in the back-end address pool.</span></span>
* <span data-ttu-id="aa034-128">探查 - 包含用來檢查後端位址集區中虛擬機器執行個體可用性的健全狀態探查。</span><span class="sxs-lookup"><span data-stu-id="aa034-128">Probes - contains health probes used to check availability of virtual machines instances in the back-end address pool.</span></span>

<span data-ttu-id="aa034-129">如需詳細資料，請參閱 [Azure Resource Manager 的負載平衡器支援](load-balancer-arm.md)。</span><span class="sxs-lookup"><span data-stu-id="aa034-129">For more information, see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-powershell-to-use-resource-manager"></a><span data-ttu-id="aa034-130">設定 PowerShell 以使用 Resource Manager</span><span class="sxs-lookup"><span data-stu-id="aa034-130">Set up PowerShell to use Resource Manager</span></span>

<span data-ttu-id="aa034-131">請確定您擁有適用於 PowerShell 的 Azure Resource Manager 模組最新生產版本。</span><span class="sxs-lookup"><span data-stu-id="aa034-131">Make sure you have the latest production version of the Azure Resource Manager module for PowerShell.</span></span>

1. <span data-ttu-id="aa034-132">登入 Azure</span><span class="sxs-lookup"><span data-stu-id="aa034-132">Sign into Azure</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

    <span data-ttu-id="aa034-133">出現提示時，請輸入您的認證。</span><span class="sxs-lookup"><span data-stu-id="aa034-133">Enter your credentials when prompted.</span></span>

2. <span data-ttu-id="aa034-134">檢查帳戶的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="aa034-134">Check the subscriptions for the account</span></span>

    ```powershell
    Get-AzureRmSubscription
    ```

3. <span data-ttu-id="aa034-135">選擇要使用哪一個 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="aa034-135">Choose which of your Azure subscriptions to use.</span></span>

    ```powershell
    Select-AzureRmSubscription -SubscriptionId 'GUID of subscription'
    ```

4. <span data-ttu-id="aa034-136">建立資源群組 (如果是使用現有的資源群組，請略過此步驟)</span><span class="sxs-lookup"><span data-stu-id="aa034-136">Create a resource group (skip this step if using an existing resource group)</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name NRP-RG -location "West US"
    ```

## <a name="create-a-virtual-network-and-a-public-ip-address-for-the-front-end-ip-pool"></a><span data-ttu-id="aa034-137">建立前端 IP 集區的虛擬網路和公用 IP 位址</span><span class="sxs-lookup"><span data-stu-id="aa034-137">Create a virtual network and a public IP address for the front-end IP pool</span></span>

1. <span data-ttu-id="aa034-138">建立具有子網路的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="aa034-138">Create a virtual network with a subnet.</span></span>

    ```powershell
    $backendSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -AddressPrefix 10.0.2.0/24
    $vnet = New-AzureRmvirtualNetwork -Name VNet -ResourceGroupName NRP-RG -Location 'West US' -AddressPrefix 10.0.0.0/16 -Subnet $backendSubnet
    ```

2. <span data-ttu-id="aa034-139">建立前端 IP 位址集區的 Azure 公用 IP 位址 (PIP) 資源。</span><span class="sxs-lookup"><span data-stu-id="aa034-139">Create Azure Public IP address (PIP) resources for the front-end IP address pool.</span></span>

    ```powershell
    $publicIPv4 = New-AzureRmPublicIpAddress -Name 'pub-ipv4' -ResourceGroupName NRP-RG -Location 'West US' -AllocationMethod Static -IpAddressVersion IPv4 -DomainNameLabel lbnrpipv4
    $publicIPv6 = New-AzureRmPublicIpAddress -Name 'pub-ipv6' -ResourceGroupName NRP-RG -Location 'West US' -AllocationMethod Dynamic -IpAddressVersion IPv6 -DomainNameLabel lbnrpipv6
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="aa034-140">負載平衡器會使用公用 IP 的網域標籤做為其 FQDN 的前置詞。</span><span class="sxs-lookup"><span data-stu-id="aa034-140">The load balancer uses the domain label of the public IP as prefix for its FQDN.</span></span> <span data-ttu-id="aa034-141">在此範例中，FQDN 是 *lbnrpipv4.westus.cloudapp.azure.com* 和*lbnrpipv6.westus.cloudapp.azure.com*。</span><span class="sxs-lookup"><span data-stu-id="aa034-141">In this example, the FQDNs are *lbnrpipv4.westus.cloudapp.azure.com* and *lbnrpipv6.westus.cloudapp.azure.com*.</span></span>

## <a name="create-a-front-end-ip-configurations-and-a-back-end-address-pool"></a><span data-ttu-id="aa034-142">建立前端 IP 組態和後端位址集區</span><span class="sxs-lookup"><span data-stu-id="aa034-142">Create a Front-End IP configurations and a Back-End Address Pool</span></span>

1. <span data-ttu-id="aa034-143">建立會使用您所建立之公用 IP 位址的前端位址組態。</span><span class="sxs-lookup"><span data-stu-id="aa034-143">Create front-end address configuration that uses the Public IP addresses you created.</span></span>

    ```powershell
    $FEIPConfigv4 = New-AzureRmLoadBalancerFrontendIpConfig -Name "LB-Frontendv4" -PublicIpAddress $publicIPv4
    $FEIPConfigv6 = New-AzureRmLoadBalancerFrontendIpConfig -Name "LB-Frontendv6" -PublicIpAddress $publicIPv6
    ```

2. <span data-ttu-id="aa034-144">建立後端位址集區。</span><span class="sxs-lookup"><span data-stu-id="aa034-144">Create back-end address pools.</span></span>

    ```powershell
    $backendpoolipv4 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "BackendPoolIPv4"
    $backendpoolipv6 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name "BackendPoolIPv6"
    ```

## <a name="create-lb-rules-nat-rules-a-probe-and-a-load-balancer"></a><span data-ttu-id="aa034-145">建立 LB 規則、NAT 規則、探查及負載平衡器</span><span class="sxs-lookup"><span data-stu-id="aa034-145">Create LB rules, NAT rules, a probe, and a load balancer</span></span>

<span data-ttu-id="aa034-146">此範例會建立下列項目：</span><span class="sxs-lookup"><span data-stu-id="aa034-146">This example creates the following items:</span></span>

* <span data-ttu-id="aa034-147">NAT 規則，用以將連接埠 443 上的所有傳入流量轉譯至連接埠 4443</span><span class="sxs-lookup"><span data-stu-id="aa034-147">a NAT rule to translate all incoming traffic on port 443 to port 4443</span></span>
* <span data-ttu-id="aa034-148">一個可將連接埠 80 上所有傳入流量負載平衡至後端集區中位址上連接埠 80 的負載平衡器規則。</span><span class="sxs-lookup"><span data-stu-id="aa034-148">a load balancer rule to balance all incoming traffic on port 80 to port 80 on the addresses in the back-end pool.</span></span>
* <span data-ttu-id="aa034-149">允許 RDP 連線到 VM 連接埠 3389 的負載平衡器規則。</span><span class="sxs-lookup"><span data-stu-id="aa034-149">a load balancer rule to allow RDP connection to the VMs on port 3389.</span></span>
* <span data-ttu-id="aa034-150">探查規則，用以檢查名為 *HealthProbe.aspx* 的頁面或連接埠 8080 的健全狀況</span><span class="sxs-lookup"><span data-stu-id="aa034-150">a probe rule to check the health status on a page named *HealthProbe.aspx* or a service on port 8080</span></span>
* <span data-ttu-id="aa034-151">會使用上述所有物件的負載平衡器</span><span class="sxs-lookup"><span data-stu-id="aa034-151">a load balancer that uses all these objects</span></span>

1. <span data-ttu-id="aa034-152">建立 NAT 規則。</span><span class="sxs-lookup"><span data-stu-id="aa034-152">Create the NAT rules.</span></span>

    ```powershell
    $inboundNATRule1v4 = New-AzureRmLoadBalancerInboundNatRuleConfig -Name "NicNatRulev4" -FrontendIpConfiguration $FEIPConfigv4 -Protocol TCP -FrontendPort 443 -BackendPort 4443
    $inboundNATRule1v6 = New-AzureRmLoadBalancerInboundNatRuleConfig -Name "NicNatRulev6" -FrontendIpConfiguration $FEIPConfigv6 -Protocol TCP -FrontendPort 443 -BackendPort 4443
    ```

2. <span data-ttu-id="aa034-153">建立健全狀況探查。</span><span class="sxs-lookup"><span data-stu-id="aa034-153">Create a health probe.</span></span> <span data-ttu-id="aa034-154">有兩種方式可以設定探查：</span><span class="sxs-lookup"><span data-stu-id="aa034-154">There are two ways to configure a probe:</span></span>

    <span data-ttu-id="aa034-155">HTTP 探查</span><span class="sxs-lookup"><span data-stu-id="aa034-155">HTTP probe</span></span>

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name 'HealthProbe-v4v6' -RequestPath 'HealthProbe.aspx' -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2
    ```

    <span data-ttu-id="aa034-156">或 TCP 探查</span><span class="sxs-lookup"><span data-stu-id="aa034-156">or TCP probe</span></span>

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name 'HealthProbe-v4v6' -Protocol Tcp -Port 8080 -IntervalInSeconds 15 -ProbeCount 2
    $RDPprobe = New-AzureRmLoadBalancerProbeConfig -Name 'RDPprobe' -Protocol Tcp -Port 3389 -IntervalInSeconds 15 -ProbeCount 2
    ```

    <span data-ttu-id="aa034-157">在此範例中，我們使用 TCP 探查</span><span class="sxs-lookup"><span data-stu-id="aa034-157">For this example, we are going to use the TCP probes.</span></span>

3. <span data-ttu-id="aa034-158">建立負載平衡器規則。</span><span class="sxs-lookup"><span data-stu-id="aa034-158">Create a load balancer rule.</span></span>

    ```powershell
    $lbrule1v4 = New-AzureRmLoadBalancerRuleConfig -Name "HTTPv4" -FrontendIpConfiguration $FEIPConfigv4 -BackendAddressPool $backendpoolipv4 -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 8080
    $lbrule1v6 = New-AzureRmLoadBalancerRuleConfig -Name "HTTPv6" -FrontendIpConfiguration $FEIPConfigv6 -BackendAddressPool $backendpoolipv6 -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 8080
    $RDPrule = New-AzureRmLoadBalancerRuleConfig -Name "RDPrule" -FrontendIpConfiguration $FEIPConfigv4 -BackendAddressPool $backendpoolipv4 -Probe $RDPprobe -Protocol Tcp -FrontendPort 3389 -BackendPort 3389
    ```

4. <span data-ttu-id="aa034-159">使用先前建立的物件來建立負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="aa034-159">Create the load balancer using the previously created objects.</span></span>

    ```powershell
    $NRPLB = New-AzureRmLoadBalancer -ResourceGroupName NRP-RG -Name 'myNrpIPv6LB' -Location 'West US' -FrontendIpConfiguration $FEIPConfigv4,$FEIPConfigv6 -InboundNatRule $inboundNATRule1v6,$inboundNATRule1v4 -BackendAddressPool $backendpoolipv4,$backendpoolipv6 -Probe $healthProbe,$RDPprobe -LoadBalancingRule $lbrule1v4,$lbrule1v6,$RDPrule
    ```

## <a name="create-nics-for-the-back-end-vms"></a><span data-ttu-id="aa034-160">建立後端 VM 的 NIC</span><span class="sxs-lookup"><span data-stu-id="aa034-160">Create NICs for the back-end VMs</span></span>

1. <span data-ttu-id="aa034-161">取得需要在其中建立 NIC 的虛擬網路和虛擬網路子網路。</span><span class="sxs-lookup"><span data-stu-id="aa034-161">Get the Virtual Network and Virtual Network Subnet, where the NICs need to be created.</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -Name VNet -ResourceGroupName NRP-RG
    $backendSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -VirtualNetwork $vnet
    ```

2. <span data-ttu-id="aa034-162">建立VM 的 IP 組態和 NIC。</span><span class="sxs-lookup"><span data-stu-id="aa034-162">Create IP configurations and NICs for the VMs.</span></span>

    ```powershell
    $nic1IPv4 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv4IPConfig" -PrivateIpAddressVersion "IPv4" -Subnet $backendSubnet -LoadBalancerBackendAddressPool $backendpoolipv4 -LoadBalancerInboundNatRule $inboundNATRule1v4
    $nic1IPv6 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv6IPConfig" -PrivateIpAddressVersion "IPv6" -LoadBalancerBackendAddressPool $backendpoolipv6 -LoadBalancerInboundNatRule $inboundNATRule1v6
    $nic1 = New-AzureRmNetworkInterface -Name 'myNrpIPv6Nic0' -IpConfiguration $nic1IPv4,$nic1IPv6 -ResourceGroupName NRP-RG -Location 'West US'

    $nic2IPv4 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv4IPConfig" -PrivateIpAddressVersion "IPv4" -Subnet $backendSubnet -LoadBalancerBackendAddressPool $backendpoolipv4
    $nic2IPv6 = New-AzureRmNetworkInterfaceIpConfig -Name "IPv6IPConfig" -PrivateIpAddressVersion "IPv6" -LoadBalancerBackendAddressPool $backendpoolipv6
    $nic2 = New-AzureRmNetworkInterface -Name 'myNrpIPv6Nic1' -IpConfiguration $nic2IPv4,$nic2IPv6 -ResourceGroupName NRP-RG -Location 'West US'
    ```

## <a name="create-virtual-machines-and-assign-the-newly-created-nics"></a><span data-ttu-id="aa034-163">建立虛擬機器並指派新建立的 NIC</span><span class="sxs-lookup"><span data-stu-id="aa034-163">Create virtual machines and assign the newly created NICs</span></span>

<span data-ttu-id="aa034-164">如需有關建立 VM 的詳細資訊，請參閱 [使用 Resource Manager 和 Azure PowerShell 建立及預先設定 Windows 虛擬機器](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="aa034-164">For more information about creating a VM, see [Create and preconfigure a Windows Virtual Machine with Resource Manager and Azure PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)</span></span>

1. <span data-ttu-id="aa034-165">建立可用性設定組和儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="aa034-165">Create an Availability Set and Storage account</span></span>

    ```powershell
    New-AzureRmAvailabilitySet -Name 'myNrpIPv6AvSet' -ResourceGroupName NRP-RG -location 'West US'
    $availabilitySet = Get-AzureRmAvailabilitySet -Name 'myNrpIPv6AvSet' -ResourceGroupName NRP-RG
    New-AzureRmStorageAccount -ResourceGroupName NRP-RG -Name 'mynrpipv6stacct' -Location 'West US' -SkuName "Standard_LRS"
    $CreatedStorageAccount = Get-AzureRmStorageAccount -ResourceGroupName NRP-RG -Name 'mynrpipv6stacct'
    ```

2. <span data-ttu-id="aa034-166">建立每個 VM 並指派先前建立的 NIC</span><span class="sxs-lookup"><span data-stu-id="aa034-166">Create each VM and assign the previous created NICs</span></span>

    ```powershell
    $mySecureCredentials= Get-Credential -Message "Type the username and password of the local administrator account."

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

## <a name="next-steps"></a><span data-ttu-id="aa034-167">後續步驟</span><span class="sxs-lookup"><span data-stu-id="aa034-167">Next steps</span></span>

[<span data-ttu-id="aa034-168">開始設定內部負載平衡器</span><span class="sxs-lookup"><span data-stu-id="aa034-168">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="aa034-169">設定負載平衡器分配模式</span><span class="sxs-lookup"><span data-stu-id="aa034-169">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="aa034-170">設定負載平衡器的閒置 TCP 逾時設定</span><span class="sxs-lookup"><span data-stu-id="aa034-170">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
