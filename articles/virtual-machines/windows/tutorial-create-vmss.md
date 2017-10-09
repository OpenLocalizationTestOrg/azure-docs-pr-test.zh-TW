---
title: "虛擬機器規模集 for Windows Azure 中 aaaCreate |Microsoft 文件"
description: "在 Windows VM 上使用虛擬機器擴展集，建立及部署高可用性應用程式"
services: virtual-machine-scale-sets
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: 
ms.topic: article
ms.date: 08/11/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: a3914571005c28a492c069d880992630851afae7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-scale-set-and-deploy-a-highly-available-app-on-windows"></a><span data-ttu-id="45229-103">在 Windows 上建立虛擬機器擴展集及部署高可用性應用程式</span><span class="sxs-lookup"><span data-stu-id="45229-103">Create a Virtual Machine Scale Set and deploy a highly available app on Windows</span></span>
<span data-ttu-id="45229-104">虛擬機器規模集可讓您 toodeploy 和管理一組完全相同，自動調整的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="45229-104">A virtual machine scale set allows you toodeploy and manage a set of identical, auto-scaling virtual machines.</span></span> <span data-ttu-id="45229-105">您可以手動調整 hello 規模集中的 Vm hello 數目，或定義規則 tooautoscale 根據 CPU 使用量、 記憶體需求或網路流量。</span><span class="sxs-lookup"><span data-stu-id="45229-105">You can scale hello number of VMs in hello scale set manually, or define rules tooautoscale based on CPU usage, memory demand, or network traffic.</span></span> <span data-ttu-id="45229-106">在本教學課程中，您將會在 Azure 部署虛擬機器擴展集。</span><span class="sxs-lookup"><span data-stu-id="45229-106">In this tutorial, you deploy a virtual machine scale set in Azure.</span></span> <span data-ttu-id="45229-107">您會了解如何：</span><span class="sxs-lookup"><span data-stu-id="45229-107">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="45229-108">使用 hello 自訂指令碼擴充 toodefine IIS 站台 tooscale</span><span class="sxs-lookup"><span data-stu-id="45229-108">Use hello Custom Script Extension toodefine an IIS site tooscale</span></span>
> * <span data-ttu-id="45229-109">建立擴展集的負載平衡器規則</span><span class="sxs-lookup"><span data-stu-id="45229-109">Create a load balancer for your scale set</span></span>
> * <span data-ttu-id="45229-110">建立虛擬機器擴展集</span><span class="sxs-lookup"><span data-stu-id="45229-110">Create a virtual machine scale set</span></span>
> * <span data-ttu-id="45229-111">增加或減少 hello 規模集中的執行個體數目</span><span class="sxs-lookup"><span data-stu-id="45229-111">Increase or decrease hello number of instances in a scale set</span></span>
> * <span data-ttu-id="45229-112">建立自動調整規則</span><span class="sxs-lookup"><span data-stu-id="45229-112">Create autoscale rules</span></span>

<span data-ttu-id="45229-113">本教學課程需要 hello Azure PowerShell 模組版本 3.6 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="45229-113">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="45229-114">執行` Get-Module -ListAvailable AzureRM`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="45229-114">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="45229-115">如果您需要 tooupgrade，請參閱[安裝 Azure PowerShell 模組](/powershell/azure/install-azurerm-ps)。</span><span class="sxs-lookup"><span data-stu-id="45229-115">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>


## <a name="scale-set-overview"></a><span data-ttu-id="45229-116">擴展集概觀</span><span class="sxs-lookup"><span data-stu-id="45229-116">Scale Set overview</span></span>
<span data-ttu-id="45229-117">規模集使用的概念類似，因為您了解有關在 hello 上一個教學課程中太[建立高可用性 Vm](tutorial-availability-sets.md)。</span><span class="sxs-lookup"><span data-stu-id="45229-117">Scale sets use similar concepts as you learned about in hello previous tutorial too[Create highly available VMs](tutorial-availability-sets.md).</span></span> <span data-ttu-id="45229-118">擴展集中的 VM 會分散於容錯網域和更新網域，如同可用性設定組中的 VM。</span><span class="sxs-lookup"><span data-stu-id="45229-118">VMs in a scale set are distributed across fault and update domains just like VMs in an availability set.</span></span>

