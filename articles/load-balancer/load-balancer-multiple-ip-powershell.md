---
title: "在 Azure 中的多個 IP 組態上進行負載平衡 | Microsoft Docs"
description: "在主要和次要 IP 組態間進行負載平衡。"
services: load-balancer
documentationcenter: na
author: anavinahar
manager: narayan
editor: na
ms.assetid: 244907cd-b275-4494-aaf7-dcfc4d93edfe
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/16/2017
ms.author: annahar
ms.openlocfilehash: a8550519f094ca7afcd868a14b313337627f97d3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="load-balancing-on-multiple-ip-configurations-using-powershell"></a><span data-ttu-id="985ca-103">使用 PowerShell 在多個 IP 組態上進行負載平衡</span><span class="sxs-lookup"><span data-stu-id="985ca-103">Load balancing on multiple IP configurations using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="985ca-104">入口網站</span><span class="sxs-lookup"><span data-stu-id="985ca-104">Portal</span></span>](load-balancer-multiple-ip.md)
> * [<span data-ttu-id="985ca-105">CLI</span><span class="sxs-lookup"><span data-stu-id="985ca-105">CLI</span></span>](load-balancer-multiple-ip-cli.md)
> * [<span data-ttu-id="985ca-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="985ca-106">PowerShell</span></span>](load-balancer-multiple-ip-powershell.md)

<span data-ttu-id="985ca-107">本文說明如何對次要網路介面 (NIC) 上的多個 IP 位址使用 Azure Load Balancer。</span><span class="sxs-lookup"><span data-stu-id="985ca-107">This article describes how to use Azure Load Balancer with multiple IP addresses on a secondary network interface (NIC).</span></span> <span data-ttu-id="985ca-108">在此案例中，我們有兩部執行 Windows 的 VM，每部各有一個主要和次要 NIC。</span><span class="sxs-lookup"><span data-stu-id="985ca-108">For this scenario, we have two VMs running Windows, each with a primary and a secondary NIC.</span></span> <span data-ttu-id="985ca-109">每個次要 Nic 有兩個 IP 組態。</span><span class="sxs-lookup"><span data-stu-id="985ca-109">Each of the secondary NICs have two IP configurations.</span></span> <span data-ttu-id="985ca-110">每部 VM 都裝載 contoso.com 和 fabrikam.com 兩個網站。每個網站繫結到次要 NIC 上的其中一個 IP 組態。</span><span class="sxs-lookup"><span data-stu-id="985ca-110">Each VM hosts both websites contoso.com and fabrikam.com. Each website is bound to one of the IP configurations on the secondary NIC.</span></span> <span data-ttu-id="985ca-111">我們使用 Azure Load Balancer 來公開兩個前端 IP 位址，每個網站各使用其中一個，以將流量分散給網站的個別 IP 組態。</span><span class="sxs-lookup"><span data-stu-id="985ca-111">We use Azure Load Balancer to expose two frontend IP addresses, one for each website, to distribute traffic to the respective IP configuration for the website.</span></span> <span data-ttu-id="985ca-112">此案例會在兩個前端以及兩個後端集區 IP 位址使用相同的連接埠號碼。</span><span class="sxs-lookup"><span data-stu-id="985ca-112">This scenario uses the same port number across both frontends, as well as both backend pool IP addresses.</span></span>

![LB 案例影像](./media/load-balancer-multiple-ip/lb-multi-ip.PNG)

## <a name="steps-to-load-balance-on-multiple-ip-configurations"></a><span data-ttu-id="985ca-114">在多個 IP 組態上進行負載平衡的步驟</span><span class="sxs-lookup"><span data-stu-id="985ca-114">Steps to load balance on multiple IP configurations</span></span>

<span data-ttu-id="985ca-115">請遵循下列步驟來達成本文所述案例︰</span><span class="sxs-lookup"><span data-stu-id="985ca-115">Follow the steps below to achieve the scenario outlined in this article:</span></span>

1. <span data-ttu-id="985ca-116">安裝 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="985ca-116">Install Azure PowerShell.</span></span> <span data-ttu-id="985ca-117">如需如何安裝最新版 Azure PowerShell、選取訂用帳戶，以及登入帳戶的相關資訊，請參閱[如何安裝和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="985ca-117">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for information about installing the latest version of Azure PowerShell, selecting your subscription, and signing in to your account.</span></span>
2. <span data-ttu-id="985ca-118">使用下列設定建立資源群組：</span><span class="sxs-lookup"><span data-stu-id="985ca-118">Create a resource group using the following settings:</span></span>

    ```powershell
    $location = "westcentralus".
    $myResourceGroup = "contosofabrikam"
    ```

    <span data-ttu-id="985ca-119">如需詳細資訊，請參閱[建立資源群組](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)的步驟 2。</span><span class="sxs-lookup"><span data-stu-id="985ca-119">For more information, see Step 2 of [Create a Resource Group](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span></span>

3. <span data-ttu-id="985ca-120">[建立可用性設定組](../virtual-machines/windows/tutorial-availability-sets.md?toc=%2fazure%2fload-balancer%2ftoc.json)以容納 VM。</span><span class="sxs-lookup"><span data-stu-id="985ca-120">[Create an Availability Set](../virtual-machines/windows/tutorial-availability-sets.md?toc=%2fazure%2fload-balancer%2ftoc.json) to contain your VMs.</span></span> <span data-ttu-id="985ca-121">在此案例中，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="985ca-121">For this scenario, use the following command:</span></span>

    ```powershell
    New-AzureRmAvailabilitySet -ResourceGroupName "contosofabrikam" -Name "myAvailset" -Location "West Central US"
    ```

4. <span data-ttu-id="985ca-122">遵循[建立 Windows VM](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)一文中的指示步驟 3 至 5，以準備建立具有單一 NIC 的 VM。</span><span class="sxs-lookup"><span data-stu-id="985ca-122">Follow instructions steps 3 through 5 in [Create a Windows VM](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json) article to prepare the creation of a VM with a single NIC.</span></span> <span data-ttu-id="985ca-123">執行步驟 6.1，並使用下列項目，而不是步驟 6.2︰</span><span class="sxs-lookup"><span data-stu-id="985ca-123">Execute step 6.1, and use the following instead of step 6.2:</span></span>

    ```powershell
    $availset = Get-AzureRmAvailabilitySet -ResourceGroupName "contosofabrikam" -Name "myAvailset"
    New-AzureRmVMConfig -VMName "VM1" -VMSize "Standard_DS1_v2" -AvailabilitySetId $availset.Id
    ```

    <span data-ttu-id="985ca-124">然後完成[建立 Windows VM](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)的步驟 6.3 至 6.8。</span><span class="sxs-lookup"><span data-stu-id="985ca-124">Then complete [Create a Windows VM](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json) steps 6.3 through 6.8.</span></span>

5. <span data-ttu-id="985ca-125">在每個 VM 中新增第二個 IP 組態。</span><span class="sxs-lookup"><span data-stu-id="985ca-125">Add a second IP configuration to each of the VMs.</span></span> <span data-ttu-id="985ca-126">遵循[對虛擬機器指派多個 IP 位址](../virtual-network/virtual-network-multiple-ip-addresses-powershell.md#add)一文中的指示。</span><span class="sxs-lookup"><span data-stu-id="985ca-126">Follow the instructions in [Assign multiple IP addresses to virtual machines](../virtual-network/virtual-network-multiple-ip-addresses-powershell.md#add) article.</span></span> <span data-ttu-id="985ca-127">使用下列組態設定：</span><span class="sxs-lookup"><span data-stu-id="985ca-127">Use the following configuration settings:</span></span>

    ```powershell
    $NicName = "VM1-NIC2"
    $RgName = "contosofabrikam"
    $NicLocation = "West Central US"
    $IPConfigName4 = "VM1-ipconfig2"
    $Subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "mySubnet" -VirtualNetwork $myVnet
    ```

    <span data-ttu-id="985ca-128">在進行本教學課程時，並不需要讓次要 IP 組態與公用 IP 建立關聯。</span><span class="sxs-lookup"><span data-stu-id="985ca-128">You do not need to associate the secondary IP configurations with public IPs for the purpose of this tutorial.</span></span> <span data-ttu-id="985ca-129">請編輯命令以移除公用 IP 關聯部分。</span><span class="sxs-lookup"><span data-stu-id="985ca-129">Edit the command to remove the public IP association part.</span></span>

6. <span data-ttu-id="985ca-130">針對 VM2 再次完成本文的步驟 4 到 6。</span><span class="sxs-lookup"><span data-stu-id="985ca-130">Complete steps 4 through 6 of this article again for VM2.</span></span> <span data-ttu-id="985ca-131">在進行這項操作時，請務必將 VM 名稱改為 VM2。</span><span class="sxs-lookup"><span data-stu-id="985ca-131">Be sure to replace the VM name to VM2 when doing this.</span></span> <span data-ttu-id="985ca-132">請注意，您不需要為第二個 VM 建立虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="985ca-132">Note that you do not need to create a virtual network for the second VM.</span></span> <span data-ttu-id="985ca-133">視您的使用案例而定，您不一定需要建立新的子網路。</span><span class="sxs-lookup"><span data-stu-id="985ca-133">You may or may not create a new subnet based on your use case.</span></span>

7. <span data-ttu-id="985ca-134">建立兩個公用 IP 位址，並將它們儲存在適當的變數中，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="985ca-134">Create two public IP addresses and store them in the appropriate variables as shown:</span></span>

    ```powershell
    $publicIP1 = New-AzureRmPublicIpAddress -Name PublicIp1 -ResourceGroupName contosofabrikam -Location 'West Central US' -AllocationMethod Dynamic -DomainNameLabel contoso
    $publicIP2 = New-AzureRmPublicIpAddress -Name PublicIp2 -ResourceGroupName contosofabrikam -Location 'West Central US' -AllocationMethod Dynamic -DomainNameLabel fabrikam

    $publicIP1 = Get-AzureRmPublicIpAddress -Name PublicIp1 -ResourceGroupName contosofabrikam
    $publicIP2 = Get-AzureRmPublicIpAddress -Name PublicIp2 -ResourceGroupName contosofabrikam
    ```

8. <span data-ttu-id="985ca-135">建立兩個前端 IP 組態：</span><span class="sxs-lookup"><span data-stu-id="985ca-135">Create two frontend IP configurations:</span></span>

    ```powershell
    $frontendIP1 = New-AzureRmLoadBalancerFrontendIpConfig -Name contosofe -PublicIpAddress $publicIP1
    $frontendIP2 = New-AzureRmLoadBalancerFrontendIpConfig -Name fabrikamfe -PublicIpAddress $publicIP2
    ```

9. <span data-ttu-id="985ca-136">建立後端位址集區、探查和負載平衡規則︰</span><span class="sxs-lookup"><span data-stu-id="985ca-136">Create your backend address pools, a probe, and your load balancing rules:</span></span>

    ```powershell
    $beaddresspool1 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name contosopool
    $beaddresspool2 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name fabrikampool

    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name HTTP -RequestPath 'index.html' -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2

    $lbrule1 = New-AzureRmLoadBalancerRuleConfig -Name HTTPc -FrontendIpConfiguration $frontendIP1 -BackendAddressPool $beaddresspool1 -Probe $healthprobe -Protocol Tcp -FrontendPort 80 -BackendPort 80
    $lbrule2 = New-AzureRmLoadBalancerRuleConfig -Name HTTPf -FrontendIpConfiguration $frontendIP2 -BackendAddressPool $beaddresspool2 -Probe $healthprobe -Protocol Tcp -FrontendPort 80 -BackendPort 80
    ```

10. <span data-ttu-id="985ca-137">建立好這些資源後，請建立負載平衡器︰</span><span class="sxs-lookup"><span data-stu-id="985ca-137">Once you have these resources created, create your load balancer:</span></span>

    ```powershell
    $mylb = New-AzureRmLoadBalancer -ResourceGroupName contosofabrikam -Name mylb -Location 'West Central US' -FrontendIpConfiguration $frontendIP1 -LoadBalancingRule $lbrule -BackendAddressPool $beAddressPool -Probe $healthProbe
    ```

11. <span data-ttu-id="985ca-138">在新建立的負載平衡器中新增第二個後端位址集區和前端 IP 組態︰</span><span class="sxs-lookup"><span data-stu-id="985ca-138">Add the second backend address pool and frontend IP configuration to your newly created load balancer:</span></span>

    ```powershell
    $mylb = Get-AzureRmLoadBalancer -Name "mylb" -ResourceGroupName $myResourceGroup | Add-AzureRmLoadBalancerBackendAddressPoolConfig -Name fabrikampool | Set-AzureRmLoadBalancer

    $mylb | Add-AzureRmLoadBalancerFrontendIpConfig -Name fabrikamfe -PublicIpAddress $publicIP2 | Set-AzureRmLoadBalancer
    
    Add-AzureRmLoadBalancerRuleConfig -Name HTTP -LoadBalancer $mylb -FrontendIpConfiguration $frontendIP2 -BackendAddressPool $beaddresspool2 -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80 | Set-AzureRmLoadBalancer
    ```

12. <span data-ttu-id="985ca-139">下列命令會取得 NIC，然後將每個次要 NIC 的這兩個 IP 組態新增至負載平衡器的後端位址集區︰</span><span class="sxs-lookup"><span data-stu-id="985ca-139">The commands below get the NICs and then add both IP configurations of each secondary NIC to the backend address pool of the load balancer:</span></span>

    ```powershell
    $nic1 = Get-AzureRmNetworkInterface -Name "VM1-NIC2" -ResourceGroupName "MyResourcegroup";
    $nic2 = Get-AzureRmNetworkInterface -Name "VM2-NIC2" -ResourceGroupName "MyResourcegroup";

    $nic1.IpConfigurations[0].LoadBalancerBackendAddressPools.Add($mylb.BackendAddressPools[0]);
    $nic1.IpConfigurations[1].LoadBalancerBackendAddressPools.Add($mylb.BackendAddressPools[1]);
    $nic2.IpConfigurations[0].LoadBalancerBackendAddressPools.Add($mylb.BackendAddressPools[0]);
    $nic2.IpConfigurations[1].LoadBalancerBackendAddressPools.Add($mylb.BackendAddressPools[1]);

    $mylb = $mylb | Set-AzureRmLoadBalancer

    $nic1 | Set-AzureRmNetworkInterface
    $nic2 | Set-AzureRmNetworkInterface
    ```

13. <span data-ttu-id="985ca-140">最後，您必須將 DNS 資源記錄設定為指向 Load Balancer 的個別前端 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="985ca-140">Finally, you must configure DNS resource records to point to the respective frontend IP address of the Load Balancer.</span></span> <span data-ttu-id="985ca-141">您可以在 Azure DNS 中裝載網域。</span><span class="sxs-lookup"><span data-stu-id="985ca-141">You may host your domains in Azure DNS.</span></span> <span data-ttu-id="985ca-142">如需搭配使用 Azure DNS 與 Load Balancer 的詳細資訊，請參閱[使用 Azure DNS 搭配其他 Azure 服務](../dns/dns-for-azure-services.md)。</span><span class="sxs-lookup"><span data-stu-id="985ca-142">For more information about using Azure DNS with Load Balancer, see [Using Azure DNS with other Azure services](../dns/dns-for-azure-services.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="985ca-143">後續步驟</span><span class="sxs-lookup"><span data-stu-id="985ca-143">Next steps</span></span>
- <span data-ttu-id="985ca-144">若要深入了解如何在 Azure 中合併負載平衡服務，請參閱[在 Azure 中使用負載平衡服務](../traffic-manager/traffic-manager-load-balancing-azure.md)。</span><span class="sxs-lookup"><span data-stu-id="985ca-144">Learn more about how to combine load balancing services in Azure in [Using load-balancing services in Azure](../traffic-manager/traffic-manager-load-balancing-azure.md).</span></span>
- <span data-ttu-id="985ca-145">若要深入了解如何在 Azure 中使用不同類型的 記錄檔來管理負載平衡器和針對其問題進行疑難排解，請參閱 [Azure Load Balancer 的 Log Analytics](../load-balancer/load-balancer-monitor-log.md)。</span><span class="sxs-lookup"><span data-stu-id="985ca-145">Learn how you can use different types of logs in Azure to manage and troubleshoot load balancer in [Log analytics for Azure Load Balancer](../load-balancer/load-balancer-monitor-log.md).</span></span>
