---
title: "aaaCreate 和管理 Windows Vm hello Azure PowerShell 模組 |Microsoft 文件"
description: "教學課程-建立和管理 Windows Vm 與 hello Azure PowerShell 模組"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 20adcb673ef4de683e6ad82d048a9625a1dc838c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-windows-vms-with-hello-azure-powershell-module"></a>建立和管理 Windows Vm 與 hello Azure PowerShell 模組

Azure 虛擬機器提供完全可設定且彈性的計算環境。 本教學課程涵蓋基本的「Azure 虛擬機器」部署項目，例如選取 VM 大小、選取 VM 映像、部署 VM。 您會了解如何：

> [!div class="checklist"]
> * 建立和連線 tooa VM
> * 選取及使用 VM 映像
> * 檢視及使用特定 VM 大小
> * 調整 VM 的大小
> * 檢視及了解 VM 狀態

本教學課程需要 hello Azure PowerShell 模組版本 3.6 版或更新版本。 執行` Get-Module -ListAvailable AzureRM`toofind hello 版本。 如果您需要 tooupgrade，請參閱[安裝 Azure PowerShell 模組](/powershell/azure/install-azurerm-ps)。

## <a name="create-resource-group"></a>建立資源群組

建立資源群組以 hello[新增 AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup)命令。 

Azure 資源群組是在其中部署與管理 Azure 資源的邏輯容器。 資源群組必須在虛擬機器之前建立。 在此範例中，資源群組命名為*myResourceGroupVM*會建立在 hello *EastUS*區域。 

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroupVM -Location EastUS
```

建立或修改 VM，能看到本教學課程時，所指定 hello 資源群組。

## <a name="create-virtual-machine"></a>Create virtual machine

虛擬機器必須連接的 tooa 虛擬網路。 您與 hello 透過網路介面卡使用的公用 IP 位址的虛擬機器進行通訊。

### <a name="create-virtual-network"></a>建立虛擬網路

使用 [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) 建立子網路：

```powershell
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24
```

使用 [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) 建立虛擬網路：

```powershell
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroupVM `
  -Location EastUS `
  -Name myVnet `
  -AddressPrefix 192.168.0.0/16 ` 
  -Subnet $subnetConfig
```
### <a name="create-public-ip-address"></a>建立公用 IP 位址

使用 [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) 建立公用 IP 位址：

```powershell
$pip = New-AzureRmPublicIpAddress ` 
  -ResourceGroupName myResourceGroupVM `
  -Location EastUS ` 
  -AllocationMethod Static `
  -Name myPublicIPAddress
```

### <a name="create-network-interface-card"></a>建立網路介面卡

使用 [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) 建立網路介面卡：

```powershell
$nic = New-AzureRmNetworkInterface `
  -ResourceGroupName myResourceGroupVM  `
  -Location EastUS `
  -Name myNic `
  -SubnetId $vnet.Subnets[0].Id `
  -PublicIpAddressId $pip.Id
```

### <a name="create-network-security-group"></a>建立網路安全性群組

Azure [網路安全性群組](../../virtual-network/virtual-networks-nsg.md) (NSG) 控制一或多部虛擬機器的輸入和傳出流量。 網路安全性群組規則可允許或拒絕特定連接埠或連接埠範圍上的網路流量。 這些規則也可以包含來源位址首碼，所以只有在預先定義的來源產生的流量可以與虛擬機器通訊。 tooaccess hello IIS web 伺服器上所安裝，您必須將輸入的 NSG 規則。

toocreate 輸入 NSG 規則，使用[新增 AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/add-azurermnetworksecurityruleconfig)。 hello 下列範例會建立名為 NSG 規則*myNSGRule*的開啟連接埠*3389* hello 虛擬機器：

```powershell
$nsgRule = New-AzureRmNetworkSecurityRuleConfig `
  -Name myNSGRule `
  -Protocol Tcp `
  -Direction Inbound `
  -Priority 1000 `
  -SourceAddressPrefix * `
  -SourcePortRange * `
  -DestinationAddressPrefix * `
  -DestinationPortRange 3389 `
  -Access Allow
```

建立 hello NSG 使用*myNSGRule*與[新增 AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup):

```powershell
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName myResourceGroupVM `
    -Location EastUS `
    -Name myNetworkSecurityGroup `
    -SecurityRules $nsgRule
```

