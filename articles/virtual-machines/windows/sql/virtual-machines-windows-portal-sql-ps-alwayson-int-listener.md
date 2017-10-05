---
title: "設定 Always On 可用性群組接聽程式 - Microsoft Azure | Microsoft Docs"
description: "使用具有一個或多個 IP 位址的內部負載平衡器，在 Azure Resource Manager 模型上設定可用性群組接聽程式。"
services: virtual-machines
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: monicar
ms.assetid: 14b39cde-311c-4ddf-98f3-8694e01a7d3b
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/22/2017
ms.author: mikeray
ms.openlocfilehash: 74fa1e4c9cfa608a9a385f3dd82a0599fbcc421c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="configure-one-or-more-always-on-availability-group-listeners---resource-manager"></a><span data-ttu-id="78296-103">設定一或多個 Always On 可用性群組接聽程式 - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="78296-103">Configure one or more Always On availability group listeners - Resource Manager</span></span>
<span data-ttu-id="78296-104">本主題說明如何：</span><span class="sxs-lookup"><span data-stu-id="78296-104">This topic shows how to:</span></span>

* <span data-ttu-id="78296-105">使用 PowerShell Cmdlet 為 SQL Server 可用性群組建立內部負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="78296-105">Create an internal load balancer for SQL Server availability groups using PowerShell cmdlets.</span></span>
* <span data-ttu-id="78296-106">將其他 IP 位址新增至多個可用性群組的負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="78296-106">Add additional IP addresses to a load balancer for more than one availability group.</span></span> 

<span data-ttu-id="78296-107">可用性群組接聽程式是用戶端連接以進行資料庫存取的虛擬網路名稱。</span><span class="sxs-lookup"><span data-stu-id="78296-107">An availability group listener is a virtual network name that clients connect to for database access.</span></span> <span data-ttu-id="78296-108">在 Azure 虛擬機器上，負載平衡器會保有接聽程式的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="78296-108">On Azure virtual machines, a load balancer holds the IP address for the listener.</span></span> <span data-ttu-id="78296-109">負載平衡器會將流量路由傳送至在探查連接埠上進行接聽的 SQL Server 執行個體。</span><span class="sxs-lookup"><span data-stu-id="78296-109">The load balancer routes traffic to the instance of SQL Server that is listening on the probe port.</span></span> <span data-ttu-id="78296-110">通常，可用性群組會使用內部負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="78296-110">Usually, an availability group uses an internal load balancer.</span></span> <span data-ttu-id="78296-111">Azure 內部負載平衡器可以裝載一或多個 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="78296-111">An Azure internal load balancer can host one or many IP addresses.</span></span> <span data-ttu-id="78296-112">每個 IP 位址皆使用特定的探查連接埠。</span><span class="sxs-lookup"><span data-stu-id="78296-112">Each IP address uses a specific probe port.</span></span> <span data-ttu-id="78296-113">本文件說明如何使用 PowerShell 來建立負載平衡器，或將 IP 位址新增至 SQL Server 可用性群組的現有負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="78296-113">This document shows how to use PowerShell to create a load balancer, or add IP addresses to an existing load balancer for SQL Server availability groups.</span></span> 

<span data-ttu-id="78296-114">將多個 IP 位址指派給內部負載平衡器是一項新的 Azure 功能，而且只有在 Resource Manager 模型中才可使用。</span><span class="sxs-lookup"><span data-stu-id="78296-114">The ability to assign multiple IP addresses to an internal load balancer is new to Azure and is only available in Resource Manager model.</span></span> <span data-ttu-id="78296-115">若要完成這項工作，您必須在 Resource Manager 模型中的 Azure 虛擬機器上部署 SQL Server 可用性群組。</span><span class="sxs-lookup"><span data-stu-id="78296-115">To complete this task, you need to have a SQL Server availability group deployed on Azure virtual machines in Resource Manager model.</span></span> <span data-ttu-id="78296-116">這兩部 SQL Server 虛擬機器必須屬於相同的可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="78296-116">Both SQL Server virtual machines must belong to the same availability set.</span></span> <span data-ttu-id="78296-117">您可以使用 [Microsoft 範本](virtual-machines-windows-portal-sql-alwayson-availability-groups.md) 在 Azure Resource Manager 中自動建立可用性群組。</span><span class="sxs-lookup"><span data-stu-id="78296-117">You can use the [Microsoft template](virtual-machines-windows-portal-sql-alwayson-availability-groups.md) to automatically create the availability group in Azure Resource Manager.</span></span> <span data-ttu-id="78296-118">此範本會自動為您建立可用性群組，包括內部負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="78296-118">This template automatically creates the availability group, including the internal load balancer for you.</span></span> <span data-ttu-id="78296-119">如果您想要的話，也可以[手動設定 Always On 可用性群組](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md)。</span><span class="sxs-lookup"><span data-stu-id="78296-119">If you prefer, you can [manually configure an Always On availability group](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).</span></span>

