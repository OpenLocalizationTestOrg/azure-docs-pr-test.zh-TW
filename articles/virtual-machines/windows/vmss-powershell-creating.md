---
title: "虛擬機器規模 aaaCreating 設定使用 PowerShell cmdlet |Microsoft 文件"
description: "使用 Azure PowerShell Cmdlet 開始建立及管理您的第一個 Azure 虛擬機器擴展集"
services: virtual-machines-windows
documentationcenter: 
author: danielsollondon
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 430d9d64-1f35-48f0-a4fd-9b69910ffa59
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/21/2017
ms.author: danielsollondon
ms.openlocfilehash: 7979be367d04c904b60d78849c1b751a52cc8caf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="creating-virtual-machine-scale-sets-using-powershell-cmdlets"></a><span data-ttu-id="e7346-103">使用 PowerShell Cmdlet 建立虛擬機器擴展集</span><span class="sxs-lookup"><span data-stu-id="e7346-103">Creating Virtual Machine Scale Sets using PowerShell cmdlets</span></span>
<span data-ttu-id="e7346-104">本文逐步解說如何 toocreate 虛擬機器規模集 (VMSS) 的範例。</span><span class="sxs-lookup"><span data-stu-id="e7346-104">This article walks through an example of how toocreate a Virtual Machine scale set (VMSS).</span></span> <span data-ttu-id="e7346-105">它會建立一個含有 3 個節點的擴展集，其中搭配關聯的「網路」和「儲存體」。</span><span class="sxs-lookup"><span data-stu-id="e7346-105">It creates a scale set of three nodes, with associated Networking and Storage.</span></span>