Hello 虛擬網路中新增子網路-NSG toohello hello[組 AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig):

```powershell
Set-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -VirtualNetwork $vnet `
    -NetworkSecurityGroup $nsg `
    -AddressPrefix 192.168.1.0/24
```

更新 hello 虛擬網路與[組 AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork):

```powershell
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```

### <a name="create-virtual-machine"></a>Create virtual machine

建立虛擬機器時，有數個可用的選項，例如作業系統映像、磁碟大小及系統管理認證。 在此範例中，虛擬機器會建立名稱為*myVM*執行 hello 最新版本的 Windows Server 2016 資料中心。

設定 hello 使用者名稱和密碼所需的 hello 與 hello 虛擬機器上的系統管理員帳戶[Get-credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):

```powershell
$cred = Get-Credential
```

建立 hello hello 的虛擬機器的初始設定[新增 AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig):

```powershell
$vm = New-AzureRmVMConfig -VMName myVM -VMSize Standard_D1
```

新增 hello 資訊 toohello 虛擬機器設定作業系統[組 AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem):

```powershell
$vm = Set-AzureRmVMOperatingSystem `
    -VM $vm `
    -Windows `
    -ComputerName myVM `
    -Credential $cred `
    -ProvisionVMAgent -EnableAutoUpdate
```

新增 hello 映像 toohello 虛擬機器組態資訊與[組 AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage):

```powershell
$vm = Set-AzureRmVMSourceImage `
    -VM $vm `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter `
    -Version latest
```

新增 hello 作業系統磁碟設定 toohello 虛擬機器組態[組 AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk):

```powershell
$vm = Set-AzureRmVMOSDisk `
    -VM $vm `
    -Name myOsDisk `
    -DiskSizeInGB 128 `
    -CreateOption FromImage `
    -Caching ReadWrite
```

新增 hello 網路介面卡，您先前建立的虛擬機器組態 toohello[新增 AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):

```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

建立虛擬機器 hello[新增 AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm)。

```powershell
New-AzureRmVM -ResourceGroupName myResourceGroupVM -Location EastUS -VM $vm
```

## <a name="connect-toovm"></a>連接 tooVM

Hello 部署已完成之後，請使用 hello 的虛擬機器建立遠端桌面連線。