<span data-ttu-id="78296-120">本主題會要求您已經設定可用性群組。</span><span class="sxs-lookup"><span data-stu-id="78296-120">This topic requires that your availability groups are already configured.</span></span>  

<span data-ttu-id="78296-121">相關主題包括：</span><span class="sxs-lookup"><span data-stu-id="78296-121">Related topics include:</span></span>

* [<span data-ttu-id="78296-122">在 Azure VM (GUI) 中設定 AlwaysOn 可用性群組</span><span class="sxs-lookup"><span data-stu-id="78296-122">Configure AlwaysOn Availability Groups in Azure VM (GUI)</span></span>](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md)   
* [<span data-ttu-id="78296-123">使用 Azure Resource Manager 和 PowerShell 來設定 VNet 對 VNet 連線</span><span class="sxs-lookup"><span data-stu-id="78296-123">Configure a VNet-to-VNet connection by using Azure Resource Manager and PowerShell</span></span>](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md)

[!INCLUDE [Start your PowerShell session](../../../../includes/sql-vm-powershell.md)]

## <a name="configure-the-windows-firewall"></a><span data-ttu-id="78296-124">設定 Windows 防火牆</span><span class="sxs-lookup"><span data-stu-id="78296-124">Configure the Windows Firewall</span></span>
<span data-ttu-id="78296-125">設定 Windows 防火牆以允許 SQL Server 存取。</span><span class="sxs-lookup"><span data-stu-id="78296-125">Configure the Windows Firewall to allow SQL Server access.</span></span> <span data-ttu-id="78296-126">防火牆規則可允許透過 TCP 連線至 SQL Server 執行個體及接聽程式探查所使用的連接埠。</span><span class="sxs-lookup"><span data-stu-id="78296-126">The firewall rules allow TCP connections to the ports use by the SQL Server instance, and the listener probe.</span></span> <span data-ttu-id="78296-127">如需詳細的指示，請參閱[設定用於 Database Engine 存取的 Windows 防火牆](http://msdn.microsoft.com/library/ms175043.aspx#Anchor_1)。</span><span class="sxs-lookup"><span data-stu-id="78296-127">For detailed instructions, see [Configure a Windows Firewall for Database Engine Access](http://msdn.microsoft.com/library/ms175043.aspx#Anchor_1).</span></span> <span data-ttu-id="78296-128">為 SQL Server 連接埠和探查連接埠建立輸入規則。</span><span class="sxs-lookup"><span data-stu-id="78296-128">Create an inbound rule for the SQL Server port and for the probe port.</span></span>

## <a name="example-script-create-an-internal-load-balancer-with-powershell"></a><span data-ttu-id="78296-129">範例指令碼：使用 PowerShell 來建立內部負載平衡器</span><span class="sxs-lookup"><span data-stu-id="78296-129">Example Script: Create an internal load balancer with PowerShell</span></span>
> [!NOTE]
> <span data-ttu-id="78296-130">如果您使用了 [Microsoft 範本](virtual-machines-windows-portal-sql-alwayson-availability-groups.md)來建立可用性群組，則已經建立內部負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="78296-130">If you created your availability group with the [Microsoft template](virtual-machines-windows-portal-sql-alwayson-availability-groups.md), the internal load balancer was already created.</span></span> 
> 
> 

<span data-ttu-id="78296-131">下列 PowerShell 指令碼會建立內部負載平衡器、設定負載平衡規則，以及設定負載平衡器的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="78296-131">The following PowerShell script creates an internal load balancer, configures the load balancing rules, and sets an IP address for the load balancer.</span></span> <span data-ttu-id="78296-132">若要執行此指令碼，請開啟 Windows PowerShell ISE，然後將指令碼貼到 [指令碼] 窗格中。</span><span class="sxs-lookup"><span data-stu-id="78296-132">To run the script, open Windows PowerShell ISE, and paste the script in the Script pane.</span></span> <span data-ttu-id="78296-133">請使用 `Login-AzureRMAccount` 來登入 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="78296-133">Use `Login-AzureRMAccount` to log in to PowerShell.</span></span> <span data-ttu-id="78296-134">如果您有多個 Azure 訂用帳戶，請使用 `Select-AzureRmSubscription ` 來設定訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="78296-134">If you have multiple Azure subscriptions, use `Select-AzureRmSubscription ` to set the subscription.</span></span> 

```powershell
# Login-AzureRmAccount
# Select-AzureRmSubscription -SubscriptionId <xxxxxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx>

$ResourceGroupName = "<Resource Group Name>" # Resource group name
$VNetName = "<Virtual Network Name>"         # Virtual network name
$SubnetName = "<Subnet Name>"                # Subnet name
$ILBName = "<Load Balancer Name>"            # ILB name
$Location = "<Azure Region>"                 # Azure location
$VMNames = "<VM1>","<VM2>"                   # Virtual machine names

$ILBIP = "<n.n.n.n>"                         # IP address
[int]$ListenerPort = "<nnnn>"                # AG listener port
[int]$ProbePort = "<nnnn>"                   # Probe port

$LBProbeName ="ILBPROBE_$ListenerPort"       # The Load balancer Probe Object Name              
$LBConfigRuleName = "ILBCR_$ListenerPort"    # The Load Balancer Rule Object Name

$FrontEndConfigurationName = "FE_SQLAGILB_1" # Object name for the front-end configuration 
$BackEndConfigurationName ="BE_SQLAGILB_1"   # Object name for the back-end configuration

$VNet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName 

$Subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $VNet -Name $SubnetName 

$FEConfig = New-AzureRMLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -PrivateIpAddress $ILBIP -SubnetId $Subnet.id

$BEConfig = New-AzureRMLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName 

$SQLHealthProbe = New-AzureRmLoadBalancerProbeConfig -Name $LBProbeName -Protocol tcp -Port $ProbePort -IntervalInSeconds 15 -ProbeCount 2

$ILBRule = New-AzureRmLoadBalancerRuleConfig -Name $LBConfigRuleName -FrontendIpConfiguration $FEConfig -BackendAddressPool $BEConfig -Probe $SQLHealthProbe -Protocol tcp -FrontendPort $ListenerPort -BackendPort $ListenerPort -LoadDistribution Default -EnableFloatingIP 

$ILB= New-AzureRmLoadBalancer -Location $Location -Name $ILBName -ResourceGroupName $ResourceGroupName -FrontendIpConfiguration $FEConfig -BackendAddressPool $BEConfig -LoadBalancingRule $ILBRule -Probe $SQLHealthProbe 

$bepool = Get-AzureRmLoadBalancerBackendAddressPoolConfig -Name $BackEndConfigurationName -LoadBalancer $ILB 

foreach($VMName in $VMNames)
    {
        $VM = Get-AzureRmVM -ResourceGroupName $ResourceGroupName -Name $VMName 
        $NICName = ($vm.NetworkProfile.NetworkInterfaces.Id.split('/') | select -last 1)
        $NIC = Get-AzureRmNetworkInterface -name $NICName -ResourceGroupName $ResourceGroupName
        $NIC.IpConfigurations[0].LoadBalancerBackendAddressPools = $BEPool
        Set-AzureRmNetworkInterface -NetworkInterface $NIC
        start-AzureRmVM -ResourceGroupName $ResourceGroupName -Name $VM.Name 
    }
```

## <span data-ttu-id="78296-135"><a name="Add-IP"></a> 範例指令碼︰使用 PowerShell 將 IP 位址新增至現有的負載平衡器</span><span class="sxs-lookup"><span data-stu-id="78296-135"><a name="Add-IP"></a> Example script: Add an IP address to an existing load balancer with PowerShell</span></span>
<span data-ttu-id="78296-136">若要使用多個可用性群組，請將額外的 IP 位址新增至負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="78296-136">To use more than one availability group, add an additional IP address to the load balancer.</span></span> <span data-ttu-id="78296-137">每個 IP 位址都需要有自己的負載平衡規則、探查連接埠及前端連接埠。</span><span class="sxs-lookup"><span data-stu-id="78296-137">Each IP address requires its own load balancing rule, probe port, and front port.</span></span>

<span data-ttu-id="78296-138">前端連接埠是應用程式用來連線到 SQL Server 執行個體的連接埠。</span><span class="sxs-lookup"><span data-stu-id="78296-138">The front-end port is the port that applications use to connect to the SQL Server instance.</span></span> <span data-ttu-id="78296-139">不同可用性群組的 IP 位址可以使用相同的前端連接埠。</span><span class="sxs-lookup"><span data-stu-id="78296-139">IP addresses for different availability groups can use the same front-end port.</span></span>

> [!NOTE]
> <span data-ttu-id="78296-140">就 SQL Server 可用性群組而言，每個 IP 位址都需要一個特定的探查連接埠。</span><span class="sxs-lookup"><span data-stu-id="78296-140">For SQL Server availability groups, each IP address requires a specific probe port.</span></span> <span data-ttu-id="78296-141">例如，如果負載平衡器上有一個 IP 位址使用探查連接埠 59999，該負載平衡器上的任何其他 IP 位址就不能使用探查連接埠 59999。</span><span class="sxs-lookup"><span data-stu-id="78296-141">For example, if one IP address on a load balancer uses probe port 59999, no other IP addresses on that load balancer can use probe port 59999.</span></span>

* <span data-ttu-id="78296-142">如需有關負載平衡器限制的資訊，請參閱[網路限制 - Azure Resource Manager](../../../azure-subscription-service-limits.md#azure-resource-manager-virtual-networking-limits) 底下的「每個負載平衡器的私人前端 IP」。</span><span class="sxs-lookup"><span data-stu-id="78296-142">For information about load balancer limits, see **Private front end IP per load balancer** under [Networking Limits - Azure Resource Manager](../../../azure-subscription-service-limits.md#azure-resource-manager-virtual-networking-limits).</span></span>
* <span data-ttu-id="78296-143">如需有關可用性群組限制的資訊，請參閱[限制 (可用性群組)](http://msdn.microsoft.com/library/ff878487.aspx#RestrictionsAG)。</span><span class="sxs-lookup"><span data-stu-id="78296-143">For information about availability group limits, see [Restrictions (Availability Groups)](http://msdn.microsoft.com/library/ff878487.aspx#RestrictionsAG).</span></span>

<span data-ttu-id="78296-144">下列指令碼會將新的 IP 位址新增至現有的負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="78296-144">The following script adds a new IP address to an existing load balancer.</span></span> <span data-ttu-id="78296-145">ILB 會使用接聽程式連接埠作為負載平衡前端連接埠。</span><span class="sxs-lookup"><span data-stu-id="78296-145">The ILB uses the listener port for the load balancing front-end port.</span></span> <span data-ttu-id="78296-146">此連接埠可以是 SQL Server 正在接聽的連接埠。</span><span class="sxs-lookup"><span data-stu-id="78296-146">This port can be the port that SQL Server is listening on.</span></span> <span data-ttu-id="78296-147">就預設的 SQL Server 執行個體而言，連接埠是 1433。</span><span class="sxs-lookup"><span data-stu-id="78296-147">For default instances of SQL Server, the port is 1433.</span></span> <span data-ttu-id="78296-148">可用性群組的負載平衡規則需要浮動 IP (伺服器直接回傳)，因此後端連接埠與前端連接埠相同。</span><span class="sxs-lookup"><span data-stu-id="78296-148">The load balancing rule for an availability group requires a floating IP (direct server return) so the back-end port is the same as the front-end port.</span></span> <span data-ttu-id="78296-149">請更新您環境的變數。</span><span class="sxs-lookup"><span data-stu-id="78296-149">Update the variables for your environment.</span></span> 

```powershell
# Login-AzureRmAccount
# Select-AzureRmSubscription -SubscriptionId <xxxxxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx>

$ResourceGroupName = "<ResourceGroup>"          # Resource group name
$VNetName = "<VirtualNetwork>"                  # Virtual network name
$SubnetName = "<Subnet>"                        # Subnet name
$ILBName = "<ILBName>"                          # ILB name                      

$ILBIP = "<n.n.n.n>"                            # IP address
[int]$ListenerPort = "<nnnn>"                   # AG listener port
[int]$ProbePort = "<nnnnn>"                     # Probe port 

$ILB = Get-AzureRmLoadBalancer -Name $ILBName -ResourceGroupName $ResourceGroupName 

$count = $ILB.FrontendIpConfigurations.Count+1
$FrontEndConfigurationName ="FE_SQLAGILB_$count"  

$LBProbeName = "ILBPROBE_$count"
$LBConfigrulename = "ILBCR_$count"

$VNet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName 
$Subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $VNet -Name $SubnetName

$ILB | Add-AzureRmLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -PrivateIpAddress $ILBIP -SubnetId $Subnet.Id 

$ILB | Add-AzureRmLoadBalancerProbeConfig -Name $LBProbeName  -Protocol Tcp -Port $Probeport -ProbeCount 2 -IntervalInSeconds 15  | Set-AzureRmLoadBalancer 

$ILB = Get-AzureRmLoadBalancer -Name $ILBname -ResourceGroupName $ResourceGroupName

$FEConfig = get-AzureRMLoadBalancerFrontendIpConfig -Name $FrontEndConfigurationName -LoadBalancer $ILB

$SQLHealthProbe  = Get-AzureRmLoadBalancerProbeConfig -Name $LBProbeName -LoadBalancer $ILB

$BEConfig = Get-AzureRmLoadBalancerBackendAddressPoolConfig -Name $ILB.BackendAddressPools[0].Name -LoadBalancer $ILB 

$ILB | Add-AzureRmLoadBalancerRuleConfig -Name $LBConfigRuleName -FrontendIpConfiguration $FEConfig  -BackendAddressPool $BEConfig -Probe $SQLHealthProbe -Protocol tcp -FrontendPort  $ListenerPort -BackendPort $ListenerPort -LoadDistribution Default -EnableFloatingIP | Set-AzureRmLoadBalancer   
```

## <a name="configure-the-listener"></a><span data-ttu-id="78296-150">設定接聽程式</span><span class="sxs-lookup"><span data-stu-id="78296-150">Configure the listener</span></span>

[!INCLUDE [ag-listener-configure](../../../../includes/virtual-machines-ag-listener-configure.md)]

## <a name="set-the-listener-port-in-sql-server-management-studio"></a><span data-ttu-id="78296-151">在 SQL Server Management Studio 中設定接聽程式連接埠</span><span class="sxs-lookup"><span data-stu-id="78296-151">Set the listener port in SQL Server Management Studio</span></span>

1. <span data-ttu-id="78296-152">啟動 SQL Server Management Studio，然後連接到主要複本。</span><span class="sxs-lookup"><span data-stu-id="78296-152">Launch SQL Server Management Studio and connect to the primary replica.</span></span>

1. <span data-ttu-id="78296-153">瀏覽至 [AlwaysOn 高可用性] | [可用性群組] | [可用性群組接聽程式]。</span><span class="sxs-lookup"><span data-stu-id="78296-153">Navigate to **AlwaysOn High Availability** | **Availability Groups** | **Availability Group Listeners**.</span></span> 

1. <span data-ttu-id="78296-154">您現在應該會看到在容錯移轉叢集管理員中建立的接聽程式名稱。</span><span class="sxs-lookup"><span data-stu-id="78296-154">You should now see the listener name that you created in Failover Cluster Manager.</span></span> <span data-ttu-id="78296-155">以滑鼠右鍵按一下接聽程式名稱，然後按一下 [屬性] 。</span><span class="sxs-lookup"><span data-stu-id="78296-155">Right-click the listener name and click **Properties**.</span></span>

1. <span data-ttu-id="78296-156">在 [連接埠] 方塊中，使用您稍早所用的 $EndpointPort (預設值是 1433) 來指定可用性群組接聽程式的連接埠號碼，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="78296-156">In the **Port** box, specify the port number for the availability group listener by using the $EndpointPort you used earlier (1433 was the default), then click **OK**.</span></span>

## <a name="test-the-connection-to-the-listener"></a><span data-ttu-id="78296-157">測試接聽程式的連線</span><span class="sxs-lookup"><span data-stu-id="78296-157">Test the connection to the listener</span></span>

<span data-ttu-id="78296-158">若要測試連線︰</span><span class="sxs-lookup"><span data-stu-id="78296-158">To test the connection:</span></span>

1. <span data-ttu-id="78296-159">透過 RDP 連接到相同虛擬網路中不擁有複本的 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="78296-159">RDP to a SQL Server that is in the same virtual network, but does not own the replica.</span></span> <span data-ttu-id="78296-160">這可以是叢集中的其他 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="78296-160">This can be the other SQL Server in the cluster.</span></span>

1. <span data-ttu-id="78296-161">使用 **sqlcmd** 公用程式來測試連線。</span><span class="sxs-lookup"><span data-stu-id="78296-161">Use **sqlcmd** utility to test the connection.</span></span> <span data-ttu-id="78296-162">例如，下列指令碼會透過接聽程式搭配 Windows 驗證，建立與主要複本的 **sqlcmd** 連線︰</span><span class="sxs-lookup"><span data-stu-id="78296-162">For example, the following script establishes a **sqlcmd** connection to the primary replica through the listener with Windows authentication:</span></span>
   
    ```
    sqlmd -S <listenerName> -E
    ```
   
    <span data-ttu-id="78296-163">如果接聽程式使用預設連接埠 (1433) 以外的連接埠，請在連接字串中指定該連接埠。</span><span class="sxs-lookup"><span data-stu-id="78296-163">If the listener is using a port other than the default port (1433), specify the port in the connection string.</span></span> <span data-ttu-id="78296-164">例如，下列 sqlcmd 命令會連線到位於連接埠 1435 的接聽程式︰</span><span class="sxs-lookup"><span data-stu-id="78296-164">For example, the following sqlcmd command connects to a listener at port 1435:</span></span> 
   
    ```
    sqlcmd -S <listenerName>,1435 -E
    ```

<span data-ttu-id="78296-165">SQLCMD 連線會自動連線到任何一個裝載主要複本的 SQL Server 執行個體。</span><span class="sxs-lookup"><span data-stu-id="78296-165">The SQLCMD connection automatically connects to whichever instance of SQL Server hosts the primary replica.</span></span> 

> [!NOTE]
> <span data-ttu-id="78296-166">確定您指定的連接埠在兩部 SQL Server 在防火牆上開啟。</span><span class="sxs-lookup"><span data-stu-id="78296-166">Make sure that the port you specify is open on the firewall of both SQL Servers.</span></span> <span data-ttu-id="78296-167">這兩部伺服器需要您使用的 TCP 連接埠的輸入規則。</span><span class="sxs-lookup"><span data-stu-id="78296-167">Both servers require an inbound rule for the TCP port that you use.</span></span> <span data-ttu-id="78296-168">如需詳細資訊，請參閱 [新增或編輯防火牆規則](http://technet.microsoft.com/library/cc753558.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="78296-168">See [Add or Edit Firewall Rule](http://technet.microsoft.com/library/cc753558.aspx) for more information.</span></span> 
> 
> 

## <a name="guidelines-and-limitations"></a><span data-ttu-id="78296-169">指導方針和限制</span><span class="sxs-lookup"><span data-stu-id="78296-169">Guidelines and limitations</span></span>
<span data-ttu-id="78296-170">請注意，下列關於 Azure 中使用內部負載平衡器之可用性群組接聽程式的指導方針：</span><span class="sxs-lookup"><span data-stu-id="78296-170">Note the following guidelines on availability group listener in Azure using internal load balancer:</span></span>

* <span data-ttu-id="78296-171">使用內部負載平衡器時，您只會從相同的虛擬網路內存取接聽程式。</span><span class="sxs-lookup"><span data-stu-id="78296-171">With an internal load balancer, you only access the listener from within the same virtual network.</span></span>


## <a name="for-more-information"></a><span data-ttu-id="78296-172">如需 Blob 的詳細資訊，</span><span class="sxs-lookup"><span data-stu-id="78296-172">For more information</span></span>
<span data-ttu-id="78296-173">如需詳細資訊，請參閱[在 Azure VM 中手動設定 Always On 可用性群組](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md)。</span><span class="sxs-lookup"><span data-stu-id="78296-173">For more information, see [Configure Always On availability group in Azure VM manually](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).</span></span>

## <a name="powershell-cmdlets"></a><span data-ttu-id="78296-174">PowerShell Cmdlet</span><span class="sxs-lookup"><span data-stu-id="78296-174">PowerShell cmdlets</span></span>
<span data-ttu-id="78296-175">請使用下列 PowerShell Cmdlet 為 Azure 虛擬機器建立內部負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="78296-175">Use the following PowerShell cmdlets to create an internal load balancer for Azure virtual machines.</span></span>

* <span data-ttu-id="78296-176">[New-AzureRmLoadBalancer](http://msdn.microsoft.com/library/mt619450.aspx) 會建立負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="78296-176">[New-AzureRmLoadBalancer](http://msdn.microsoft.com/library/mt619450.aspx) creates a load balancer.</span></span> 
* <span data-ttu-id="78296-177">[New-AzureRMLoadBalancerFrontendIpConfig](http://msdn.microsoft.com/library/mt603510.aspx) 會建立負載平衡器的前端 IP 組態。</span><span class="sxs-lookup"><span data-stu-id="78296-177">[New-AzureRMLoadBalancerFrontendIpConfig](http://msdn.microsoft.com/library/mt603510.aspx) creates a front-end IP configuration for a load balancer.</span></span> 
* <span data-ttu-id="78296-178">[New-AzureRmLoadBalancerRuleConfig](http://msdn.microsoft.com/library/mt619391.aspx) 會建立負載平衡器的規則組態。</span><span class="sxs-lookup"><span data-stu-id="78296-178">[New-AzureRmLoadBalancerRuleConfig](http://msdn.microsoft.com/library/mt619391.aspx) creates a rule configuration for a load balancer.</span></span> 
* <span data-ttu-id="78296-179">[New-AzureRmLoadBalancerBackendAddressPoolConfig](http://msdn.microsoft.com/library/mt603791.aspx) 會建立負載平衡器的後端位址集區組態。</span><span class="sxs-lookup"><span data-stu-id="78296-179">[New-AzureRmLoadBalancerBackendAddressPoolConfig](http://msdn.microsoft.com/library/mt603791.aspx) creates a backend address pool configuration for a load balancer.</span></span> 
* <span data-ttu-id="78296-180">[New-AzureRmLoadBalancerProbeConfig](http://msdn.microsoft.com/library/mt603847.aspx) 會建立負載平衡器的探查組態。</span><span class="sxs-lookup"><span data-stu-id="78296-180">[New-AzureRmLoadBalancerProbeConfig](http://msdn.microsoft.com/library/mt603847.aspx) creates a probe configuration for a load balancer.</span></span>
* <span data-ttu-id="78296-181">[Remove-AzureRmLoadBalancer](http://msdn.microsoft.com/library/mt603862.aspx) 會從 Azure 資源群組中移除負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="78296-181">[Remove-AzureRmLoadBalancer](http://msdn.microsoft.com/library/mt603862.aspx) removes a load balancer from an Azure resource group.</span></span>
