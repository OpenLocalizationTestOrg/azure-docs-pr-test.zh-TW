---
title: "aaaConfigure 一律在可用性群組接聽程式 – Microsoft Azure |Microsoft 文件"
description: "設定可用性群組接聽程式上使用內部負載平衡器與一或多個 IP 位址的 hello Azure Resource Manager 模型。"
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
ms.openlocfilehash: 81edfe2c2ea536d8dcec466f36fccf8bc0e02c2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-one-or-more-always-on-availability-group-listeners---resource-manager"></a><span data-ttu-id="9e702-103">設定一或多個 Always On 可用性群組接聽程式 - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="9e702-103">Configure one or more Always On availability group listeners - Resource Manager</span></span>
<span data-ttu-id="9e702-104">本主題說明如何：</span><span class="sxs-lookup"><span data-stu-id="9e702-104">This topic shows how to:</span></span>

* <span data-ttu-id="9e702-105">使用 PowerShell Cmdlet 為 SQL Server 可用性群組建立內部負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="9e702-105">Create an internal load balancer for SQL Server availability groups using PowerShell cmdlets.</span></span>
* <span data-ttu-id="9e702-106">加入其他 IP 位址 tooa 負載平衡器的多個可用性群組。</span><span class="sxs-lookup"><span data-stu-id="9e702-106">Add additional IP addresses tooa load balancer for more than one availability group.</span></span> 

<span data-ttu-id="9e702-107">可用性群組接聽程式是用戶端連線 toofor 資料庫存取權的虛擬網路名稱。</span><span class="sxs-lookup"><span data-stu-id="9e702-107">An availability group listener is a virtual network name that clients connect toofor database access.</span></span> <span data-ttu-id="9e702-108">Azure 的虛擬機器上的負載平衡器會保存 hello hello 接聽程式的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="9e702-108">On Azure virtual machines, a load balancer holds hello IP address for hello listener.</span></span> <span data-ttu-id="9e702-109">hello 負載平衡器路由流量 toohello hello 探查連接埠上接聽的 SQL Server 執行個體。</span><span class="sxs-lookup"><span data-stu-id="9e702-109">hello load balancer routes traffic toohello instance of SQL Server that is listening on hello probe port.</span></span> <span data-ttu-id="9e702-110">通常，可用性群組會使用內部負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="9e702-110">Usually, an availability group uses an internal load balancer.</span></span> <span data-ttu-id="9e702-111">Azure 內部負載平衡器可以裝載一或多個 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="9e702-111">An Azure internal load balancer can host one or many IP addresses.</span></span> <span data-ttu-id="9e702-112">每個 IP 位址皆使用特定的探查連接埠。</span><span class="sxs-lookup"><span data-stu-id="9e702-112">Each IP address uses a specific probe port.</span></span> <span data-ttu-id="9e702-113">本文件說明如何 toouse PowerShell toocreate 負載平衡器，或新增 IP 位址 tooan 現有負載平衡器的 SQL Server 可用性群組。</span><span class="sxs-lookup"><span data-stu-id="9e702-113">This document shows how toouse PowerShell toocreate a load balancer, or add IP addresses tooan existing load balancer for SQL Server availability groups.</span></span> 

<span data-ttu-id="9e702-114">hello 能力 tooassign 多個 IP 位址 tooan 內部負載平衡器是新 tooAzure，只可在模型中的資源管理員。</span><span class="sxs-lookup"><span data-stu-id="9e702-114">hello ability tooassign multiple IP addresses tooan internal load balancer is new tooAzure and is only available in Resource Manager model.</span></span> <span data-ttu-id="9e702-115">toocomplete 這個工作中，您需要的 toohave Azure 資源管理員模型中的虛擬機器部署 SQL Server 可用性群組。</span><span class="sxs-lookup"><span data-stu-id="9e702-115">toocomplete this task, you need toohave a SQL Server availability group deployed on Azure virtual machines in Resource Manager model.</span></span> <span data-ttu-id="9e702-116">這兩個 SQL Server 虛擬機器必須屬於 toohello 相同可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="9e702-116">Both SQL Server virtual machines must belong toohello same availability set.</span></span> <span data-ttu-id="9e702-117">您可以使用 hello [Microsoft 範本](virtual-machines-windows-portal-sql-alwayson-availability-groups.md)tooautomatically hello 可用性群組建立 Azure 資源管理員中。</span><span class="sxs-lookup"><span data-stu-id="9e702-117">You can use hello [Microsoft template](virtual-machines-windows-portal-sql-alwayson-availability-groups.md) tooautomatically create hello availability group in Azure Resource Manager.</span></span> <span data-ttu-id="9e702-118">此範本會自動建立 hello 可用性群組，包括為您的 hello 內部負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="9e702-118">This template automatically creates hello availability group, including hello internal load balancer for you.</span></span> <span data-ttu-id="9e702-119">如果您想要的話，也可以[手動設定 Always On 可用性群組](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md)。</span><span class="sxs-lookup"><span data-stu-id="9e702-119">If you prefer, you can [manually configure an Always On availability group](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).</span></span>

