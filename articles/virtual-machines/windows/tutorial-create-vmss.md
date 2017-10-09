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
# <a name="create-a-virtual-machine-scale-set-and-deploy-a-highly-available-app-on-windows"></a>在 Windows 上建立虛擬機器擴展集及部署高可用性應用程式
虛擬機器規模集可讓您 toodeploy 和管理一組完全相同，自動調整的虛擬機器。 您可以手動調整 hello 規模集中的 Vm hello 數目，或定義規則 tooautoscale 根據 CPU 使用量、 記憶體需求或網路流量。 在本教學課程中，您將會在 Azure 部署虛擬機器擴展集。 您會了解如何：

> [!div class="checklist"]
> * 使用 hello 自訂指令碼擴充 toodefine IIS 站台 tooscale
> * 建立擴展集的負載平衡器規則
> * 建立虛擬機器擴展集
> * 增加或減少 hello 規模集中的執行個體數目
> * 建立自動調整規則

本教學課程需要 hello Azure PowerShell 模組版本 3.6 版或更新版本。 執行` Get-Module -ListAvailable AzureRM`toofind hello 版本。 如果您需要 tooupgrade，請參閱[安裝 Azure PowerShell 模組](/powershell/azure/install-azurerm-ps)。


## <a name="scale-set-overview"></a>擴展集概觀
規模集使用的概念類似，因為您了解有關在 hello 上一個教學課程中太[建立高可用性 Vm](tutorial-availability-sets.md)。 擴展集中的 VM 會分散於容錯網域和更新網域，如同可用性設定組中的 VM。

VM 會視需要建立於擴展集中。 您可以定義自動調整規模規則 toocontrol 如何及何時加入或移除從 hello 擴展集 Vm。 您可以根據計量 (例如 CPU 負載、記憶體使用量或網路流量) 觸發這些規則。

小數位數設定總 too1，000 Vm，當您使用 Azure 平台映像的支援。 重要的安裝或 VM 自訂需求的工作負載，您可能希望太[建立自訂的 VM 映像](tutorial-custom-images.md)。 您可以建立啟動 too100 Vm 擴展集時使用的自訂映像內。


## <a name="create-an-app-tooscale"></a>建立應用程式 tooscale
建立擴展集之前，請先使用 [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) 來建立資源群組。 hello 下列範例會建立名為的資源群組*myResourceGroupAutomate*在 hello *EastUS*位置：

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroupScaleSet -Location EastUS
```

在先前的教學課程，您學會如何太[自動化 VM 組態](tutorial-automate-vm-deployment.md)使用 hello 自訂指令碼擴充。 建立一個小數位數組設定，然後套用自訂指令碼擴充 tooinstall 及設定 IIS:

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

## <a name="create-scale-load-balancer"></a>建立擴展負載平衡器
Azure Load Balancer 是 Layer-4 (TCP、UDP) 負載平衡器，可將連入流量分散於狀況良好的 VM 來提供高可用性。 負載平衡器健全狀況探查監視每個 VM 上指定的連接埠，並只會發佈流量 tooan 操作的 VM。 如需詳細資訊，請參閱 hello 下一個教學課程上[tooload 如何平衡 Windows 虛擬機器](tutorial-load-balancer.md)。

建立負載平衡器，包含公用 IP 位址及並分散連接埠 80 上的網路流量︰

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

## <a name="create-a-scale-set"></a>建立擴展集
現在使用 [New-AzureRmVmss](/powershell/module/azurerm.compute/new-azurermvm) 建立虛擬機器擴展集。 hello 下列範例會建立名為小數位數*myScaleSet*:

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

它會採用幾分鐘的時間 toocreate 並設定所有 hello 小數位數設定的資源和 Vm。


## <a name="test-your-app"></a>測試應用程式
toosee 在動作中，您的 IIS 網站取得您的負載平衡器的 hello 公用 IP 位址[Get AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress)。 hello 下列範例會取得 IP 位址 hello *myPublicIP*建立 hello 規模集的一部分：

```powershell
Get-AzureRmPublicIPAddress -ResourceGroupName myResourceGroupScaleSet -Name myPublicIP | select IpAddress
```

Tooa 網頁瀏覽器中輸入 hello 公用 IP 位址。 會顯示 hello 應用程式，包括 hello 的 hello VM 該 hello 負載平衡器分散流量的主機名稱：

![執行中的 IIS 網站](./media/tutorial-create-vmss/running-iis-site.png)

在動作中設定 toosee hello 標尺，您可以強制重新整理 web 瀏覽器 toosee hello 負載平衡器會將流量分散到所有的 hello Vm 執行您的應用程式。


## <a name="management-tasks"></a>管理工作
整個 hello 規模集的 hello 生命週期，您可能需要 toorun 一或多個管理工作。 此外，您可能想將不同的生命週期工作自動化的 toocreate 指令碼。 Azure PowerShell 提供快速的方式 toodo 這些工作。 以下是一些常見工作。

### <a name="view-vms-in-a-scale-set"></a>檢視擴展集中的 VM
tooview 一份您的標尺中執行的 Vm 設定，請使用[Get AzureRmVmssVM](/powershell/module/azurerm.compute/get-azurermvmssvm) ，如下所示：

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


### <a name="increase-or-decrease-vm-instances"></a>增加或減少 VM 執行個體
執行個體 toosee hello 數目您目前有小數位數中設定，請使用[Get AzureRmVmss](/powershell/module/azurerm.compute/get-azurermvmss)及查詢上*sku.capacity*:

```powershell
Get-AzureRmVmss -ResourceGroupName myResourceGroupScaleSet `
    -VMScaleSetName myScaleSet | `
    Select -ExpandProperty Sku
```

您可以再以手動方式增加或減少 hello 擴展集內的虛擬機器的 hello 數目[更新 AzureRmVmss](/powershell/module/azurerm.compute/update-azurermvmss)。 hello 下列範例會設定 hello Vm 數目在您設定過的標尺*5*:

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

如果花費幾分鐘的時間 tooupdate hello 指定中的執行個體數目規模集。


### <a name="configure-autoscale-rules"></a>設定自動調整規則
而非手動調整您的標尺 hello 執行個體數目的設定，您會定義自動調整規模規則。 這些規則會監控的 hello 中您的標尺的執行個體設定，並回應據以根據標準和您所定義的臨界值。 下列範例中的 hello 能有效擴充 hello 執行個體數目一個 hello 平均 CPU 負載大於 60 %5 分鐘期間內。 如果 hello 平均 CPU 負載然後卸除低於 30 %5 分鐘期間內，會以某個執行個體進行縮放 hello 執行個體：

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


## <a name="next-steps"></a>後續步驟
在本教學課程中，您已建立虛擬機器擴展集。 您已了解如何︰

> [!div class="checklist"]
> * 使用 hello 自訂指令碼擴充 toodefine IIS 站台 tooscale
> * 建立擴展集的負載平衡器規則
> * 建立虛擬機器擴展集
> * 增加或減少 hello 規模集中的執行個體數目
> * 建立自動調整規則

前進 toohello 下一個教學課程 toolearn 有關負載平衡的虛擬機器概念的詳細資訊。

> [!div class="nextstepaction"]
> [平衡虛擬機器的負載](tutorial-load-balancer.md)
