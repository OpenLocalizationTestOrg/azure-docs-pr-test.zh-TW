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
# <a name="how-tooload-balance-windows-virtual-machines-in-azure-toocreate-a-highly-available-application"></a>如何 tooload 會平衡 Azure toocreate 中的 Windows 虛擬機器的高可用性的應用程式
負載平衡會將傳入要求分散到多部虛擬機器，藉此提供高可用性。 在本教學課程中，您會了解 hello 的不同元件 hello Azure 負載平衡器會將流量，以及提供高可用性。 您會了解如何：

> [!div class="checklist"]
> * 建立 Azure Load Balancer
> * 建立負載平衡器健全狀況探查
> * 建立負載平衡器流量規則
> * 使用 hello 自訂指令碼擴充 toocreate 基本的 IIS 站台
> * 建立虛擬機器，並附加 tooa 負載平衡器
> * 檢視作用中的負載平衡器
> * 新增和移除虛擬機器的負載平衡器

本教學課程需要 hello Azure PowerShell 模組版本 3.6 版或更新版本。 執行` Get-Module -ListAvailable AzureRM`toofind hello 版本。 如果您需要 tooupgrade，請參閱[安裝 Azure PowerShell 模組](/powershell/azure/install-azurerm-ps)。


## <a name="azure-load-balancer-overview"></a>Azure Load Balancer 概觀
Azure Load Balancer 是 Layer-4 (TCP、UDP) 負載平衡器，可將連入流量分散於狀況良好的 VM 來提供高可用性。 負載平衡器健全狀況探查監視每個 VM 上指定的連接埠，並只會發佈流量 tooan 操作的 VM。

您可定義含有一或多個公用 IP 位址的前端 IP 組態。 此前端 IP 組態可讓您的負載平衡器和應用程式 toobe 存取透過 hello 網際網路。 

虛擬機器連接 tooa 負載平衡器使用他們的虛擬網路介面卡 (NIC)。 toodistribute 流量 toohello Vm 後, 端位址集區包含 hello hello 虛擬 (Nic) 連線的 toohello 負載平衡器的 IP 位址。

toocontrol hello 流量的流量，您會定義特定連接埠和通訊協定對應 tooyour Vm 的負載平衡器規則。


## <a name="create-azure-load-balancer"></a>建立 Azure Load Balancer
本節將詳細說明如何建立及設定 hello 負載平衡器的每個元件。 請先使用 [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) 來建立資源群組，才可建立負載平衡器。 hello 下列範例會建立名為的資源群組*myResourceGroupLoadBalancer*在 hello *EastUS*位置：

```powershell
New-AzureRmResourceGroup `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS
```

### <a name="create-a-public-ip-address"></a>建立公用 IP 位址
tooaccess 上的應用程式 hello 網際網路，您就需要公用 IP 位址 hello 負載平衡器。 使用 [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) 建立公用 IP 位址。 hello 下列範例會建立名為的公用 IP 位址*myPublicIP*在 hello *myResourceGroupLoadBalancer*資源群組：

```powershell
$publicIP = New-AzureRmPublicIpAddress `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS `
  -AllocationMethod Static `
  -Name myPublicIP
```

### <a name="create-a-load-balancer"></a>建立負載平衡器
使用 [New-AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig) 建立前端 IP 位址。 hello 下列範例會建立名為的前端 IP 位址*myFrontEndPool*: 

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig `
  -Name myFrontEndPool `
  -PublicIpAddress $publicIP
```

使用 [New-AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig) 建立後端位址集區。 hello 下列範例會建立名為後端位址集區*myBackEndPool*:

```powershell
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name myBackEndPool
```

現在，建立 hello 的負載平衡器[新增 AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer)。 hello 下列範例會建立名為負載平衡器*myLoadBalancer*使用 hello *myPublicIP*位址：

```powershell
$lb = New-AzureRmLoadBalancer `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myLoadBalancer `
  -Location EastUS `
  -FrontendIpConfiguration $frontendIP `
  -BackendAddressPool $backendPool
