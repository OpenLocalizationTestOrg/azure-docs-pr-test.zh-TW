---
title: "aaaTutorial-建置 Azure Vm 上的高可用性應用程式 |Microsoft 文件"
description: "深入了解如何 toocreate 與負載平衡器，在 Azure 中的三個 Windows Vm 之間的高度可用且安全的應用程式"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 03/30/2017
ms.author: davidmu
ms.openlocfilehash: f9eff96be4f3999651c4108f0334e4eaa1a39c0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-load-balanced-highly-available-application-on-windows-virtual-machines-in-azure"></a>在 Azure 中的 Windows 虛擬機器上，建置已負載平衡的高可用性應用程式

在本教學課程中，您可以建立具有恢復功能 toomaintenance 事件的高可用性應用程式。 hello 應用程式使用負載平衡器、 可用性設定組和三個 Windows 虛擬機器 (Vm)。 本教學課程會安裝 IIS，但您可以使用不同的應用程式架構，使用此教學課程 toodeploy hello 相同的高可用性元件和指導方針。 

## <a name="step-1---azure-prerequisites"></a>步驟 1 - Azure 必要條件

toocomplete 本教學課程，請確定您有最新安裝 hello [Azure PowerShell](/powershell/azure/overview)模組。

首先，登入 tooyour hello 登入 AzureRmAccount 命令與 Azure 訂用帳戶，並遵循螢幕上指示 hello。

```powershell
Login-AzureRmAccount
```

Azure 資源群組是在其中部署與管理 Azure 資源的邏輯容器。 您可以建立其他的 Azure 資源之前，您需要 toocreate 的資源群組與[新增 AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup)。 hello 下列範例會建立名為的資源群組`myResourceGroup`在 hello`westeurope`區域： 

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroup -Location westeurope
```

## <a name="step-2---create-availability-set"></a>步驟 2 - 建立可用性設定組

可以跨越邏輯容錯和更新網域建立虛擬機器。 每個邏輯網域代表 hello 基礎的 Azure 資料中心內的硬體的一部分。 當您建立兩部或多部 VM 時，您的計算和儲存體資源會分散於這些網域。 如果硬體元件需要維護，此分佈會維護應用程式的 hello 可用性。 可用性設定組可讓您定義這些邏輯容錯和更新網域。

使用 [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset) 建立可用性設定組。 hello 下列範例會建立可用性設定組具名`myAvailabilitySet`:

```powershell
$availabilitySet = New-AzureRmAvailabilitySet `
  -ResourceGroupName myResourceGroup `
  -Name myAvailabilitySet `
  -Location westeurope `
  -Managed `
  -PlatformFaultDomainCount 3 `
  -PlatformUpdateDomainCount 2
```

## <a name="step-3---create-load-balancer"></a>步驟 3 - 建立負載平衡器

Azure Load Balancer 會使用負載平衡器規則，將流量分散於一組定義的 VM。 健全狀況探查監視每個 VM 上指定的連接埠，並只會發佈流量 tooan 操作的 VM。

### <a name="create-public-ip-address"></a>建立公用 IP 位址

tooaccess hello 網際網路上的應用程式指派的公用 IP 位址 toohello 負載平衡器。 使用 [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) 建立公用 IP 位址。 hello 下列範例會建立名為的公用 IP 位址`myPublicIP`:

```powershell
$pip = New-AzureRmPublicIpAddress `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -AllocationMethod Static `
  -Name myPublicIP
```

### <a name="create-load-balancer"></a>建立負載平衡器

使用 [New-AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig) 建立前端 IP 位址。 hello 下列範例會建立名為的前端 IP 位址`myFrontEndPool`: 

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name myFrontEndPool -PublicIpAddress $pip
```

使用 [New-AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig) 建立後端位址集區。 hello 下列範例會建立名為後端位址集區`myBackEndPool`:

```powershell
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name myBackEndPool
```

現在，建立 hello 的負載平衡器[新增 AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer)。 hello 下列範例會建立名為負載平衡器`myLoadBalancer`使用 hello`myPublicIP`位址：

```powershell
$lb = New-AzureRmLoadBalancer `
  -ResourceGroupName myResourceGroup `
  -Name myLoadBalancer `
  -Location westeurope `
  -FrontendIpConfiguration $frontendIP `
  -BackendAddressPool $backendPool
```

### <a name="create-health-probe"></a>建立健全狀況探查

tooallow hello 負載平衡器 toomonitor hello 狀態的應用程式，您可以使用健全狀況探查。 hello 健全狀況探查以動態方式加入或移除 hello 負載平衡器輪替根據其回應 toohealth 檢查 Vm。 根據預設，VM 會移除從 15 秒的間隔的兩個連續多次失敗後的 hello 負載平衡器發佈。

使用 [Add-AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig) 建立健全狀況探查。 hello 下列範例會建立名為健全狀況探查`myHealthProbe`，監視每個 VM:

```powershell
Add-AzureRmLoadBalancerProbeConfig -Name myHealthProbe `
  -LoadBalancer $lb `
  -Protocol tcp `
  -Port 80 `
  -IntervalInSeconds 15 `
  -ProbeCount 2
```

