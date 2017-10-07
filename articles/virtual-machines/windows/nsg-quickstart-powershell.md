---
title: "aaaOpen 連接埠 tooa VM 使用 Azure PowerShell |Microsoft 文件"
description: "深入了解如何 tooopen 連接埠建立端點 tooyour Windows VM / 使用 hello Azure 資源管理員部署模式和 Azure PowerShell"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: cf45f7d8-451a-48ab-8419-730366d54f1e
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: iainfou
ms.openlocfilehash: c1817a0c447ae4ce7a1ce2a1fc6927bedf2dacb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooopen-ports-and-endpoints-tooa-vm-in-azure-using-powershell"></a>如何 tooopen 連接埠和端點 tooa 使用 PowerShell 在 Azure 中的 VM
[!INCLUDE [virtual-machines-common-nsg-quickstart](../../../includes/virtual-machines-common-nsg-quickstart.md)]

## <a name="quick-commands"></a>快速命令
toocreate 網路安全性的群組和 ACL 規則您需要[hello 最新版本的 Azure PowerShell 安裝](/powershell/azureps-cmdlets-docs)。 您也可以[使用 hello Azure 入口網站執行這些步驟](nsg-quickstart-portal.md)。

Azure 帳戶登入 tooyour 中：

```powershell
Login-AzureRmAccount
```

在 hello 下列範例中，會取代您自己的值的範例參數名稱。 範例參數名稱包括 myResourceGroup、myNetworkSecurityGroup 和 myVnet。

使用 [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) 建立規則。 hello 下列範例會建立名為的規則*myNetworkSecurityGroupRule* tooallow *tcp*連接埠的流量*80*:

```powershell
$httprule = New-AzureRmNetworkSecurityRuleConfig `
    -Name "myNetworkSecurityGroupRule" `
    -Description "Allow HTTP" `
    -Access "Allow" `
    -Protocol "Tcp" `
    -Direction "Inbound" `
    -Priority "100" `
    -SourceAddressPrefix "Internet" `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 80
```

接下來，建立您的網路安全性群組與[新增 AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup)和指派 hello HTTP 規則您剛剛建立，如下所示。 hello 下列範例會建立名為的網路安全性群組*myNetworkSecurityGroup*:

```powershell
$nsg = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName "myResourceGroup" `
    -Location "EastUS" `
    -Name "myNetworkSecurityGroup" `
    -SecurityRules $httprule
```

現在讓我們將您的網路安全性群組 tooa 子網路指派。 hello 下列範例會將指派現有的虛擬網路，名為*myVnet* toohello 變數*$vnet*與[Get AzureRmVirtualNetwork](/powershell/module/azurerm.network/get-azurermvirtualnetwork):

```powershell
$vnet = Get-AzureRmVirtualNetwork `
    -ResourceGroupName "myResourceGroup" `
    -Name "myVnet"
```

使用 [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig) 將網路安全性群組與子網路建立關聯。 hello 下列範例將名為 「 hello 」 子網路*mySubnet*與您的網路安全性群組：

```powershell
$subnetPrefix = $vnet.Subnets|?{$_.Name -eq 'mySubnet'}

Set-AzureRmVirtualNetworkSubnetConfig `
    -VirtualNetwork $vnet `
    -Name "mySubnet" `
    -AddressPrefix $subnetPrefix.AddressPrefix `
    -NetworkSecurityGroup $nsg
```

最後，更新虛擬網路與[組 AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork)為了讓您變更 tootake 效果：

```powershell
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```


## <a name="more-information-on-network-security-groups"></a>網路安全性群組的詳細資訊
這裡 hello 快速命令可讓您設定 tooget 和流量流動 tooyour VM 執行。 網路安全性群組可提供許多很棒的功能和控制存取 tooyour 資源的資料粒度。 您可以深入了解 [建立網路安全性群組和 ACL 規則](tutorial-virtual-network.md#manage-internal-traffic)。

針對高可用性 Web 應用程式，您應該將 VM 放在 Azure Load Balancer 後方。 hello 負載平衡器會將流量 tooVMs，以提供的流量篩選的網路安全性群組。 如需詳細資訊，請參閱[如何 tooload 平衡 Linux 虛擬機器中 Azure toocreate 高可用性的應用程式](tutorial-load-balancer.md)。

## <a name="next-steps"></a>後續步驟
在此範例中，您可以建立簡單的規則 tooallow HTTP 流量。 您可以找到有關 hello 下列文件中建立更詳細的環境：

* [Azure Resource Manager 概觀](../../azure-resource-manager/resource-group-overview.md)
* [什麼是網路安全性群組 (NSG)？](../../virtual-network/virtual-networks-nsg.md)
* [負載平衡器的 Azure Resource Manager 概觀](../../load-balancer/load-balancer-arm.md)