```

### <a name="create-a-health-probe"></a>建立健康狀態探查
tooallow hello 負載平衡器 toomonitor hello 狀態的應用程式，您可以使用健全狀況探查。 hello 健全狀況探查以動態方式加入或移除 hello 負載平衡器輪替根據其回應 toohealth 檢查 Vm。 根據預設，VM 會移除從 15 秒的間隔的兩個連續多次失敗後的 hello 負載平衡器發佈。 您可根據通訊協定或您應用程式的特定健康狀態檢查頁面，建立健康狀態探查。 

hello 下列範例會建立 TCP 探查。 您也可以建立自訂 HTTP 探查，以進行更精細的健康狀態檢查。 時使用自訂的 HTTP 探查，您必須建立 hello 健康情況檢查 頁面上，例如*healthcheck.aspx*。 必須傳回 hello 探查**HTTP 200 「 確定**回應 hello 負載平衡器 tookeep hello 中主機的旋轉。

您使用 toocreate TCP 健全狀況探查，[新增 AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig)。 hello 下列範例會建立名為健全狀況探查*myHealthProbe* ，監視每個 VM:

```powershell
Add-AzureRmLoadBalancerProbeConfig `
  -Name myHealthProbe `
  -LoadBalancer $lb `
  -Protocol tcp `
  -Port 80 `
  -IntervalInSeconds 15 `
  -ProbeCount 2
```

更新與 hello 負載平衡器[組 AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```

### <a name="create-a-load-balancer-rule"></a>建立負載平衡器規則
負載平衡器規則是使用的 toodefine 流量的分散式的 toohello Vm 的方式。 您定義 hello 連入流量和 hello 後端 IP 集區 tooreceive hello 流量，以及 hello 必要的來源和目的地連接埠 hello 前端 IP 組態。 toomake 確定只有狀況良好的 Vm 接收流量，您也定義 hello 健全狀況探查 toouse。

使用 [Add-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig) 建立負載平衡器規則。 hello 下列範例會建立名為的負載平衡器規則*myLoadBalancerRule*平衡連接埠上的流量和*80*:

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