### <a name="create-load-balancer-rule"></a>建立負載平衡器規則

負載平衡器規則是使用的 toodefine 流量的分散式的 toohello Vm 的方式。

使用 [Add-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig) 建立負載平衡器規則。 hello 下列範例會建立名為的負載平衡器規則`myLoadBalancerRule`平衡連接埠上的流量和`80`:

```powershell
Add-AzureRmLoadBalancerRuleConfig -Name myLoadBalancerRule `
  -LoadBalancer $lb `
  -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
  -BackendAddressPool $lb.BackendAddressPools[0] `
  -Protocol Tcp `
  -FrontendPort 80 `
  -BackendPort 80
```

更新與 hello 負載平衡器[組 AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```

## <a name="step-4---configure-networking"></a>步驟 4 - 設定網路功能

每個 VM 有一或多個虛擬網路介面卡 (Nic) 的 tooa 虛擬網路連線。 此虛擬網路被保護 toofilter 定義的存取規則為基礎的流量。

### <a name="create-virtual-network"></a>建立虛擬網路

首先，使用 [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) 設定子網路。 hello 下列範例會建立名為的子網路`mySubnet`:

```powershell
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name mySubnet -AddressPrefix 192.168.1.0/24
```

tooprovide 網路連線 tooyour Vm，建立虛擬網路與[新增 AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork)。 hello 下列範例會建立虛擬網路，名為`myVnet`與`mySubnet`:

```powershell
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -Name myVnet `
  -AddressPrefix 192.168.0.0/16 `
  -Subnet $subnetConfig
```

### <a name="configure-network-security"></a>設定網路安全性

Azure [網路安全性群組](../../virtual-network/virtual-networks-nsg.md) (NSG) 控制一或多部虛擬機器的輸入和傳出流量。 網路安全性群組規則可允許或拒絕特定連接埠或連接埠範圍上的網路流量。 這些規則也可以包含來源位址首碼，所以只有在預先定義的來源產生的流量可以與虛擬機器通訊。

tooallow web 流量 tooreach 您的應用程式，請建立網路安全性群組規則與[新增 AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig)。 hello 下列範例會建立網路安全性群組規則命名為`myNetworkSecurityGroupRule`:

```powershell
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
```

使用 [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) 建立網路安全性群組。 hello 下列範例會建立名為 NSG `myNetworkSecurityGroup`:

```powershell
$nsg = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -Name myNetworkSecurityGroup `
  -SecurityRules $nsgRule
```

新增 hello 安全性群組 toohello 子網路與[組 AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig):

```powershell
Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet `
  -Name mySubnet `
  -NetworkSecurityGroup $nsg `
  -AddressPrefix 192.168.1.0/24
```

更新 hello 虛擬網路與[組 AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork):

```powershell
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```

### <a name="create-virtual-network-interface-cards"></a>建立虛擬網路介面卡

負載平衡器函式與 hello 虛擬 NIC 資源，而不是 hello 實際的 VM。 hello 虛擬 NIC 連線的 toohello 的負載平衡，然後附加 tooa VM。

使用 [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) 建立虛擬 NIC。 hello 下列範例會建立三個虛擬 Nic。 （每個 VM 的虛擬 NIC 建立 hello 下列中的應用程式的步驟）：


```powershell
for ($i=1; $i -le 3; $i++)
{
   New-AzureRmNetworkInterface -ResourceGroupName myResourceGroup `
     -Name myNic$i `
     -Location westeurope `
     -Subnet $vnet.Subnets[0] `
     -LoadBalancerBackendAddressPool $lb.BackendAddressPools[0]
}

```

## <a name="step-5---create-virtual-machines"></a>步驟 5 - 建立虛擬機器

以所有 hello 基礎就地元件，您現在可以建立高可用性 Vm toorun 您的應用程式。 

取得 hello 使用者名稱和密碼所需的 hello 與 hello 虛擬機器上的系統管理員帳戶[Get-credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):

```powershell
$cred = Get-Credential
```

建立與 hello Vm[新增 AzureRmVMConfig](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/new-azurermvmconfig)，[組 AzureRmVMOperatingSystem](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmoperatingsystem)，[組 AzureRmVMSourceImage](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmsourceimage)，[組 AzureRmVMOSDisk](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmosdisk)，[新增 AzureRmVMNetworkInterface](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/add-azurermvmnetworkinterface)，和[新 AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm)。 hello 下列範例會建立三個 Vm:

```powershell
for ($i=1; $i -le 3; $i++)
{
   $vm = New-AzureRmVMConfig -VMName myVM$i -VMSize Standard_D1 -AvailabilitySetId $availabilitySet.Id
   $vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName myVM$i -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
   $vm = Set-AzureRmVMSourceImage -VM $vm -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2016-Datacenter -Version latest
   $vm = Set-AzureRmVMOSDisk -VM $vm -Name myOsDisk$i -StorageAccountType StandardLRS -DiskSizeInGB 128 -CreateOption FromImage -Caching ReadWrite
   $nic = Get-AzureRmNetworkInterface -ResourceGroupName myResourceGroup -Name myNic$i
   $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
   New-AzureRmVM -ResourceGroupName myResourceGroup -Location westeurope -VM $vm
}

```

它會採用數個分鐘 toocreate 並設定所有三個 Vm。 hello 負載平衡器健全狀況探查會自動偵測 hello 應用程式在每個 VM 上執行。 一旦 hello 應用程式正在執行，hello 負載平衡器規則會啟動 toodistribute 流量。

### <a name="install-hello-app"></a>安裝 hello 應用程式 

Azure 虛擬機器擴充功能是使用的 tooautomate 虛擬機器組態工作，例如安裝應用程式和設定 hello 作業系統。 hello[適用於 Windows 的自訂指令碼延伸](./../virtual-machines-windows-extensions-customscript.md)是使用的 toorun hello 虛擬機器上的任何 PowerShell 指令碼。 hello 指令碼可以儲存在 Azure 儲存體，任何可存取的 HTTP 端點，或內嵌在 hello 自訂指令碼延伸模組組態。 當使用 hello 自訂指令碼延伸模組，hello Azure VM 代理程式管理 hello 指令碼執行。

使用[組 AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall hello 自訂指令碼延伸。 hello 延伸模組執行`powershell Add-WindowsFeature Web-Server`tooinstall hello IIS web 伺服器：

```powershell
for ($i=1; $i -le 3; $i++)
{
   Set-AzureRmVMExtension -ResourceGroupName myResourceGroup `
     -ExtensionName IIS `
     -VMName myVM$i `
     -Publisher Microsoft.Compute `
     -ExtensionType CustomScriptExtension `
     -TypeHandlerVersion 1.4 `
     -SettingString '{"commandToExecute":"powershell Add-WindowsFeature Web-Server"}' `
     -Location westeurope
}
```

### <a name="test-your-app"></a>測試應用程式

取得您的負載平衡器的 hello 公用 IP 位址[Get AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress)。 hello 下列範例會取得 IP 位址 hello`myPublicIP`稍早建立：

```powershell
Get-AzureRmPublicIPAddress -ResourceGroupName myResourceGroup -Name myPublicIP | select IpAddress
```

Tooa 網頁瀏覽器中輸入 hello 公用 IP 位址。 與就地 hello NSG 規則，會顯示 hello 預設 IIS 網站。 

![IIS 預設網站](media/load-balanced-iis-tutorial/iis.png)

## <a name="step-6--management-tasks"></a>步驟 6 - 管理工作

您可能需要 tooperform hello 執行您的應用程式，例如安裝作業系統更新的 Vm 上的維護。 toodeal 使用增加的流量 tooyour 應用程式，您可能需要 tooadd 其他 Vm。 這個區段會顯示如何 tooremove 或加入 VM 從 hello 負載平衡器。 

### <a name="remove-a-vm-from-hello-load-balancer"></a>從 hello 負載平衡器移除 VM

藉由重設 hello 了 LoadBalancerBackendAddressPools 屬性 hello 網路介面卡移除 hello 後端位址集區的 VM。

取得與 hello 網路介面卡[Get AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface):

```powershell
$nic = Get-AzureRmNetworkInterface -ResourceGroupName myResourceGroup -Name myNic2
``` 

Hello 網路介面卡 hello 了 LoadBalancerBackendAddressPools 屬性設定太 $null:

```powershell
$nic.Ipconfigurations[0].LoadBalancerBackendAddressPools=$null
```

更新 hello 網路介面卡：

```powershell
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

### <a name="add-a-vm-toohello-load-balancer"></a>新增 VM toohello 負載平衡器

之後執行 VM 維護，或如果您需要 tooexpand 容量時，加入 hello NIC VM toohello 後端位址集區的 hello 負載平衡器。

收到 hello 負載平衡器：

```powershell
$lb = Get-AzureRMLoadBalancer -ResourceGroupName myResourceGroup -Name myLoadBalancer 
```

新增 hello hello 負載平衡器 toohello 網路介面卡的後端位址集區：

```powershell
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$lb.BackendAddressPools[0]
```

更新 hello 網路介面卡：

```powershell
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

## <a name="next-steps"></a>後續步驟

範例 – [Azure 虛擬機器 PowerShell 範例指令碼](./../virtual-machines-windows-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
