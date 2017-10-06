---
title: "aaaAzure PowerShell 指令碼範例的對等的兩個虛擬網路 |Microsoft 文件"
description: "Azure PowerShell 指令碼範例 - 讓兩個虛擬網路對等互連"
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
ms.openlocfilehash: 8b66085c35de2fc30bcef57a00d7d370911d1f3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="peer-two-virtual-networks"></a>讓兩個虛擬網路對等互連

此指令碼會建立和連接 hello 中的兩個虛擬網路相同的區域 trhough hello Azure 網路。 執行 hello 指令碼之後, 您將建立兩個虛擬網路之間對等互連。

如有需要安裝 Azure PowerShell 中使用 hello 指令位於 hello hello [Azure PowerShell 指南](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/)，然後執行`Login-AzureRmAccount`toocreate 與 Azure 的連線。

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>範例指令碼

[!code-azurepowershell[main](../../../powershell_scripts/virtual-network/peer-two-virtual-networks/peer-two-virtual-networks.ps1 "Peer two networks")]

## <a name="clean-up-deployment"></a>清除部署 

執行下列命令 tooremove hello 資源群組、 VM 和所有相關的資源的 hello。

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a>指令碼說明

此指令碼會使用下列命令 toocreate 資源群組、 虛擬機器的 hello 和所有相關聯的資源。 Hello 資料表連結 toocommand 特定文件中的每個命令。

| 命令 | 注意事項 |
|---|---|
| [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) | 建立用來存放所有資源的資源群組。 | 
| [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork)| 建立 Azure 虛擬網路和子網路。 |
| [Add-AzureRmVirtualNetworkPeering](/powershell/module/azurerm.network/add-azurermvirtualnetworkpeering) | 在兩個虛擬網路之間建立對等互連。  |
| [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | 刪除資源群組，包括所有的巢狀資源。 |

## <a name="next-steps"></a>後續步驟

如需有關 hello Azure PowerShell 的詳細資訊，請參閱[Azure PowerShell 文件](https://docs.microsoft.com/powershell/azure/overview)。

其他網路的 PowerShell 指令碼範例可以在 hello [Azure 網路概觀文件](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json)。