<span data-ttu-id="45229-119">VM 會視需要建立於擴展集中。</span><span class="sxs-lookup"><span data-stu-id="45229-119">VMs are created as needed in a scale set.</span></span> <span data-ttu-id="45229-120">您可以定義自動調整規模規則 toocontrol 如何及何時加入或移除從 hello 擴展集 Vm。</span><span class="sxs-lookup"><span data-stu-id="45229-120">You define autoscale rules toocontrol how and when VMs are added or removed from hello scale set.</span></span> <span data-ttu-id="45229-121">您可以根據計量 (例如 CPU 負載、記憶體使用量或網路流量) 觸發這些規則。</span><span class="sxs-lookup"><span data-stu-id="45229-121">These rules can trigger based on metrics such as CPU load, memory usage, or network traffic.</span></span>

<span data-ttu-id="45229-122">小數位數設定總 too1，000 Vm，當您使用 Azure 平台映像的支援。</span><span class="sxs-lookup"><span data-stu-id="45229-122">Scale sets support up too1,000 VMs when you use an Azure platform image.</span></span> <span data-ttu-id="45229-123">重要的安裝或 VM 自訂需求的工作負載，您可能希望太[建立自訂的 VM 映像](tutorial-custom-images.md)。</span><span class="sxs-lookup"><span data-stu-id="45229-123">For workloads with significant installation or VM customization requirements, you may wish too[Create a custom VM image](tutorial-custom-images.md).</span></span> <span data-ttu-id="45229-124">您可以建立啟動 too100 Vm 擴展集時使用的自訂映像內。</span><span class="sxs-lookup"><span data-stu-id="45229-124">You can create up too100 VMs in a scale set when using a custom image.</span></span>


## <a name="create-an-app-tooscale"></a><span data-ttu-id="45229-125">建立應用程式 tooscale</span><span class="sxs-lookup"><span data-stu-id="45229-125">Create an app tooscale</span></span>
<span data-ttu-id="45229-126">建立擴展集之前，請先使用 [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) 來建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="45229-126">Before you can create a scale set, create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="45229-127">hello 下列範例會建立名為的資源群組*myResourceGroupAutomate*在 hello *EastUS*位置：</span><span class="sxs-lookup"><span data-stu-id="45229-127">hello following example creates a resource group named *myResourceGroupAutomate* in hello *EastUS* location:</span></span>

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroupScaleSet -Location EastUS
```

<span data-ttu-id="45229-128">在先前的教學課程，您學會如何太[自動化 VM 組態](tutorial-automate-vm-deployment.md)使用 hello 自訂指令碼擴充。</span><span class="sxs-lookup"><span data-stu-id="45229-128">In an earlier tutorial, you learned how too[Automate VM configuration](tutorial-automate-vm-deployment.md) using hello Custom Script Extension.</span></span> <span data-ttu-id="45229-129">建立一個小數位數組設定，然後套用自訂指令碼擴充 tooinstall 及設定 IIS:</span><span class="sxs-lookup"><span data-stu-id="45229-129">Create a scale set configuration then apply a Custom Script Extension tooinstall and configure IIS:</span></span>

```powershell
# Create a config object
$vmssConfig = New-AzureRmVmssConfig `
    -Location EastUS `
    -SkuCapacity 2 `
    -SkuName Standard_DS2 `
    -UpgradePolicyMode Automatic

# Define hello script for your Custom Script Extension toorun
$publicSettings = @{
    "fileUris" = (,"https://raw.githubusercontent.com/iainfoulds/azure-samples/master/automate-iis.ps1");
    "commandToExecute" = "powershell -ExecutionPolicy Unrestricted -File automate-iis.ps1"
}

# Use Custom Script Extension tooinstall IIS and configure basic website
Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmssConfig `
    -Name "customScript" `
    -Publisher "Microsoft.Compute" `
    -Type "CustomScriptExtension" `
    -TypeHandlerVersion 1.8 `
    -Setting $publicSettings
```

