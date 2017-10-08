---
title: "aaaAzure 虛擬網路和 Windows 虛擬機器 |Microsoft 文件"
description: "教學課程 - 使用 Azure PowerShell 來管理 Azure 虛擬網路和 Windows 虛擬機器"
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
ms.date: 05/02/2017
ms.author: davidmu
ms.custom: mvc
ms.openlocfilehash: ed77d9d5873e849fcb2aaf15e41899d7ad8c781a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-virtual-networks-and-windows-virtual-machines-with-azure-powershell"></a>使用 Azure PowerShell 來管理 Azure 虛擬網路和 Windows 虛擬機器

Azure 虛擬機器會使用 Azure 網路進行內部和外部的網路通訊。 在本教學課程中，您會在虛擬網路中建立多部虛擬機器 (VM)，並設定這些機器間的網路連線。 您會了解如何：

> [!div class="checklist"]
> * 建立虛擬網路
> * 建立虛擬網路子網路
> * 使用網路安全性群組來控制網路流量
> * 檢視作用中的流量規則

本教學課程需要 hello Azure PowerShell 模組版本 3.6 版或更新版本。 執行` Get-Module -ListAvailable AzureRM`toofind hello 版本。 如果您需要 tooupgrade，請參閱[安裝 Azure PowerShell 模組](/powershell/azure/install-azurerm-ps)。

## <a name="create-vnet"></a>建立 VNet

VNet 是網路的您自己 hello 雲端中的表示法。 VNet 是 hello 的隔離的邏輯專用的 Azure 雲端 tooyour 訂用帳戶。 在 VNet 中，您可以找到子網路，連線 toothose 子網路和來自 hello Vm toohello 子網路連線的規則。

您可以建立其他的 Azure 資源之前，您需要 toocreate 的資源群組與[新增 AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup)。 hello 下列範例會建立名為的資源群組*myRGNetwork*在 hello *EastUS*位置：

```powershell
New-AzureRmResourceGroup -ResourceGroupName myRGNetwork -Location EastUS
```

子網路是 VNET 的子資源，而且有助於使用 IP 位址首碼來定義 CIDR 區塊內位址空間的區段。 Nic 可以加入 toosubnets，並已連線的 tooVMs，提供各種工作負載的連線。

使用 [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) 來建立子網路：

```powershell
$frontendSubnet = New-AzureRmVirtualNetworkSubnetConfig `
  -Name myFrontendSubnet `
  -AddressPrefix 10.0.0.0/24
```

使用 myFrontendSubnet 和 [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) 建立一個名為 *myVNet* 的 VNET：

```powershell
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myVNet `
  -AddressPrefix 10.0.0.0/16 `
  -Subnet $frontendSubnet
```

## <a name="create-front-end-vm"></a>建立前端 VM

在 VNet 中 VM toocommunicate，它必須在虛擬網路介面 (NIC)。 hello *myFrontendVM*從 hello 存取網際網路，因此也需要公用 IP 位址。 

使用 [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) 來建立公用 IP 位址：

```powershell
$pip = New-AzureRmPublicIpAddress `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -AllocationMethod Static `
  -Name myPublicIPAddress
```

使用 [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) 來建立 NIC：


```powershell
$frontendNic = New-AzureRmNetworkInterface `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myFrontendNic `
  -SubnetId $vnet.Subnets[0].Id `
  -PublicIpAddressId $pip.Id
```

設定 hello 使用者名稱和密碼所需的 hello hello VM 上的系統管理員帳戶與[Get-credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):

```powershell
$cred = Get-Credential
```

建立與 hello Vm[新增 AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig)，[組 AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem)，[組 AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage)，[組 AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk)，[新增 AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface)，和[新 AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm)。 

```powershell
$frontendVM = New-AzureRmVMConfig `
    -VMName myFrontendVM `
    -VMSize Standard_D1
$frontendVM = Set-AzureRmVMOperatingSystem `
    -VM $frontendVM `
    -Windows `
    -ComputerName myFrontendVM `
    -Credential $cred `
    -ProvisionVMAgent `
    -EnableAutoUpdate
$frontendVM = Set-AzureRmVMSourceImage `
    -VM $frontendVM `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter `
    -Version latest
$frontendVM = Set-AzureRmVMOSDisk `
    -VM $frontendVM `
    -Name myFrontendOSDisk `
    -DiskSizeInGB 128 `
    -CreateOption FromImage `
    -Caching ReadWrite
$frontendVM = Add-AzureRmVMNetworkInterface `
    -VM $frontendVM `
    -Id $frontendNic.Id
New-AzureRmVM `
    -ResourceGroupName myRGNetwork `
    -Location EastUS `
    -VM $frontendVM
```

## <a name="install-web-server"></a>安裝 Web 伺服器

您可以使用遠端桌面工作階段在 myFrontendVM 上安裝 IIS。 您需要 tooget hello 公用 IP 位址的 hello VM tooaccess 它。

您可以取得 hello 公用 IP 位址*myFrontendVM*與[Get AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress)。 hello 下列範例會取得 IP 位址 hello *myPublicIPAddress*稍早建立：

```powershell
Get-AzureRmPublicIPAddress `
    -ResourceGroupName myRGNetwork `
    -Name myPublicIPAddress | select IpAddress
```

請記下此 IP 位址，以便在未來的步驟中使用它。

使用 hello 下列命令與遠端桌面工作階段的 toocreate *myFrontendVM*。 取代 *<publicIPAddress>*  hello 位址，您先前記錄的密碼。 出現提示時，輸入 hello 建立 hello VM 時所使用的認證。

