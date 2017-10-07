---
title: "aaaAzure PowerShell 指令碼範例透過網路的虛擬設備的路由傳送流量 |Microsoft 文件"
description: "Azure PowerShell 指令碼範例 - 透過防火牆網路虛擬設備來路由傳送流量。"
services: virtual-network
documentationcenter: virtual-network
author: georgewallace
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: powershell
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 05/16/2017
ms.author: gwallace
ms.openlocfilehash: 3b999f3289d654c00d5becb973e2883896457d52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="route-traffic-through-a-network-virtual-appliance"></a>透過網路虛擬設備來路由傳送流量

此指令碼範例會建立一個具有前端和後端子網路的虛擬網路。 它也會將啟用的 tooroute 流量 hello 兩個子網路之間轉送 ip 建立 VM。 執行 hello 指令碼之後，您可以部署網路的軟體，例如防火牆應用程式，toohello VM。

如有需要安裝 Azure PowerShell 中使用 hello 指令位於 hello hello [Azure PowerShell 指南](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/)，然後執行`Login-AzureRmAccount`toocreate 與 Azure 的連線。

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>範例指令碼


[!code-powershell[main](../../../powershell_scripts/virtual-network/route-traffic-through-nva/route-traffic-through-nva.ps1 "Route traffic through a network virtual appliance")]

## <a name="clean-up-deployment"></a>清除部署 

執行下列命令 tooremove hello 資源群組、 VM 和所有相關的資源的 hello。

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```
## <a name="script-explanation"></a>指令碼說明

此指令碼會使用下列命令 toocreate hello 資源群組、 虛擬網路和網路安全性群組。 Hello 資料表連結 toocommand 特定文件中的每個命令。

| 命令 | 注意事項 |
|---|---|
| [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup)  | 建立用來存放所有資源的資源群組。 |
| [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | 建立 Azure 虛擬網路和前端子網路。 |
| [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | 建立後端和 DMZ 子網路。 |
| [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) | 建立從 hello 網際網路的公用 IP 位址 tooaccess hello VM。 |
| [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) | 建立虛擬網路介面並為它啟用 IP 轉送功能。 |
| [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | 建立網路安全性群組 (NSG)。 |
| [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | 建立允許 HTTP 和 HTTPS 連接埠輸入 toohello VM 的 NSG 規則。 |
| [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig)| 路由資料表 toosubnets 和相關聯 hello Nsg。 |
| [New-AzureRmRouteTable](/powershell/module/azurerm.network/new-azurermroutetable)| 為所有路由建立一個路由表。 |
| [New-AzureRMRouteConfig](/powershell/module/azurerm.network/new-azurermrouteconfig)| 建立路由 tooroute hello 網際網路透過 hello VM 子網路之間的流量。 |
| [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) | 建立虛擬機器，並附加 hello NIC tooit。 此命令也會指定 hello 虛擬機器映像 toouse 和系統管理認證。 |
| [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup)  | 刪除資源群組及其包含的所有資源。 |

## <a name="next-steps"></a>後續步驟

如需有關 hello Azure PowerShell 的詳細資訊，請參閱[Azure PowerShell 文件](https://docs.microsoft.com/powershell/azure/overview)。

其他網路的 PowerShell 指令碼範例可以在 hello [Azure 網路概觀文件](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json)。