<span data-ttu-id="9e702-120">本主題會要求您已經設定可用性群組。</span><span class="sxs-lookup"><span data-stu-id="9e702-120">This topic requires that your availability groups are already configured.</span></span>  

<span data-ttu-id="9e702-121">相關主題包括：</span><span class="sxs-lookup"><span data-stu-id="9e702-121">Related topics include:</span></span>

* [<span data-ttu-id="9e702-122">在 Azure VM (GUI) 中設定 AlwaysOn 可用性群組</span><span class="sxs-lookup"><span data-stu-id="9e702-122">Configure AlwaysOn Availability Groups in Azure VM (GUI)</span></span>](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md)   
* [<span data-ttu-id="9e702-123">使用 Azure Resource Manager 和 PowerShell 來設定 VNet 對 VNet 連線</span><span class="sxs-lookup"><span data-stu-id="9e702-123">Configure a VNet-to-VNet connection by using Azure Resource Manager and PowerShell</span></span>](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md)

[!INCLUDE [Start your PowerShell session](../../../../includes/sql-vm-powershell.md)]

## <a name="configure-hello-windows-firewall"></a><span data-ttu-id="9e702-124">設定 Windows 防火牆 hello</span><span class="sxs-lookup"><span data-stu-id="9e702-124">Configure hello Windows Firewall</span></span>
<span data-ttu-id="9e702-125">設定 hello Windows 防火牆 tooallow SQL Server 存取。</span><span class="sxs-lookup"><span data-stu-id="9e702-125">Configure hello Windows Firewall tooallow SQL Server access.</span></span> <span data-ttu-id="9e702-126">hello 防火牆規則允許 TCP 連接 toohello 連接埠藉由 hello SQL Server 執行個體，並使用 hello 接聽程式探查。</span><span class="sxs-lookup"><span data-stu-id="9e702-126">hello firewall rules allow TCP connections toohello ports use by hello SQL Server instance, and hello listener probe.</span></span> <span data-ttu-id="9e702-127">如需詳細的指示，請參閱[設定用於 Database Engine 存取的 Windows 防火牆](http://msdn.microsoft.com/library/ms175043.aspx#Anchor_1)。</span><span class="sxs-lookup"><span data-stu-id="9e702-127">For detailed instructions, see [Configure a Windows Firewall for Database Engine Access](http://msdn.microsoft.com/library/ms175043.aspx#Anchor_1).</span></span> <span data-ttu-id="9e702-128">建立 SQL Server 連接埠 hello 和 hello 探查連接埠的輸入的規則。</span><span class="sxs-lookup"><span data-stu-id="9e702-128">Create an inbound rule for hello SQL Server port and for hello probe port.</span></span>

## <a name="example-script-create-an-internal-load-balancer-with-powershell"></a><span data-ttu-id="9e702-129">範例指令碼：使用 PowerShell 來建立內部負載平衡器</span><span class="sxs-lookup"><span data-stu-id="9e702-129">Example Script: Create an internal load balancer with PowerShell</span></span>
> [!NOTE]
> <span data-ttu-id="9e702-130">如果您要建立可用性群組以 hello [Microsoft 範本](virtual-machines-windows-portal-sql-alwayson-availability-groups.md)，已經建立 hello 內部負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="9e702-130">If you created your availability group with hello [Microsoft template](virtual-machines-windows-portal-sql-alwayson-availability-groups.md), hello internal load balancer was already created.</span></span> 
> 
> 

<span data-ttu-id="9e702-131">hello 下列 PowerShell 指令碼會建立內部負載平衡器、 設定 hello 負載平衡規則，並且設定 IP 位址 hello 負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="9e702-131">hello following PowerShell script creates an internal load balancer, configures hello load balancing rules, and sets an IP address for hello load balancer.</span></span> <span data-ttu-id="9e702-132">toorun hello 指令碼，開啟 Windows PowerShell ISE 中，並貼上 hello 指令碼窗格中的 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="9e702-132">toorun hello script, open Windows PowerShell ISE, and paste hello script in hello Script pane.</span></span> <span data-ttu-id="9e702-133">使用`Login-AzureRMAccount`toolog tooPowerShell 中的。</span><span class="sxs-lookup"><span data-stu-id="9e702-133">Use `Login-AzureRMAccount` toolog in tooPowerShell.</span></span> <span data-ttu-id="9e702-134">如果您有多個 Azure 訂用帳戶，使用`Select-AzureRmSubscription `tooset hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="9e702-134">If you have multiple Azure subscriptions, use `Select-AzureRmSubscription ` tooset hello subscription.</span></span> 

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

$LBProbeName ="ILBPROBE_$ListenerPort"       # hello Load balancer Probe Object Name              
$LBConfigRuleName = "ILBCR_$ListenerPort"    # hello Load Balancer Rule Object Name

$FrontEndConfigurationName = "FE_SQLAGILB_1" # Object name for hello front-end configuration 
$BackEndConfigurationName ="BE_SQLAGILB_1"   # Object name for hello back-end configuration

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

## <span data-ttu-id="9e702-135"><a name="Add-IP"></a>範例指令碼： 新增 IP 位址 tooan 現有負載平衡器使用 PowerShell</span><span class="sxs-lookup"><span data-stu-id="9e702-135"><a name="Add-IP"></a> Example script: Add an IP address tooan existing load balancer with PowerShell</span></span>
<span data-ttu-id="9e702-136">以上一個可用性群組的 toouse 加入其他 IP 位址 toohello 負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="9e702-136">toouse more than one availability group, add an additional IP address toohello load balancer.</span></span> <span data-ttu-id="9e702-137">每個 IP 位址都需要有自己的負載平衡規則、探查連接埠及前端連接埠。</span><span class="sxs-lookup"><span data-stu-id="9e702-137">Each IP address requires its own load balancing rule, probe port, and front port.</span></span>

<span data-ttu-id="9e702-138">hello 應用程式使用 tooconnect toohello SQL Server 執行個體的連接埠 hello 前端連接埠。</span><span class="sxs-lookup"><span data-stu-id="9e702-138">hello front-end port is hello port that applications use tooconnect toohello SQL Server instance.</span></span> <span data-ttu-id="9e702-139">不同的可用性群組可以使用的 IP 位址 hello 相同的前端連接埠。</span><span class="sxs-lookup"><span data-stu-id="9e702-139">IP addresses for different availability groups can use hello same front-end port.</span></span>

> [!NOTE]
> <span data-ttu-id="9e702-140">就 SQL Server 可用性群組而言，每個 IP 位址都需要一個特定的探查連接埠。</span><span class="sxs-lookup"><span data-stu-id="9e702-140">For SQL Server availability groups, each IP address requires a specific probe port.</span></span> <span data-ttu-id="9e702-141">例如，如果負載平衡器上有一個 IP 位址使用探查連接埠 59999，該負載平衡器上的任何其他 IP 位址就不能使用探查連接埠 59999。</span><span class="sxs-lookup"><span data-stu-id="9e702-141">For example, if one IP address on a load balancer uses probe port 59999, no other IP addresses on that load balancer can use probe port 59999.</span></span>

* <span data-ttu-id="9e702-142">如需有關負載平衡器限制的資訊，請參閱[網路限制 - Azure Resource Manager](../../../azure-subscription-service-limits.md#azure-resource-manager-virtual-networking-limits) 底下的「每個負載平衡器的私人前端 IP」。</span><span class="sxs-lookup"><span data-stu-id="9e702-142">For information about load balancer limits, see **Private front end IP per load balancer** under [Networking Limits - Azure Resource Manager](../../../azure-subscription-service-limits.md#azure-resource-manager-virtual-networking-limits).</span></span>
* <span data-ttu-id="9e702-143">如需有關可用性群組限制的資訊，請參閱[限制 (可用性群組)](http://msdn.microsoft.com/library/ff878487.aspx#RestrictionsAG)。</span><span class="sxs-lookup"><span data-stu-id="9e702-143">For information about availability group limits, see [Restrictions (Availability Groups)](http://msdn.microsoft.com/library/ff878487.aspx#RestrictionsAG).</span></span>

<span data-ttu-id="9e702-144">hello 下列指令碼會新增新 IP 位址 tooan 現有負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="9e702-144">hello following script adds a new IP address tooan existing load balancer.</span></span> <span data-ttu-id="9e702-145">hello ILB hello 負載平衡前端連接埠使用 hello 接聽程式通訊埠。</span><span class="sxs-lookup"><span data-stu-id="9e702-145">hello ILB uses hello listener port for hello load balancing front-end port.</span></span> <span data-ttu-id="9e702-146">此連接埠可以是 SQL Server 正在接聽的 hello 連接埠。</span><span class="sxs-lookup"><span data-stu-id="9e702-146">This port can be hello port that SQL Server is listening on.</span></span> <span data-ttu-id="9e702-147">SQL server 的預設執行個體，hello 連接埠為 1433年。</span><span class="sxs-lookup"><span data-stu-id="9e702-147">For default instances of SQL Server, hello port is 1433.</span></span> <span data-ttu-id="9e702-148">hello 負載平衡可用性群組的規則需要浮動 IP （伺服器直接回傳） 因此 hello 後端連接埠是 hello 相同做為 hello 前端連接埠。</span><span class="sxs-lookup"><span data-stu-id="9e702-148">hello load balancing rule for an availability group requires a floating IP (direct server return) so hello back-end port is hello same as hello front-end port.</span></span> <span data-ttu-id="9e702-149">更新您的環境的 hello 變數。</span><span class="sxs-lookup"><span data-stu-id="9e702-149">Update hello variables for your environment.</span></span> 

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

## <a name="configure-hello-listener"></a><span data-ttu-id="9e702-150">Hello 接聽程式設定</span><span class="sxs-lookup"><span data-stu-id="9e702-150">Configure hello listener</span></span>

[!INCLUDE [ag-listener-configure](../../../../includes/virtual-machines-ag-listener-configure.md)]

## <a name="set-hello-listener-port-in-sql-server-management-studio"></a><span data-ttu-id="9e702-151">設定 SQL Server Management Studio 中的 hello 接聽程式通訊埠</span><span class="sxs-lookup"><span data-stu-id="9e702-151">Set hello listener port in SQL Server Management Studio</span></span>

1. <span data-ttu-id="9e702-152">啟動 SQL Server Management Studio 並連接 toohello 主要複本。</span><span class="sxs-lookup"><span data-stu-id="9e702-152">Launch SQL Server Management Studio and connect toohello primary replica.</span></span>

1. <span data-ttu-id="9e702-153">瀏覽過**AlwaysOn 高可用性** | **可用性群組** | **可用性群組接聽程式**。</span><span class="sxs-lookup"><span data-stu-id="9e702-153">Navigate too**AlwaysOn High Availability** | **Availability Groups** | **Availability Group Listeners**.</span></span> 

1. <span data-ttu-id="9e702-154">您現在應該會看到您在建立容錯移轉叢集管理員 中的 hello 接聽程式名稱。</span><span class="sxs-lookup"><span data-stu-id="9e702-154">You should now see hello listener name that you created in Failover Cluster Manager.</span></span> <span data-ttu-id="9e702-155">以滑鼠右鍵按一下 hello 接聽程式名稱，然後按一下**屬性**。</span><span class="sxs-lookup"><span data-stu-id="9e702-155">Right-click hello listener name and click **Properties**.</span></span>

1. <span data-ttu-id="9e702-156">在 hello**連接埠**方塊中，使用 hello $EndpointPort 您稍早所指定 hello hello 可用性群組接聽程式的連接埠號碼 （1433年是 hello 預設值），然後按一下 **確定**。</span><span class="sxs-lookup"><span data-stu-id="9e702-156">In hello **Port** box, specify hello port number for hello availability group listener by using hello $EndpointPort you used earlier (1433 was hello default), then click **OK**.</span></span>

## <a name="test-hello-connection-toohello-listener"></a><span data-ttu-id="9e702-157">測試 hello 連接 toohello 接聽程式</span><span class="sxs-lookup"><span data-stu-id="9e702-157">Test hello connection toohello listener</span></span>

<span data-ttu-id="9e702-158">tootest hello 連線：</span><span class="sxs-lookup"><span data-stu-id="9e702-158">tootest hello connection:</span></span>

1. <span data-ttu-id="9e702-159">RDP tooa hello 中的 SQL Server 相同虛擬網路，但不會無法自己 hello 複本。</span><span class="sxs-lookup"><span data-stu-id="9e702-159">RDP tooa SQL Server that is in hello same virtual network, but does not own hello replica.</span></span> <span data-ttu-id="9e702-160">這可以 hello hello 叢集中的其他 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="9e702-160">This can be hello other SQL Server in hello cluster.</span></span>

1. <span data-ttu-id="9e702-161">使用**sqlcmd**公用程式 tootest hello 連線。</span><span class="sxs-lookup"><span data-stu-id="9e702-161">Use **sqlcmd** utility tootest hello connection.</span></span> <span data-ttu-id="9e702-162">例如，下列指令碼的 hello 建立**sqlcmd**透過 hello 接聽程式使用 Windows 驗證連接 toohello 主要複本：</span><span class="sxs-lookup"><span data-stu-id="9e702-162">For example, hello following script establishes a **sqlcmd** connection toohello primary replica through hello listener with Windows authentication:</span></span>
   
    ```
    sqlmd -S <listenerName> -E
    ```
   
    <span data-ttu-id="9e702-163">如果 hello 接聽程式正在使用連接埠以外 hello 預設連接埠 (1433)，hello 連接字串中指定 hello 連接埠。</span><span class="sxs-lookup"><span data-stu-id="9e702-163">If hello listener is using a port other than hello default port (1433), specify hello port in hello connection string.</span></span> <span data-ttu-id="9e702-164">例如，hello 下列 sqlcmd 命令連接埠 1435 tooa 接聽程式：</span><span class="sxs-lookup"><span data-stu-id="9e702-164">For example, hello following sqlcmd command connects tooa listener at port 1435:</span></span> 
   
    ```
    sqlcmd -S <listenerName>,1435 -E
    ```

<span data-ttu-id="9e702-165">hello SQLCMD 連線自動連線 toowhichever SQL Server 裝載 hello 主要複本執行個體。</span><span class="sxs-lookup"><span data-stu-id="9e702-165">hello SQLCMD connection automatically connects toowhichever instance of SQL Server hosts hello primary replica.</span></span> 

> [!NOTE]
> <span data-ttu-id="9e702-166">請確定您指定的 hello 通訊埠的兩個 SQL 伺服器 hello 防火牆上開啟。</span><span class="sxs-lookup"><span data-stu-id="9e702-166">Make sure that hello port you specify is open on hello firewall of both SQL Servers.</span></span> <span data-ttu-id="9e702-167">這兩部伺服器所需 hello 您使用的 TCP 連接埠的輸入的規則。</span><span class="sxs-lookup"><span data-stu-id="9e702-167">Both servers require an inbound rule for hello TCP port that you use.</span></span> <span data-ttu-id="9e702-168">如需詳細資訊，請參閱 [新增或編輯防火牆規則](http://technet.microsoft.com/library/cc753558.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="9e702-168">See [Add or Edit Firewall Rule](http://technet.microsoft.com/library/cc753558.aspx) for more information.</span></span> 
> 
> 

## <a name="guidelines-and-limitations"></a><span data-ttu-id="9e702-169">指導方針和限制</span><span class="sxs-lookup"><span data-stu-id="9e702-169">Guidelines and limitations</span></span>
<span data-ttu-id="9e702-170">請注意下列指導方針，在 Azure 中使用內部負載平衡器的可用性群組接聽程式上的 hello:</span><span class="sxs-lookup"><span data-stu-id="9e702-170">Note hello following guidelines on availability group listener in Azure using internal load balancer:</span></span>

* <span data-ttu-id="9e702-171">內部負載平衡器，您只能存取從 hello 中的 hello 接聽程式相同的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="9e702-171">With an internal load balancer, you only access hello listener from within hello same virtual network.</span></span>


## <a name="for-more-information"></a><span data-ttu-id="9e702-172">取得詳細資訊</span><span class="sxs-lookup"><span data-stu-id="9e702-172">For more information</span></span>
<span data-ttu-id="9e702-173">如需詳細資訊，請參閱[在 Azure VM 中手動設定 Always On 可用性群組](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md)。</span><span class="sxs-lookup"><span data-stu-id="9e702-173">For more information, see [Configure Always On availability group in Azure VM manually](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).</span></span>

## <a name="powershell-cmdlets"></a><span data-ttu-id="9e702-174">PowerShell Cmdlet</span><span class="sxs-lookup"><span data-stu-id="9e702-174">PowerShell cmdlets</span></span>
<span data-ttu-id="9e702-175">使用下列 PowerShell cmdlet toocreate Azure 虛擬機器的內部負載平衡器的 hello。</span><span class="sxs-lookup"><span data-stu-id="9e702-175">Use hello following PowerShell cmdlets toocreate an internal load balancer for Azure virtual machines.</span></span>

* <span data-ttu-id="9e702-176">[New-AzureRmLoadBalancer](http://msdn.microsoft.com/library/mt619450.aspx) 會建立負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="9e702-176">[New-AzureRmLoadBalancer](http://msdn.microsoft.com/library/mt619450.aspx) creates a load balancer.</span></span> 
* <span data-ttu-id="9e702-177">[New-AzureRMLoadBalancerFrontendIpConfig](http://msdn.microsoft.com/library/mt603510.aspx) 會建立負載平衡器的前端 IP 組態。</span><span class="sxs-lookup"><span data-stu-id="9e702-177">[New-AzureRMLoadBalancerFrontendIpConfig](http://msdn.microsoft.com/library/mt603510.aspx) creates a front-end IP configuration for a load balancer.</span></span> 
* <span data-ttu-id="9e702-178">[New-AzureRmLoadBalancerRuleConfig](http://msdn.microsoft.com/library/mt619391.aspx) 會建立負載平衡器的規則組態。</span><span class="sxs-lookup"><span data-stu-id="9e702-178">[New-AzureRmLoadBalancerRuleConfig](http://msdn.microsoft.com/library/mt619391.aspx) creates a rule configuration for a load balancer.</span></span> 
* <span data-ttu-id="9e702-179">[New-AzureRmLoadBalancerBackendAddressPoolConfig](http://msdn.microsoft.com/library/mt603791.aspx) 會建立負載平衡器的後端位址集區組態。</span><span class="sxs-lookup"><span data-stu-id="9e702-179">[New-AzureRmLoadBalancerBackendAddressPoolConfig](http://msdn.microsoft.com/library/mt603791.aspx) creates a backend address pool configuration for a load balancer.</span></span> 
* <span data-ttu-id="9e702-180">[New-AzureRmLoadBalancerProbeConfig](http://msdn.microsoft.com/library/mt603847.aspx) 會建立負載平衡器的探查組態。</span><span class="sxs-lookup"><span data-stu-id="9e702-180">[New-AzureRmLoadBalancerProbeConfig](http://msdn.microsoft.com/library/mt603847.aspx) creates a probe configuration for a load balancer.</span></span>
* <span data-ttu-id="9e702-181">[Remove-AzureRmLoadBalancer](http://msdn.microsoft.com/library/mt603862.aspx) 會從 Azure 資源群組中移除負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="9e702-181">[Remove-AzureRmLoadBalancer](http://msdn.microsoft.com/library/mt603862.aspx) removes a load balancer from an Azure resource group.</span></span>