執行下列命令 tooreturn hello 公用 IP 位址的 hello 虛擬機器的 hello。 記下此 IP 位址，讓您能連接 tooit 與您的瀏覽器 tootest web 連線，在未來的步驟。

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName myResourceGroupVM  | Select IpAddress
```

使用 hello 下列命令 toocreate 與 hello 虛擬機器的遠端桌面工作階段。 Hello IP 位址取代成 hello *publicIPAddress*的虛擬機器。 出現提示時，輸入 hello 建立 hello 虛擬機器時使用的認證。

```powershell
mstsc /v:<publicIpAddress>
```

## <a name="understand-vm-images"></a>了解 VM 映像

hello Azure marketplace 包括許多可以使用的 toocreate 新的虛擬機器的虛擬機器映像。 在 hello 先前步驟中，已使用 hello Windows Server 2016 資料中心映像建立虛擬機器。 在此步驟中，會使用的 toosearch hello marketplace 中的其他 Windows 映像，適用於新的 Vm 也可以做為基底 hello PowerShell 模組。 這個程序包含尋找 hello 發行者、 提供項目和 hello 映像名稱 (Sku)。 

使用 hello [Get AzureRmVMImagePublisher](/powershell/module/azurerm.compute/get-azurermvmimagepublisher)命令 tooreturn 映像的發行者清單。  

```powersehll
Get-AzureRmVMImagePublisher -Location "EastUS"
```

使用 hello [Get AzureRmVMImageOffer](/powershell/module/azurerm.compute/get-azurermvmimageoffer) tooreturn 映像優惠清單。 利用這個命令，hello 傳回 hello 指定 「 發行者 」 上篩選清單。 

```powershell
Get-AzureRmVMImageOffer -Location "EastUS" -PublisherName "MicrosoftWindowsServer"
```

```powershell
Offer             PublisherName          Location
-----             -------------          -------- 
Windows-HUB       MicrosoftWindowsServer EastUS 
WindowsServer     MicrosoftWindowsServer EastUS   
WindowsServer-HUB MicrosoftWindowsServer EastUS   
```

hello [Get AzureRmVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku)命令將會接著篩選 hello 發行者和供應項目名稱 tooreturn 上的映像名稱清單。

```powershell
Get-AzureRmVMImageSku -Location "EastUS" -PublisherName "MicrosoftWindowsServer" -Offer "WindowsServer"
```

```powershell
Skus                            Offer         PublisherName          Location
----                            -----         -------------          --------
2008-R2-SP1                     WindowsServer MicrosoftWindowsServer EastUS  
2008-R2-SP1-BYOL                WindowsServer MicrosoftWindowsServer EastUS  
2012-Datacenter                 WindowsServer MicrosoftWindowsServer EastUS  
2012-Datacenter-BYOL            WindowsServer MicrosoftWindowsServer EastUS  
2012-R2-Datacenter              WindowsServer MicrosoftWindowsServer EastUS  
2012-R2-Datacenter-BYOL         WindowsServer MicrosoftWindowsServer EastUS  
2016-Datacenter                 WindowsServer MicrosoftWindowsServer EastUS  
2016-Datacenter-Server-Core     WindowsServer MicrosoftWindowsServer EastUS  
2016-Datacenter-with-Containers WindowsServer MicrosoftWindowsServer EastUS  
2016-Nano-Server                WindowsServer MicrosoftWindowsServer EastUS
```

這項資訊可以使用的 toodeploy 具有特定的映像的 VM。 這個範例 hello VM 物件上設定 hello 映像名稱。 在本教學課程的完整的部署步驟，請參閱 toohello 前面的範例。

```powershell
$vm = Set-AzureRmVMSourceImage `
    -VM $vm `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter-with-Containers `
    -Version latest
```

## <a name="understand-vm-sizes"></a>了解 VM 大小

虛擬機器大小會決定 hello 量，例如 CPU、 GPU，以及記憶體都會提供 toohello 虛擬機器的計算資源。 虛擬機器必須 toobe 建立大小適當的 hello 預期工作負載。 如果工作負載增加，可以調整現有虛擬機器的大小。

### <a name="vm-sizes"></a>VM 大小

下表中的 hello 將大小分類成使用案例。  

| 類型                     | 大小           |    說明       |
|--------------------------|-------------------|------------------------------------------------------------------------------------------------------------------------------------|
| 一般用途         |DSv2、Dv2、DS、D、Av2、A0-7| 平衡的 CPU 對記憶體。 適用於開發 / 測試及小型 toomedium 應用程式和資料解決方案。  |
| 計算最佳化      | Fs、F             | CPU 與記憶體的比例高。 適用於中流量應用程式、網路設備及批次處理。        |
| 記憶體最佳化       | GS、G、DSv2、DS、Dv2、D   | 記憶體與核心的比例高。 太棒了關聯式資料庫、 中度 toolarge 快取，以及記憶體中分析。                 |
| 儲存體最佳化       | Ls                | 高磁碟輸送量及 IO。 適用於巨量資料、SQL 及 NoSQL 資料庫。                                                         |
| GPU           | NV、NC            | 以大量圖形轉譯和影片編輯為目標的特製化 VM。       |
| 高效能 | H、A8-11          | 我們的最強大 CPU VM，可搭配選用的高輸送量網路介面 (RDMA)。 


### <a name="find-available-vm-sizes"></a>尋找可用的 VM 大小

在特定區域大小可用 toosee VM 的清單，請使用 hello [Get AzureRmVMSize](/powershell/module/azurerm.compute/get-azurermvmsize)命令。

```powershell
Get-AzureRmVMSize -Location EastUS
```

## <a name="resize-a-vm"></a>調整 VM 的大小

已部署 VM 之後，它可以是調整過大小的 tooincrease 或減少資源配置。

之前調整 VM 大小時，請檢查 hello 所需的大小是否可以使用 hello 目前 VM 的叢集。 hello [Get AzureRmVMSize](/powershell/module/azurerm.compute/get-azurermvmsize)命令會傳回大小的清單。 