## <a name="create-scale-load-balancer"></a><span data-ttu-id="45229-130">建立擴展負載平衡器</span><span class="sxs-lookup"><span data-stu-id="45229-130">Create scale load balancer</span></span>
<span data-ttu-id="45229-131">Azure Load Balancer 是 Layer-4 (TCP、UDP) 負載平衡器，可將連入流量分散於狀況良好的 VM 來提供高可用性。</span><span class="sxs-lookup"><span data-stu-id="45229-131">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer that provides high availability by distributing incoming traffic among healthy VMs.</span></span> <span data-ttu-id="45229-132">負載平衡器健全狀況探查監視每個 VM 上指定的連接埠，並只會發佈流量 tooan 操作的 VM。</span><span class="sxs-lookup"><span data-stu-id="45229-132">A load balancer health probe monitors a given port on each VM and only distributes traffic tooan operational VM.</span></span> <span data-ttu-id="45229-133">如需詳細資訊，請參閱 hello 下一個教學課程上[tooload 如何平衡 Windows 虛擬機器](tutorial-load-balancer.md)。</span><span class="sxs-lookup"><span data-stu-id="45229-133">For more information, see hello next tutorial on [How tooload balance Windows virtual machines](tutorial-load-balancer.md).</span></span>

<span data-ttu-id="45229-134">建立負載平衡器，包含公用 IP 位址及並分散連接埠 80 上的網路流量︰</span><span class="sxs-lookup"><span data-stu-id="45229-134">Create a load balancer that has a public IP address and distributes web traffic on port 80:</span></span>

```powershell
# Create a public IP address
$publicIP = New-AzureRmPublicIpAddress `
  -ResourceGroupName myResourceGroupScaleSet `
  -Location EastUS `
  -AllocationMethod Static `
  -Name myPublicIP

# Create a frontend and backend IP pool
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig `
  -Name myFrontEndPool `
  -PublicIpAddress $publicIP
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name myBackEndPool

# Create hello load balancer
$lb = New-AzureRmLoadBalancer `
  -ResourceGroupName myResourceGroupScaleSet `
  -Name myLoadBalancer `
  -Location EastUS `
  -FrontendIpConfiguration $frontendIP `
  -BackendAddressPool $backendPool

# Create a load balancer health probe on port 80
Add-AzureRmLoadBalancerProbeConfig -Name myHealthProbe `
  -LoadBalancer $lb `
  -Protocol tcp `
  -Port 80 `
  -IntervalInSeconds 15 `
  -ProbeCount 2

# Create a load balancer rule toodistribute traffic on port 80
Add-AzureRmLoadBalancerRuleConfig `
  -Name myLoadBalancerRule `
  -LoadBalancer $lb `
  -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
  -BackendAddressPool $lb.BackendAddressPools[0] `
  -Protocol Tcp `
  -FrontendPort 80 `
  -BackendPort 80

# Update hello load balancer configuration
Set-AzureRmLoadBalancer -LoadBalancer $lb
```