## <a name="first-steps"></a><span data-ttu-id="e7346-106">第一個步驟</span><span class="sxs-lookup"><span data-stu-id="e7346-106">First Steps</span></span>
<span data-ttu-id="e7346-107">請確認您擁有 hello 安裝最新 Azure PowerShell 模組，toomake 確定您擁有 hello PowerShell 指令程式所需 toomaintain，並建立規模集。</span><span class="sxs-lookup"><span data-stu-id="e7346-107">Ensure you have hello latest Azure PowerShell module installed, toomake sure you have hello PowerShell commandlets needed toomaintain, and create scale sets.</span></span>
<span data-ttu-id="e7346-108">移 toohello 命令列工具[這裡](http://aka.ms/webpi-azps)的 hello 最新可用的 Azure 模組。</span><span class="sxs-lookup"><span data-stu-id="e7346-108">Go toohello command line tools [here](http://aka.ms/webpi-azps) for hello latest available Azure Modules.</span></span>

<span data-ttu-id="e7346-109">toofind VMSS 相關指令程式，請使用 hello 搜尋字串\*VMSS\*。</span><span class="sxs-lookup"><span data-stu-id="e7346-109">toofind VMSS related commandlets, use hello search string \*VMSS\*.</span></span> <span data-ttu-id="e7346-110">例如 _gcm *vmss*_</span><span class="sxs-lookup"><span data-stu-id="e7346-110">For example, _gcm *vmss*_</span></span>

## <a name="creating-a-vmss"></a><span data-ttu-id="e7346-111">建立 VMSS</span><span class="sxs-lookup"><span data-stu-id="e7346-111">Creating a VMSS</span></span>
#### <a name="create-resource-group"></a><span data-ttu-id="e7346-112">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="e7346-112">Create Resource Group</span></span>
```
$loc = 'westus';
$rgname = 'mynewrgwu';
  New-AzureRmResourceGroup -Name $rgname -Location $loc -Force;
```

### <a name="create-networking-vnet--subnet"></a><span data-ttu-id="e7346-113">建立網路 (VNET/子網路)</span><span class="sxs-lookup"><span data-stu-id="e7346-113">Create Networking (VNET / Subnet)</span></span>
#### <a name="subnet-specification"></a><span data-ttu-id="e7346-114">子網路規格</span><span class="sxs-lookup"><span data-stu-id="e7346-114">Subnet Specification</span></span>
```
$subnetName = 'websubnet'
  $subnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix "10.0.0.0/24";
```

#### <a name="vnet-specification"></a><span data-ttu-id="e7346-115">VNET 規格</span><span class="sxs-lookup"><span data-stu-id="e7346-115">VNET Specification</span></span>
```
$vnet = New-AzureRmVirtualNetwork -Force -Name ('vnet' + $rgname) -ResourceGroupName $rgname -Location $loc -AddressPrefix "10.0.0.0/16" -Subnet $subnet;
$vnet = Get-AzureRmVirtualNetwork -Name ('vnet' + $rgname) -ResourceGroupName $rgname;

# In this case assume hello new subnet is hello only one
$subnetId = $vnet.Subnets[0].Id;
```

#### <a name="create-public-ip-resource-tooallow-external-access"></a><span data-ttu-id="e7346-116">建立公用 IP 資源 tooAllow 外部存取</span><span class="sxs-lookup"><span data-stu-id="e7346-116">Create Public IP Resource tooAllow External Access</span></span>
<span data-ttu-id="e7346-117">這會是繫結的 toohello 負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="e7346-117">This will be bound toohello Load Balancer.</span></span>

```
$pubip = New-AzureRmPublicIpAddress -Force -Name ('pubip' + $rgname) -ResourceGroupName $rgname -Location $loc -AllocationMethod Dynamic -DomainNameLabel ('pubip' + $rgname);
$pubip = Get-AzureRmPublicIpAddress -Name ('pubip' + $rgname) -ResourceGroupName $rgname;
```

#### <a name="create-load-balancer"></a><span data-ttu-id="e7346-118">建立負載平衡器</span><span class="sxs-lookup"><span data-stu-id="e7346-118">Create Load Balancer</span></span>
```
$frontendName = 'fe' + $rgname
$backendAddressPoolName = 'bepool' + $rgname
$probeName = 'vmssprobe' + $rgname
$inboundNatPoolName = 'innatpool' + $rgname
$lbruleName = 'lbrule' + $rgname
$lbName = 'vmsslb' + $rgname

# Bind Public IP tooLoad Balancer
$frontend = New-AzureRmLoadBalancerFrontendIpConfig -Name $frontendName -PublicIpAddress $pubip
```

#### <a name="configure-load-balancer"></a><span data-ttu-id="e7346-119">設定負載平衡器</span><span class="sxs-lookup"><span data-stu-id="e7346-119">Configure Load Balancer</span></span>
<span data-ttu-id="e7346-120">建立後端位址集區組態，這將會被共用 hello Nic 的 hello Vm hello 規模集中。</span><span class="sxs-lookup"><span data-stu-id="e7346-120">Create Backend Address Pool Config, this will be shared by hello NICs of hello VMs in hello scale set.</span></span>

```
$backendAddressPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name $backendAddressPoolName
```

<span data-ttu-id="e7346-121">設定負載平衡的探查連接埠，變更為適合您的應用程式的 hello 設定。</span><span class="sxs-lookup"><span data-stu-id="e7346-121">Set Load Balanced Probe Port, change hello settings as appropriate for your application.</span></span>

```
$probe = New-AzureRmLoadBalancerProbeConfig -Name $probeName -RequestPath healthcheck.aspx -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2
```

<span data-ttu-id="e7346-122">建立直接路由連線 （不負載平衡） 的輸入的 NAT 集區透過 hello 負載平衡器設定 toohello Vm 在 hello 小數位數。</span><span class="sxs-lookup"><span data-stu-id="e7346-122">Create an inbound NAT pool for direct routed connectivity (not load balanced) toohello VMs in hello scale set via hello Load Balancer.</span></span> <span data-ttu-id="e7346-123">這是使用 RDP toodemonstrate，而且您的應用程式中可能不需要。</span><span class="sxs-lookup"><span data-stu-id="e7346-123">This is toodemonstrate using RDP and may not be required in your application.</span></span>

```
$frontendpoolrangestart = 3360
$frontendpoolrangeend = 3370
$backendvmport = 3389
$inboundNatPool = New-AzureRmLoadBalancerInboundNatPoolConfig -Name $inboundNatPoolName -FrontendIPConfigurationId `
$frontend.Id -Protocol Tcp -FrontendPortRangeStart $frontendpoolrangestart -FrontendPortRangeEnd $frontendpoolrangeend -BackendPort $backendvmport;
```

<span data-ttu-id="e7346-124">建立 hello 負載平衡規則，此範例中顯示的負載平衡連接埠 80 個要求，使用先前步驟中的 hello 設定。</span><span class="sxs-lookup"><span data-stu-id="e7346-124">Create hello Load Balanced Rule, this example shows load balancing port 80 requests, using hello settings from previous steps.</span></span>

```
$protocol = 'Tcp'
$feLBPort = 80
$beLBPort = 80

$lbrule = New-AzureRmLoadBalancerRuleConfig -Name $lbruleName `
-FrontendIPConfiguration $frontend -BackendAddressPool $backendAddressPool `
-Probe $probe -Protocol $protocol -FrontendPort $feLBPort -BackendPort $beLBPort `
-IdleTimeoutInMinutes 15 -EnableFloatingIP -LoadDistribution SourceIP -Verbose;
```

<span data-ttu-id="e7346-125">以組態建立負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="e7346-125">Create Load Balancer with configuration.</span></span>

```
$actualLb = New-AzureRmLoadBalancer -Name $lbName -ResourceGroupName $rgname -Location $loc `
-FrontendIpConfiguration $frontend -BackendAddressPool $backendAddressPool `
-Probe $probe -LoadBalancingRule $lbrule -InboundNatPool $inboundNatPool -Verbose;
```

<span data-ttu-id="e7346-126">請檢查 LB 設定、 檢查負載平衡連接埠組態的雲端組態，請注意，您將不會看到直到 hello Vm hello 規模集中的輸入 NAT 規則的建立。</span><span class="sxs-lookup"><span data-stu-id="e7346-126">Check  LB settings, check load balanced port configs, note, you will not see Inbound NAT rules until hello VMs in hello scale set are created.</span></span>

```
$expectedLb = Get-AzureRmLoadBalancer -Name $lbName -ResourceGroupName $rgname
```

##### <a name="configure-and-create-hello-scale-set"></a><span data-ttu-id="e7346-127">設定並建立 hello 規模調整集合</span><span class="sxs-lookup"><span data-stu-id="e7346-127">Configure and Create hello scale set</span></span>
<span data-ttu-id="e7346-128">請注意，此基礎結構範例示範如何向上 tooset 散發和延展 web 流量 hello 規模集，但此處指定的 Vm 映像 hello 並沒有安裝任何 web 服務。</span><span class="sxs-lookup"><span data-stu-id="e7346-128">Note, this infrastructure example shows how tooset up distribute and scale web traffic across hello scale set, but hello VMs Images specified here do not have any web services installed.</span></span>

```
# specify scale set Name
$vmssName = 'vmss' + $rgname;

## specify VMSS specific details
$adminUsername = 'azadmin';
$adminPassword = "Password1234!";

$PublisherName = 'MicrosoftWindowsServer'
$Offer         = 'WindowsServer'
$Sku          = '2012-R2-Datacenter'
$Version       = 'latest'
$vmNamePrefix = 'winvmss'

###add an extension
$extname = 'BGInfo';
$publisher = 'Microsoft.Compute';
$exttype = 'BGInfo';
$extver = '2.1';
```

<span data-ttu-id="e7346-129">將 NIC tooLoad 平衡器和子網路繫結</span><span class="sxs-lookup"><span data-stu-id="e7346-129">Bind NIC tooLoad Balancer and Subnet</span></span>

```
$ipCfg = New-AzureRmVmssIPConfig -Name 'nic' `
-LoadBalancerInboundNatPoolsId $actualLb.InboundNatPools[0].Id `
-LoadBalancerBackendAddressPoolsId $actualLb.BackendAddressPools[0].Id `
-SubnetId $subnetId;
```

<span data-ttu-id="e7346-130">建立擴展集組態</span><span class="sxs-lookup"><span data-stu-id="e7346-130">Create scale set Config</span></span>

```
# Specify number of nodes
$numberofnodes = 3

$vmss = New-AzureRmVmssConfig -Location $loc -SkuCapacity $numberofnodes -SkuName 'Standard_A2' -UpgradePolicyMode 'automatic' `
    | Add-AzureRmVmssNetworkInterfaceConfiguration -Name $subnetName -Primary $true -IPConfiguration $ipCfg `
    | Set-AzureRmVmssOSProfile -ComputerNamePrefix $vmNamePrefix -AdminUsername $adminUsername -AdminPassword $adminPassword `
    | Set-AzureRmVmssStorageProfile -OsDiskCreateOption 'FromImage' -OsDiskCaching 'None' `
    -ImageReferenceOffer $Offer -ImageReferenceSku $Sku -ImageReferenceVersion $Version `
    -ImageReferencePublisher $PublisherName `
    | Add-AzureRmVmssExtension -Name $extname -Publisher $publisher -Type $exttype -TypeHandlerVersion $extver -AutoUpgradeMinorVersion $true
```

<span data-ttu-id="e7346-131">建置擴展集的組態</span><span class="sxs-lookup"><span data-stu-id="e7346-131">Build scale set configuration</span></span>

```
New-AzureRmVmss -ResourceGroupName $rgname -Name $vmssName -VirtualMachineScaleSet $vmss -Verbose;
```

<span data-ttu-id="e7346-132">現在您已建立 hello 規模集。</span><span class="sxs-lookup"><span data-stu-id="e7346-132">Now you have created hello scale set.</span></span> <span data-ttu-id="e7346-133">您可以測試連接 toohello 個別 VM 在此範例中使用 RDP:</span><span class="sxs-lookup"><span data-stu-id="e7346-133">You can test connecting toohello individual VM using RDP in this example:</span></span>

```
VM0 : pubipmynewrgwu.westus.cloudapp.azure.com:3360
VM1 : pubipmynewrgwu.westus.cloudapp.azure.com:3361
VM2 : pubipmynewrgwu.westus.cloudapp.azure.com:3362
```