更新與 hello 負載平衡器[組 AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```


## <a name="configure-virtual-network"></a>設定虛擬網路
您將一些 Vm 部署，並可以測試您平衡器之前，先建立 hello 支援的虛擬網路資源。 如需有關虛擬網路的詳細資訊，請參閱 hello[管理 Azure 虛擬網路](tutorial-virtual-network.md)教學課程。

### <a name="create-network-resources"></a>建立網路資源
使用 [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) 建立虛擬網路。 hello 下列範例會建立虛擬網路，名為*myVnet*與*mySubnet*:

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

使用 [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) 建立網路安全性群組規則，然後使用 [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) 建立網路安全性群組。 新增 hello 安全性群組 toohello 子網路與[組 AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig)然後再更新 hello 虛擬網路與[組 AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork)。 

hello 下列範例會建立網路安全性群組規則命名為*myNetworkSecurityGroup*並將其套用太*mySubnet*:

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

使用 [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) 建立虛擬 NIC。 hello 下列範例會建立三個虛擬 Nic。 （每個 VM 的虛擬 NIC 建立 hello 下列中的應用程式的步驟）。 您可以隨時建立其他虛擬 Nic 和 Vm，並將它們加入 toohello 負載平衡器：

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

## <a name="create-virtual-machines"></a>建立虛擬機器
tooimprove hello 高可用性的應用程式會將您的 Vm 放在可用性設定組。

使用 [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset) 建立可用性設定組。 hello 下列範例會建立可用性設定組具名*myAvailabilitySet*:

```powershell
$availabilitySet = New-AzureRmAvailabilitySet `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myAvailabilitySet `
  -Location EastUS `
  -Managed `
  -PlatformFaultDomainCount 3 `
  -PlatformUpdateDomainCount 2
```

設定系統管理員使用者名稱和密碼具有 hello Vm [Get-credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):

```powershell
$cred = Get-Credential
```

現在您可以建立與 hello Vm[新增 AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm)。 hello 下列範例會建立三個 Vm:

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

它會採用幾分鐘的時間 toocreate 並設定所有三個 Vm。

### <a name="install-iis-with-custom-script-extension"></a>安裝 IIS 與自訂指令碼擴充功能
在上一個教學課程中，在[如何 toocustomize Windows 虛擬機器](tutorial-automate-vm-deployment.md)，您學到如何與 tooautomate VM 自訂 hello 自訂指令碼延伸的視窗。 您可以使用 hello 相同 tooinstall 會很接近，且您的 Vm 上設定 IIS。

使用[組 AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall hello 自訂指令碼擴充。 hello 延伸模組執行`powershell Add-WindowsFeature Web-Server`tooinstall hello IIS 網頁伺服器，然後再更新 hello *Default.htm*頁面 tooshow hello 主機名稱的 hello VM:

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

## <a name="test-load-balancer"></a>測試負載平衡器
取得您的負載平衡器的 hello 公用 IP 位址[Get AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress)。 hello 下列範例會取得 IP 位址 hello *myPublicIP*稍早建立：

```powershell
Get-AzureRmPublicIPAddress `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myPublicIP | select IpAddress
```

然後，您就可以 tooa 網頁瀏覽器中輸入 hello 公用 IP 位址。 hello 網站將會顯示，包括 hello hello VM 主機名稱的 hello 負載平衡器分散流量 tooas hello 下列範例中：

![執行中的 IIS 網站](./media/tutorial-load-balancer/running-iis-website.png)

toosee hello 負載平衡器會將流量分散到執行您的應用程式的所有三個 Vm，您可以強制重新整理您的 web 瀏覽器。


## <a name="add-and-remove-vms"></a>新增和移除 VM
您可能需要 tooperform hello 執行您的應用程式，例如安裝作業系統更新的 Vm 上的維護。 toodeal 使用增加的流量 tooyour 應用程式，您可能需要 tooadd 其他 Vm。 這個區段會顯示如何 tooremove 或加入 VM 從 hello 負載平衡器。

### <a name="remove-a-vm-from-hello-load-balancer"></a>從 hello 負載平衡器移除 VM
取得與 hello 網路介面卡[Get AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface)，然後設定 hello*了 LoadBalancerBackendAddressPools*屬性太 hello 虛擬 NIC*$null*。 最後，更新虛擬 nic。 hello:

```powershell
$nic = Get-AzureRmNetworkInterface `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Name myNic2
$nic.Ipconfigurations[0].LoadBalancerBackendAddressPools=$null
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

toosee hello 負載平衡器會將流量分散到 hello 剩餘的兩個 Vm 執行您的應用程式您可以強制重新整理您的 web 瀏覽器。 您現在可以在 hello VM，如安裝作業系統更新，或執行 VM 重新啟動電腦上執行維護。

### <a name="add-a-vm-toohello-load-balancer"></a>新增 VM toohello 負載平衡器
之後，請執行 VM 維護，或如果您需要 tooexpand 產能，設定 hello*了 LoadBalancerBackendAddressPools* hello 虛擬 NIC toohello 屬性*BackendAddressPool*從[Get AzureRMLoadBalancer](/powershell/module/azurerm.network/get-azurermloadbalancer):

收到 hello 負載平衡器：

```powershell
$lb = Get-AzureRMLoadBalancer `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Name myLoadBalancer 
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$lb.BackendAddressPools[0]
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

## <a name="next-steps"></a>後續步驟

在本教學課程中，您可以建立負載平衡器，並附加 Vm tooit。 您已了解如何︰

> [!div class="checklist"]
> * 建立 Azure Load Balancer
> * 建立負載平衡器健全狀況探查
> * 建立負載平衡器流量規則
> * 使用 hello 自訂指令碼擴充 toocreate 基本的 IIS 站台
> * 建立虛擬機器，並附加 tooa 負載平衡器
> * 檢視作用中的負載平衡器
> * 新增和移除虛擬機器的負載平衡器

如何前進 toohello 下一個教學課程 toolearn toomanage VM 網路。

> [!div class="nextstepaction"]
> [管理 VM 和虛擬網路](./tutorial-virtual-network.md)
