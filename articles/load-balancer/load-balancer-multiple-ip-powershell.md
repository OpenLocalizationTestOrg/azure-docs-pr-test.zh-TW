---
title: "在 Azure 中的多個 IP 組態上的平衡 aaaLoad |Microsoft 文件"
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
ms.openlocfilehash: fe1cdb317350942ff759229491c2025e98dd24a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="load-balancing-on-multiple-ip-configurations-using-powershell"></a><span data-ttu-id="9e57e-103">使用 PowerShell 在多個 IP 組態上進行負載平衡</span><span class="sxs-lookup"><span data-stu-id="9e57e-103">Load balancing on multiple IP configurations using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="9e57e-104">入口網站</span><span class="sxs-lookup"><span data-stu-id="9e57e-104">Portal</span></span>](load-balancer-multiple-ip.md)
> * [<span data-ttu-id="9e57e-105">CLI</span><span class="sxs-lookup"><span data-stu-id="9e57e-105">CLI</span></span>](load-balancer-multiple-ip-cli.md)
> * [<span data-ttu-id="9e57e-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9e57e-106">PowerShell</span></span>](load-balancer-multiple-ip-powershell.md)

<span data-ttu-id="9e57e-107">本文說明如何 toouse Azure 負載平衡器與多個 IP 位址上的次要網路介面 (NIC)。</span><span class="sxs-lookup"><span data-stu-id="9e57e-107">This article describes how toouse Azure Load Balancer with multiple IP addresses on a secondary network interface (NIC).</span></span> <span data-ttu-id="9e57e-108">在此案例中，我們有兩部執行 Windows 的 VM，每部各有一個主要和次要 NIC。</span><span class="sxs-lookup"><span data-stu-id="9e57e-108">For this scenario, we have two VMs running Windows, each with a primary and a secondary NIC.</span></span> <span data-ttu-id="9e57e-109">每個次要 hello Nic 有兩個 IP 組態。</span><span class="sxs-lookup"><span data-stu-id="9e57e-109">Each of hello secondary NICs have two IP configurations.</span></span> <span data-ttu-id="9e57e-110">每部 VM 都裝載 contoso.com 和 fabrikam.com 兩個網站。每個網站會繫結的 tooone 的 hello hello 次要 NIC 上的 IP 組態</span><span class="sxs-lookup"><span data-stu-id="9e57e-110">Each VM hosts both websites contoso.com and fabrikam.com. Each website is bound tooone of hello IP configurations on hello secondary NIC.</span></span> <span data-ttu-id="9e57e-111">我們使用 Azure 負載平衡器 tooexpose 兩個前端 IP 位址，一個用於每個網站，toodistribute 流量 toohello 個別的 IP 組態 hello 網站。</span><span class="sxs-lookup"><span data-stu-id="9e57e-111">We use Azure Load Balancer tooexpose two frontend IP addresses, one for each website, toodistribute traffic toohello respective IP configuration for hello website.</span></span> <span data-ttu-id="9e57e-112">這種情況下使用 hello 跨前端，以及兩個後端集區 IP 位址相同的連接埠號碼。</span><span class="sxs-lookup"><span data-stu-id="9e57e-112">This scenario uses hello same port number across both frontends, as well as both backend pool IP addresses.</span></span>

![LB 案例影像](./media/load-balancer-multiple-ip/lb-multi-ip.PNG)

## <a name="steps-tooload-balance-on-multiple-ip-configurations"></a><span data-ttu-id="9e57e-114">多個 IP 組態步驟 tooload 餘額</span><span class="sxs-lookup"><span data-stu-id="9e57e-114">Steps tooload balance on multiple IP configurations</span></span>

<span data-ttu-id="9e57e-115">請遵循下面這篇文章所述的 tooachieve hello 案例 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="9e57e-115">Follow hello steps below tooachieve hello scenario outlined in this article:</span></span>