```powershell
Get-AzureRmVMSize -ResourceGroupName myResourceGroupVM -VMName myVM 
```

如果 hello 所需的大小是可用，hello VM 可以調整大小，從開機的狀態，不過 hello 作業期間重新開機。

```powershell
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroupVM  -VMName myVM 
$vm.HardwareProfile.VmSize = "Standard_D4"
Update-AzureRmVM -VM $vm -ResourceGroupName myResourceGroupVM 
```

如果 hello 所需的大小不 hello 目前在叢集上，hello VM toobe hello 的調整大小作業之前取消配置可能會發生的需求。 請注意，當 hello VM 開機回、 hello 暫存磁碟上的任何資料會遭到移除，並 hello 公用 IP 位址變更，除非正在使用的靜態 IP 位址。 

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroupVM -Name "myVM" -Force
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroupVM  -VMName myVM
$vm.HardwareProfile.VmSize = "Standard_F4s"
Update-AzureRmVM -VM $vm -ResourceGroupName myResourceGroupVM 
Start-AzureRmVM -ResourceGroupName myResourceGroupVM  -Name $vm.name
```

## <a name="vm-power-states"></a>VM 電源狀態

Azure VM 的電源狀態可以是許多電源狀態的其中一種。 此狀態表示 hello 目前 hello VM 的狀態從 hello hypervisor hello 觀點來看。 

### <a name="power-states"></a>電源狀態

| 電源狀態 | 說明
|----|----|
| 啟動中 | 指出正在啟動 hello 虛擬機器。 |
| 執行中 | 指出該 hello 虛擬機器正在執行。 |
| 停止中 | 表示正在停止該 hello 虛擬機器。 | 
| 已停止 | 表示該 hello 虛擬機器已停止。 請注意在 hello 停止狀態的虛擬機器仍會產生計算費用。  |
| 正在解除配置 | 表示已解除配置該 hello 虛擬機器。 |
| 已解除配置 | 表示從 hello hypervisor，但仍然可以使用 hello 控制平面中完全移除該 hello 虛擬機器。 Hello 取消配置狀態中的虛擬機器不會產生計算費用。 |
| - | 表示 hello hello 虛擬機器的電源狀態不明。 |

### <a name="find-power-state"></a>尋找電源狀態

特定的 VM，使用 hello tooretrieve hello 狀態[Get AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm)命令。 為確定 toospecify 虛擬機器與資源群組的有效名稱。 

```powershell
Get-AzureRmVM `
    -ResourceGroupName myResourceGroup `
    -Name myVM `
    -Status | Select @{n="Status"; e={$_.Statuses[1].Code}}
```

輸出：

```powershell
Status
------
PowerState/running
```

## <a name="management-tasks"></a>管理工作

在虛擬機器的 hello 生命週期，您可能想 toorun 管理工作，例如啟動、 停止或刪除虛擬機器。 此外，您可能想 toocreate 指令碼 tooautomate 重複或複雜工作。 使用 Azure PowerShell，多的常見管理工作可以執行從 hello 命令列或指令碼中。

### <a name="stop-virtual-machine"></a>停止虛擬機器

使用 [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) 停止及解除配置虛擬機器：

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroupVM -Name "myVM" -Force
```

如果您想 tookeep hello 中佈建狀態的虛擬機器，請使用 hello-StayProvisioned 參數。

### <a name="start-virtual-machine"></a>啟動虛擬機器

```powershell
Start-AzureRmVM -ResourceGroupName myResourceGroupVM -Name myVM
```

### <a name="delete-resource-group"></a>刪除資源群組

刪除資源群組同時會刪除其內含的所有資源。

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroupVM -Force
```

## <a name="next-steps"></a>後續步驟

在本教學課程中，您已了解基本的 VM 建立和管理，像是如何：

> [!div class="checklist"]
> * 建立和連線 tooa VM
> * 選取及使用 VM 映像
> * 檢視及使用特定 VM 大小
> * 調整 VM 的大小
> * 檢視及了解 VM 狀態

前進 toohello 下一個教學課程的 toolearn 有關 VM 磁碟。  

> [!div class="nextstepaction"]
> [建立和管理 VM 磁碟](./tutorial-manage-data-disk.md)