## <a name="create-a-scale-set"></a><span data-ttu-id="45229-135">建立擴展集</span><span class="sxs-lookup"><span data-stu-id="45229-135">Create a scale set</span></span>
<span data-ttu-id="45229-136">現在使用 [New-AzureRmVmss](/powershell/module/azurerm.compute/new-azurermvm) 建立虛擬機器擴展集。</span><span class="sxs-lookup"><span data-stu-id="45229-136">Now create a virtual machine scale set with [New-AzureRmVmss](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="45229-137">hello 下列範例會建立名為小數位數*myScaleSet*:</span><span class="sxs-lookup"><span data-stu-id="45229-137">hello following example creates a scale set named *myScaleSet*:</span></span>

```powershell
# Reference a virtual machine image from hello gallery
Set-AzureRmVmssStorageProfile $vmssConfig `
  -ImageReferencePublisher MicrosoftWindowsServer `
  -ImageReferenceOffer WindowsServer `
  -ImageReferenceSku 2016-Datacenter `
  -ImageReferenceVersion latest

# Set up information for authenticating with hello virtual machine
Set-AzureRmVmssOsProfile $vmssConfig `
  -AdminUsername azureuser `
  -AdminPassword P@ssword! `
  -ComputerNamePrefix myVM

# Create hello virtual network resources
$subnet = New-AzureRmVirtualNetworkSubnetConfig `
  -Name "mySubnet" `
  -AddressPrefix 10.0.0.0/24
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName "myResourceGroupScaleSet" `
  -Name "myVnet" `
  -Location "EastUS" `
  -AddressPrefix 10.0.0.0/16 `
  -Subnet $subnet
$ipConfig = New-AzureRmVmssIpConfig `
  -Name "myIPConfig" `
  -LoadBalancerBackendAddressPoolsId $lb.BackendAddressPools[0].Id `
  -SubnetId $vnet.Subnets[0].Id

# Attach hello virtual network toohello config object
Add-AzureRmVmssNetworkInterfaceConfiguration `
  -VirtualMachineScaleSet $vmssConfig `
  -Name "network-config" `
  -Primary $true `
  -IPConfiguration $ipConfig

# Create hello scale set with hello config object (this step might take a few minutes)
New-AzureRmVmss `
  -ResourceGroupName myResourceGroupScaleSet `
  -Name myScaleSet `
  -VirtualMachineScaleSet $vmssConfig
```

<span data-ttu-id="45229-138">它會採用幾分鐘的時間 toocreate 並設定所有 hello 小數位數設定的資源和 Vm。</span><span class="sxs-lookup"><span data-stu-id="45229-138">It takes a few minutes toocreate and configure all hello scale set resources and VMs.</span></span>


## <a name="test-your-app"></a><span data-ttu-id="45229-139">測試應用程式</span><span class="sxs-lookup"><span data-stu-id="45229-139">Test your app</span></span>
<span data-ttu-id="45229-140">toosee 在動作中，您的 IIS 網站取得您的負載平衡器的 hello 公用 IP 位址[Get AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress)。</span><span class="sxs-lookup"><span data-stu-id="45229-140">toosee your IIS website in action, obtain hello public IP address of your load balancer with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="45229-141">hello 下列範例會取得 IP 位址 hello *myPublicIP*建立 hello 規模集的一部分：</span><span class="sxs-lookup"><span data-stu-id="45229-141">hello following example obtains hello IP address for *myPublicIP* created as part of hello scale set:</span></span>

```powershell
Get-AzureRmPublicIPAddress -ResourceGroupName myResourceGroupScaleSet -Name myPublicIP | select IpAddress
```

<span data-ttu-id="45229-142">Tooa 網頁瀏覽器中輸入 hello 公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="45229-142">Enter hello public IP address in tooa web browser.</span></span> <span data-ttu-id="45229-143">會顯示 hello 應用程式，包括 hello 的 hello VM 該 hello 負載平衡器分散流量的主機名稱：</span><span class="sxs-lookup"><span data-stu-id="45229-143">hello app is displayed, including hello hostname of hello VM that hello load balancer distributed traffic to:</span></span>

![執行中的 IIS 網站](./media/tutorial-create-vmss/running-iis-site.png)

<span data-ttu-id="45229-145">在動作中設定 toosee hello 標尺，您可以強制重新整理 web 瀏覽器 toosee hello 負載平衡器會將流量分散到所有的 hello Vm 執行您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="45229-145">toosee hello scale set in action, you can force-refresh your web browser toosee hello load balancer distribute traffic across all hello VMs running your app.</span></span>


## <a name="management-tasks"></a><span data-ttu-id="45229-146">管理工作</span><span class="sxs-lookup"><span data-stu-id="45229-146">Management tasks</span></span>
<span data-ttu-id="45229-147">整個 hello 規模集的 hello 生命週期，您可能需要 toorun 一或多個管理工作。</span><span class="sxs-lookup"><span data-stu-id="45229-147">Throughout hello lifecycle of hello scale set, you may need toorun one or more management tasks.</span></span> <span data-ttu-id="45229-148">此外，您可能想將不同的生命週期工作自動化的 toocreate 指令碼。</span><span class="sxs-lookup"><span data-stu-id="45229-148">Additionally, you may want toocreate scripts that automate various lifecycle-tasks.</span></span> <span data-ttu-id="45229-149">Azure PowerShell 提供快速的方式 toodo 這些工作。</span><span class="sxs-lookup"><span data-stu-id="45229-149">Azure PowerShell provides a quick way toodo those tasks.</span></span> <span data-ttu-id="45229-150">以下是一些常見工作。</span><span class="sxs-lookup"><span data-stu-id="45229-150">Here are a few common tasks.</span></span>

### <a name="view-vms-in-a-scale-set"></a><span data-ttu-id="45229-151">檢視擴展集中的 VM</span><span class="sxs-lookup"><span data-stu-id="45229-151">View VMs in a scale set</span></span>
<span data-ttu-id="45229-152">tooview 一份您的標尺中執行的 Vm 設定，請使用[Get AzureRmVmssVM](/powershell/module/azurerm.compute/get-azurermvmssvm) ，如下所示：</span><span class="sxs-lookup"><span data-stu-id="45229-152">tooview a list of VMs running in your scale set, use [Get-AzureRmVmssVM](/powershell/module/azurerm.compute/get-azurermvmssvm) as follows:</span></span>

```powershell
# Get current scale set
$scaleset = Get-AzureRmVmss `
  -ResourceGroupName myResourceGroupScaleSet `
  -VMScaleSetName myScaleSet

# Loop through hello instanaces in your scale set
for ($i=1; $i -le ($scaleset.Sku.Capacity - 1); $i++) {
    Get-AzureRmVmssVM -ResourceGroupName myResourceGroupScaleSet `
      -VMScaleSetName myScaleSet `
      -InstanceId $i
}
```


### <a name="increase-or-decrease-vm-instances"></a><span data-ttu-id="45229-153">增加或減少 VM 執行個體</span><span class="sxs-lookup"><span data-stu-id="45229-153">Increase or decrease VM instances</span></span>
<span data-ttu-id="45229-154">執行個體 toosee hello 數目您目前有小數位數中設定，請使用[Get AzureRmVmss](/powershell/module/azurerm.compute/get-azurermvmss)及查詢上*sku.capacity*:</span><span class="sxs-lookup"><span data-stu-id="45229-154">toosee hello number of instances you currently have in a scale set, use [Get-AzureRmVmss](/powershell/module/azurerm.compute/get-azurermvmss) and query on *sku.capacity*:</span></span>

```powershell
Get-AzureRmVmss -ResourceGroupName myResourceGroupScaleSet `
    -VMScaleSetName myScaleSet | `
    Select -ExpandProperty Sku
```

<span data-ttu-id="45229-155">您可以再以手動方式增加或減少 hello 擴展集內的虛擬機器的 hello 數目[更新 AzureRmVmss](/powershell/module/azurerm.compute/update-azurermvmss)。</span><span class="sxs-lookup"><span data-stu-id="45229-155">You can then manually increase or decrease hello number of virtual machines in hello scale set with [Update-AzureRmVmss](/powershell/module/azurerm.compute/update-azurermvmss).</span></span> <span data-ttu-id="45229-156">hello 下列範例會設定 hello Vm 數目在您設定過的標尺*5*:</span><span class="sxs-lookup"><span data-stu-id="45229-156">hello following example sets hello number of VMs in your scale set too*5*:</span></span>

```powershell
# Get current scale set
$scaleset = Get-AzureRmVmss `
  -ResourceGroupName myResourceGroupScaleSet `
  -VMScaleSetName myScaleSet

# Set and update hello capacity of your scale set
$scaleset.sku.capacity = 5
Update-AzureRmVmss -ResourceGroupName myResourceGroupScaleSet `
    -Name myScaleSet `
    -VirtualMachineScaleSet $scaleset
```

<span data-ttu-id="45229-157">如果花費幾分鐘的時間 tooupdate hello 指定中的執行個體數目規模集。</span><span class="sxs-lookup"><span data-stu-id="45229-157">If takes a few minutes tooupdate hello specified number of instances in your scale set.</span></span>


### <a name="configure-autoscale-rules"></a><span data-ttu-id="45229-158">設定自動調整規則</span><span class="sxs-lookup"><span data-stu-id="45229-158">Configure autoscale rules</span></span>
<span data-ttu-id="45229-159">而非手動調整您的標尺 hello 執行個體數目的設定，您會定義自動調整規模規則。</span><span class="sxs-lookup"><span data-stu-id="45229-159">Rather than manually scaling hello number of instances in your scale set, you define autoscale rules.</span></span> <span data-ttu-id="45229-160">這些規則會監控的 hello 中您的標尺的執行個體設定，並回應據以根據標準和您所定義的臨界值。</span><span class="sxs-lookup"><span data-stu-id="45229-160">These rules monitor hello instances in your scale set and respond accordingly based on metrics and thresholds you define.</span></span> <span data-ttu-id="45229-161">下列範例中的 hello 能有效擴充 hello 執行個體數目一個 hello 平均 CPU 負載大於 60 %5 分鐘期間內。</span><span class="sxs-lookup"><span data-stu-id="45229-161">hello following example scales out hello number of instances by one when hello average CPU load is greater than 60% over a 5 minute period.</span></span> <span data-ttu-id="45229-162">如果 hello 平均 CPU 負載然後卸除低於 30 %5 分鐘期間內，會以某個執行個體進行縮放 hello 執行個體：</span><span class="sxs-lookup"><span data-stu-id="45229-162">If hello average CPU load then drops below 30% over a 5 minute period, hello instances are scaled in by one instance:</span></span>

```powershell
# Define your scale set information
$mySubscriptionId = (Get-AzureRmSubscription).Id
$myResourceGroup = "myResourceGroupScaleSet"
$myScaleSet = "myScaleSet"
$myLocation = "East US"

# Create a scale up rule tooincrease hello number instances after 60% average CPU usage exceeded for a 5 minute period
$myRuleScaleUp = New-AzureRmAutoscaleRule `
  -MetricName "Percentage CPU" `
  -MetricResourceId /subscriptions/$mySubscriptionId/resourceGroups/$myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/$myScaleSet `
  -Operator GreaterThan `
  -MetricStatistic Average `
  -Threshold 60 `
  -TimeGrain 00:01:00 `
  -TimeWindow 00:05:00 `
  -ScaleActionCooldown 00:05:00 `
  -ScaleActionDirection Increase `
  -ScaleActionValue 1

# Create a scale down rule toodecrease hello number of instances after 30% average CPU usage over a 5 minute period
$myRuleScaleDown = New-AzureRmAutoscaleRule `
  -MetricName "Percentage CPU" `
  -MetricResourceId /subscriptions/$mySubscriptionId/resourceGroups/$myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/$myScaleSet `
  -Operator LessThan `
  -MetricStatistic Average `
  -Threshold 30 `
  -TimeGrain 00:01:00 `
  -TimeWindow 00:05:00 `
  -ScaleActionCooldown 00:05:00 `
  -ScaleActionDirection Decrease `
  -ScaleActionValue 1

# Create a scale profile with your scale up and scale down rules
$myScaleProfile = New-AzureRmAutoscaleProfile `
  -DefaultCapacity 2  `
  -MaximumCapacity 10 `
  -MinimumCapacity 2 `
  -Rules $myRuleScaleUp,$myRuleScaleDown `
  -Name "autoprofile"

# Apply hello autoscale rules
Add-AzureRmAutoscaleSetting `
  -Location $myLocation `
  -Name "autosetting" `
  -ResourceGroup $myResourceGroup `
  -TargetResourceId /subscriptions/$mySubscriptionId/resourceGroups/$myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/$myScaleSet `
  -AutoscaleProfiles $myScaleProfile
```


## <a name="next-steps"></a><span data-ttu-id="45229-163">後續步驟</span><span class="sxs-lookup"><span data-stu-id="45229-163">Next steps</span></span>
<span data-ttu-id="45229-164">在本教學課程中，您已建立虛擬機器擴展集。</span><span class="sxs-lookup"><span data-stu-id="45229-164">In this tutorial, you created a virtual machine scale set.</span></span> <span data-ttu-id="45229-165">您已了解如何︰</span><span class="sxs-lookup"><span data-stu-id="45229-165">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="45229-166">使用 hello 自訂指令碼擴充 toodefine IIS 站台 tooscale</span><span class="sxs-lookup"><span data-stu-id="45229-166">Use hello Custom Script Extension toodefine an IIS site tooscale</span></span>
> * <span data-ttu-id="45229-167">建立擴展集的負載平衡器規則</span><span class="sxs-lookup"><span data-stu-id="45229-167">Create a load balancer for your scale set</span></span>
> * <span data-ttu-id="45229-168">建立虛擬機器擴展集</span><span class="sxs-lookup"><span data-stu-id="45229-168">Create a virtual machine scale set</span></span>
> * <span data-ttu-id="45229-169">增加或減少 hello 規模集中的執行個體數目</span><span class="sxs-lookup"><span data-stu-id="45229-169">Increase or decrease hello number of instances in a scale set</span></span>
> * <span data-ttu-id="45229-170">建立自動調整規則</span><span class="sxs-lookup"><span data-stu-id="45229-170">Create autoscale rules</span></span>

<span data-ttu-id="45229-171">前進 toohello 下一個教學課程 toolearn 有關負載平衡的虛擬機器概念的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="45229-171">Advance toohello next tutorial toolearn more about load balancing concepts for virtual machines.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="45229-172">平衡虛擬機器的負載</span><span class="sxs-lookup"><span data-stu-id="45229-172">Load balance virtual machines</span></span>](tutorial-load-balancer.md)