1. <span data-ttu-id="9e57e-116">安裝 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="9e57e-116">Install Azure PowerShell.</span></span> <span data-ttu-id="9e57e-117">請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)如需有關安裝 hello 最新版本的 Azure PowerShell 中，選取您的訂閱，並登入 tooyour 帳戶資訊。</span><span class="sxs-lookup"><span data-stu-id="9e57e-117">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for information about installing hello latest version of Azure PowerShell, selecting your subscription, and signing in tooyour account.</span></span>
2. <span data-ttu-id="9e57e-118">建立資源群組使用 hello 下列設定：</span><span class="sxs-lookup"><span data-stu-id="9e57e-118">Create a resource group using hello following settings:</span></span>

    ```powershell
    $location = "westcentralus".
    $myResourceGroup = "contosofabrikam"
    ```

    <span data-ttu-id="9e57e-119">如需詳細資訊，請參閱[建立資源群組](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)的步驟 2。</span><span class="sxs-lookup"><span data-stu-id="9e57e-119">For more information, see Step 2 of [Create a Resource Group](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span></span>

3. <span data-ttu-id="9e57e-120">[建立可用性設定組](../virtual-machines/windows/tutorial-availability-sets.md?toc=%2fazure%2fload-balancer%2ftoc.json)toocontain Vm。</span><span class="sxs-lookup"><span data-stu-id="9e57e-120">[Create an Availability Set](../virtual-machines/windows/tutorial-availability-sets.md?toc=%2fazure%2fload-balancer%2ftoc.json) toocontain your VMs.</span></span> <span data-ttu-id="9e57e-121">此案例中，使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="9e57e-121">For this scenario, use hello following command:</span></span>

    ```powershell
    New-AzureRmAvailabilitySet -ResourceGroupName "contosofabrikam" -Name "myAvailset" -Location "West Central US"
    ```

4. <span data-ttu-id="9e57e-122">請依照下列指示步驟 3 至 5[建立 Windows VM](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)文章 tooprepare hello 建立與單一 NIC VM</span><span class="sxs-lookup"><span data-stu-id="9e57e-122">Follow instructions steps 3 through 5 in [Create a Windows VM](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json) article tooprepare hello creation of a VM with a single NIC.</span></span> <span data-ttu-id="9e57e-123">執行步驟 6.1，並使用 hello 下列而非 6.2 步驟：</span><span class="sxs-lookup"><span data-stu-id="9e57e-123">Execute step 6.1, and use hello following instead of step 6.2:</span></span>

    ```powershell
    $availset = Get-AzureRmAvailabilitySet -ResourceGroupName "contosofabrikam" -Name "myAvailset"
    New-AzureRmVMConfig -VMName "VM1" -VMSize "Standard_DS1_v2" -AvailabilitySetId $availset.Id
    ```

    <span data-ttu-id="9e57e-124">然後完成[建立 Windows VM](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)的步驟 6.3 至 6.8。</span><span class="sxs-lookup"><span data-stu-id="9e57e-124">Then complete [Create a Windows VM](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json) steps 6.3 through 6.8.</span></span>

5. <span data-ttu-id="9e57e-125">新增第二個 IP 組態 tooeach 的 hello Vm。</span><span class="sxs-lookup"><span data-stu-id="9e57e-125">Add a second IP configuration tooeach of hello VMs.</span></span> <span data-ttu-id="9e57e-126">請依照下列中的 hello 指示[指派多個 IP 位址 toovirtual 機器](../virtual-network/virtual-network-multiple-ip-addresses-powershell.md#add)發行項。</span><span class="sxs-lookup"><span data-stu-id="9e57e-126">Follow hello instructions in [Assign multiple IP addresses toovirtual machines](../virtual-network/virtual-network-multiple-ip-addresses-powershell.md#add) article.</span></span> <span data-ttu-id="9e57e-127">使用下列組態設定的 hello:</span><span class="sxs-lookup"><span data-stu-id="9e57e-127">Use hello following configuration settings:</span></span>

    ```powershell
    $NicName = "VM1-NIC2"
    $RgName = "contosofabrikam"
    $NicLocation = "West Central US"
    $IPConfigName4 = "VM1-ipconfig2"
    $Subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "mySubnet" -VirtualNetwork $myVnet
    ```

    <span data-ttu-id="9e57e-128">您不需要此教學課程中的 hello 目的 tooassociate hello 次要 IP 組態與公用 Ip。</span><span class="sxs-lookup"><span data-stu-id="9e57e-128">You do not need tooassociate hello secondary IP configurations with public IPs for hello purpose of this tutorial.</span></span> <span data-ttu-id="9e57e-129">編輯 hello 命令 tooremove hello 公用 IP 關聯組件。</span><span class="sxs-lookup"><span data-stu-id="9e57e-129">Edit hello command tooremove hello public IP association part.</span></span>

6. <span data-ttu-id="9e57e-130">針對 VM2 再次完成本文的步驟 4 到 6。</span><span class="sxs-lookup"><span data-stu-id="9e57e-130">Complete steps 4 through 6 of this article again for VM2.</span></span> <span data-ttu-id="9e57e-131">這項操作時，是確定 tooreplace hello VM 名稱 tooVM2。</span><span class="sxs-lookup"><span data-stu-id="9e57e-131">Be sure tooreplace hello VM name tooVM2 when doing this.</span></span> <span data-ttu-id="9e57e-132">請注意，您不需要虛擬網路 toocreate hello 第二個 VM。</span><span class="sxs-lookup"><span data-stu-id="9e57e-132">Note that you do not need toocreate a virtual network for hello second VM.</span></span> <span data-ttu-id="9e57e-133">視您的使用案例而定，您不一定需要建立新的子網路。</span><span class="sxs-lookup"><span data-stu-id="9e57e-133">You may or may not create a new subnet based on your use case.</span></span>

7. <span data-ttu-id="9e57e-134">建立兩個公用 IP 位址，並將其儲存在 hello 適當的變數，如下所示：</span><span class="sxs-lookup"><span data-stu-id="9e57e-134">Create two public IP addresses and store them in hello appropriate variables as shown:</span></span>

    ```powershell
    $publicIP1 = New-AzureRmPublicIpAddress -Name PublicIp1 -ResourceGroupName contosofabrikam -Location 'West Central US' -AllocationMethod Dynamic -DomainNameLabel contoso
    $publicIP2 = New-AzureRmPublicIpAddress -Name PublicIp2 -ResourceGroupName contosofabrikam -Location 'West Central US' -AllocationMethod Dynamic -DomainNameLabel fabrikam

    $publicIP1 = Get-AzureRmPublicIpAddress -Name PublicIp1 -ResourceGroupName contosofabrikam
    $publicIP2 = Get-AzureRmPublicIpAddress -Name PublicIp2 -ResourceGroupName contosofabrikam
    ```

8. <span data-ttu-id="9e57e-135">建立兩個前端 IP 組態：</span><span class="sxs-lookup"><span data-stu-id="9e57e-135">Create two frontend IP configurations:</span></span>

    ```powershell
    $frontendIP1 = New-AzureRmLoadBalancerFrontendIpConfig -Name contosofe -PublicIpAddress $publicIP1
    $frontendIP2 = New-AzureRmLoadBalancerFrontendIpConfig -Name fabrikamfe -PublicIpAddress $publicIP2
    ```

9. <span data-ttu-id="9e57e-136">建立後端位址集區、探查和負載平衡規則︰</span><span class="sxs-lookup"><span data-stu-id="9e57e-136">Create your backend address pools, a probe, and your load balancing rules:</span></span>

    ```powershell
    $beaddresspool1 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name contosopool
    $beaddresspool2 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name fabrikampool

    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name HTTP -RequestPath 'index.html' -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2

    $lbrule1 = New-AzureRmLoadBalancerRuleConfig -Name HTTPc -FrontendIpConfiguration $frontendIP1 -BackendAddressPool $beaddresspool1 -Probe $healthprobe -Protocol Tcp -FrontendPort 80 -BackendPort 80
    $lbrule2 = New-AzureRmLoadBalancerRuleConfig -Name HTTPf -FrontendIpConfiguration $frontendIP2 -BackendAddressPool $beaddresspool2 -Probe $healthprobe -Protocol Tcp -FrontendPort 80 -BackendPort 80
    ```

10. <span data-ttu-id="9e57e-137">建立好這些資源後，請建立負載平衡器︰</span><span class="sxs-lookup"><span data-stu-id="9e57e-137">Once you have these resources created, create your load balancer:</span></span>

    ```powershell
    $mylb = New-AzureRmLoadBalancer -ResourceGroupName contosofabrikam -Name mylb -Location 'West Central US' -FrontendIpConfiguration $frontendIP1 -LoadBalancingRule $lbrule -BackendAddressPool $beAddressPool -Probe $healthProbe
    ```

11. <span data-ttu-id="9e57e-138">新增 hello 第二個後端位址集區和前端 IP 組態 tooyour 新建立的負載平衡器：</span><span class="sxs-lookup"><span data-stu-id="9e57e-138">Add hello second backend address pool and frontend IP configuration tooyour newly created load balancer:</span></span>

    ```powershell
    $mylb = Get-AzureRmLoadBalancer -Name "mylb" -ResourceGroupName $myResourceGroup | Add-AzureRmLoadBalancerBackendAddressPoolConfig -Name fabrikampool | Set-AzureRmLoadBalancer

    $mylb | Add-AzureRmLoadBalancerFrontendIpConfig -Name fabrikamfe -PublicIpAddress $publicIP2 | Set-AzureRmLoadBalancer
    
    Add-AzureRmLoadBalancerRuleConfig -Name HTTP -LoadBalancer $mylb -FrontendIpConfiguration $frontendIP2 -BackendAddressPool $beaddresspool2 -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80 | Set-AzureRmLoadBalancer
    ```

12. <span data-ttu-id="9e57e-139">下列的 hello 命令取得 hello Nic，並將每個次要 NIC toohello 後端位址集區的 hello 這兩個 ipconfiguration 的負載平衡器：</span><span class="sxs-lookup"><span data-stu-id="9e57e-139">hello commands below get hello NICs and then add both IP configurations of each secondary NIC toohello backend address pool of hello load balancer:</span></span>

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

13. <span data-ttu-id="9e57e-140">最後，您必須設定 DNS 資源記錄 toopoint toohello 各自的前端 IP 位址的 hello 負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="9e57e-140">Finally, you must configure DNS resource records toopoint toohello respective frontend IP address of hello Load Balancer.</span></span> <span data-ttu-id="9e57e-141">您可以在 Azure DNS 中裝載網域。</span><span class="sxs-lookup"><span data-stu-id="9e57e-141">You may host your domains in Azure DNS.</span></span> <span data-ttu-id="9e57e-142">如需搭配使用 Azure DNS 與 Load Balancer 的詳細資訊，請參閱[使用 Azure DNS 搭配其他 Azure 服務](../dns/dns-for-azure-services.md)。</span><span class="sxs-lookup"><span data-stu-id="9e57e-142">For more information about using Azure DNS with Load Balancer, see [Using Azure DNS with other Azure services](../dns/dns-for-azure-services.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9e57e-143">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9e57e-143">Next steps</span></span>
- <span data-ttu-id="9e57e-144">深入了解如何 toocombine 負載平衡服務在 Azure 中[在 Azure 中使用負載平衡服務](../traffic-manager/traffic-manager-load-balancing-azure.md)。</span><span class="sxs-lookup"><span data-stu-id="9e57e-144">Learn more about how toocombine load balancing services in Azure in [Using load-balancing services in Azure](../traffic-manager/traffic-manager-load-balancing-azure.md).</span></span>
- <span data-ttu-id="9e57e-145">了解如何在 Azure toomanage 中使用不同類型的記錄檔，以及疑難排解負載平衡器中的[Azure 負載平衡器的記錄分析](../load-balancer/load-balancer-monitor-log.md)。</span><span class="sxs-lookup"><span data-stu-id="9e57e-145">Learn how you can use different types of logs in Azure toomanage and troubleshoot load balancer in [Log analytics for Azure Load Balancer](../load-balancer/load-balancer-monitor-log.md).</span></span>