```
mstsc /v:<publicIpAddress>
``` 

既然已登入太*myFrontendVM*，您可以使用單行 PowerShell tooinstall IIS 並啟用 hello 本機防火牆規則 tooallow web 流量。 開啟 PowerShell 命令提示字元並執行下列命令的 hello:

使用[Install-windowsfeature](https://technet.microsoft.com/itpro/powershell/windows/servermanager/install-windowsfeature) toorun hello 自訂指令碼延伸安裝 hello IIS web 伺服器：

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

現在您可以使用 hello 公用 IP 位址 toobrowse toohello VM toosee hello IIS 站台。

![IIS 預設網站](./media/tutorial-virtual-network/iis.png)

## <a name="manage-internal-traffic"></a>管理內部網路流量

網路安全性群組 (NSG) 包含一份安全性規則，允許或拒絕網路流量連線的 tooresources tooa VNet。 Nsg 可以是相關聯的 toosubnets 或個別的 Nic 附加 tooVMs。 開啟或關閉存取 tooVMs 透過連接埠是使用 NSG 規則。 建立 myFrontendVM 時，會自動開啟輸入連接埠 3389 以供 RDP 連線使用。

您可以使用 NSG 來設定 VM 的內部通訊。 在本節中，您學會如何 toocreate hello 中的其他子網路的網路並指派 NSG tooit tooallow 從連接*myFrontendVM*太*myBackendVM*通訊埠 1433年上。 hello 指派子網路是然後 toohello VM 建立時。

您可以限制內部流量太*myBackendVM*僅從*myFrontendVM*藉由建立 hello 後端子網路的 NSG。 hello 下列範例會建立名為 NSG 規則*myBackendNSGRule*與[新增 AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig):

```powershell
$nsgBackendRule = New-AzureRmNetworkSecurityRuleConfig `
  -Name myBackendNSGRule `
  -Protocol Tcp `
  -Direction Inbound `
  -Priority 100 `
  -SourceAddressPrefix 10.0.0.0/24 `
  -SourcePortRange * `
  -DestinationAddressPrefix * `
  -DestinationPortRange 1433 `
  -Access Allow
```

使用 [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) 來新增名為 myBackendNSG 的網路安全性群組：

```powershell
$nsgBackend = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myBackendNSG `
  -SecurityRules $nsgBackendRule
```
## <a name="add-back-end-subnet"></a>新增後端子網路

新增*myBackEndSubnet*太*myVNet*與[新增 AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig):

```powershell
Add-AzureRmVirtualNetworkSubnetConfig `
  -Name myBackendSubnet `
  -VirtualNetwork $vnet `
  -AddressPrefix 10.0.1.0/24 `
  -NetworkSecurityGroup $nsgBackend
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
$vnet = Get-AzureRmVirtualNetwork `
  -ResourceGroupName myRGNetwork `
  -Name myVNet
```

## <a name="create-back-end-vm"></a>建立後端 VM

最簡單方式 toocreate hello hello 後端 VM 是使用 SQL Server 映像。 本教學課程只會 hello VM 建立 hello 資料庫伺服器，但不會提供有關存取 hello 資料庫資訊。

建立 myBackendNic：

```powershell
$backendNic = New-AzureRmNetworkInterface `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -Name myBackendNic `
  -SubnetId $vnet.Subnets[1].Id
```

Hello 使用者名稱和密碼所需的 hello hello Get-credential 與 VM 上的系統管理員帳戶設定：

```powershell
$cred = Get-Credential
```

建立 myBackendVM：

```powershell
$backendVM = New-AzureRmVMConfig `
  -VMName myBackendVM `
  -VMSize Standard_D1
$backendVM = Set-AzureRmVMOperatingSystem `
  -VM $backendVM `
  -Windows `
  -ComputerName myBackendVM `
  -Credential $cred `
  -ProvisionVMAgent `
  -EnableAutoUpdate
$backendVM = Set-AzureRmVMSourceImage `
  -VM $backendVM `
  -PublisherName MicrosoftSQLServer `
  -Offer SQL2016SP1-WS2016 `
  -Skus Enterprise `
  -Version latest
$backendVM = Set-AzureRmVMOSDisk `
  -VM $backendVM `
  -Name myBackendOSDisk `
  -DiskSizeInGB 128 `
  -CreateOption FromImage `
  -Caching ReadWrite
$backendVM = Add-AzureRmVMNetworkInterface `
  -VM $backendVM `
  -Id $backendNic.Id
New-AzureRmVM `
  -ResourceGroupName myRGNetwork `
  -Location EastUS `
  -VM $backendVM
```

hello 映像使用有 SQL Server 安裝，而不是在本教學課程。 它是包含的 tooshow 您如何設定 VM toohandle 網路流量和 VM toohandle 資料庫管理。

## <a name="next-steps"></a>後續步驟

在本教學課程中，您可以建立並保護做為相關的 toovirtual 機器的 Azure 網路。 

> [!div class="checklist"]
> * 建立虛擬網路
> * 建立虛擬網路子網路
> * 使用網路安全性群組來控制網路流量
> * 檢視作用中的流量規則

前進 toohello 下一個教學課程的 toolearn 有關監視使用 Azure 備份的虛擬機器上的保護資料。 .

> [!div class="nextstepaction"]
> [備份 Azure 中的 Windows 虛擬機器](./tutorial-backup-vms.md)
