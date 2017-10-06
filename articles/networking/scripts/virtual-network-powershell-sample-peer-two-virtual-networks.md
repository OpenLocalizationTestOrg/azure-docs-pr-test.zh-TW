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
# <a name="peer-two-virtual-networks"></a><span data-ttu-id="bcac1-103">讓兩個虛擬網路對等互連</span><span class="sxs-lookup"><span data-stu-id="bcac1-103">Peer two virtual networks</span></span>

<span data-ttu-id="bcac1-104">此指令碼會建立和連接 hello 中的兩個虛擬網路相同的區域 trhough hello Azure 網路。</span><span class="sxs-lookup"><span data-stu-id="bcac1-104">This script creates and connects two virtual networks in hello same region trhough hello Azure network.</span></span> <span data-ttu-id="bcac1-105">執行 hello 指令碼之後, 您將建立兩個虛擬網路之間對等互連。</span><span class="sxs-lookup"><span data-stu-id="bcac1-105">After running hello script, you will create a peering between two virtual networks.</span></span>

<span data-ttu-id="bcac1-106">如有需要安裝 Azure PowerShell 中使用 hello 指令位於 hello hello [Azure PowerShell 指南](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/)，然後執行`Login-AzureRmAccount`toocreate 與 Azure 的連線。</span><span class="sxs-lookup"><span data-stu-id="bcac1-106">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="bcac1-107">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="bcac1-107">Sample script</span></span>

[!code-azurepowershell[main](../../../powershell_scripts/virtual-network/peer-two-virtual-networks/peer-two-virtual-networks.ps1 "Peer two networks")]

## <a name="clean-up-deployment"></a><span data-ttu-id="bcac1-108">清除部署</span><span class="sxs-lookup"><span data-stu-id="bcac1-108">Clean up deployment</span></span> 

<span data-ttu-id="bcac1-109">執行下列命令 tooremove hello 資源群組、 VM 和所有相關的資源的 hello。</span><span class="sxs-lookup"><span data-stu-id="bcac1-109">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="bcac1-110">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="bcac1-110">Script explanation</span></span>

<span data-ttu-id="bcac1-111">此指令碼會使用下列命令 toocreate 資源群組、 虛擬機器的 hello 和所有相關聯的資源。</span><span class="sxs-lookup"><span data-stu-id="bcac1-111">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="bcac1-112">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="bcac1-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="bcac1-113">命令</span><span class="sxs-lookup"><span data-stu-id="bcac1-113">Command</span></span> | <span data-ttu-id="bcac1-114">注意事項</span><span class="sxs-lookup"><span data-stu-id="bcac1-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="bcac1-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="bcac1-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="bcac1-116">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="bcac1-116">Creates a resource group in which all resources are stored.</span></span> | 
| [<span data-ttu-id="bcac1-117">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="bcac1-117">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork)| <span data-ttu-id="bcac1-118">建立 Azure 虛擬網路和子網路。</span><span class="sxs-lookup"><span data-stu-id="bcac1-118">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="bcac1-119">Add-AzureRmVirtualNetworkPeering</span><span class="sxs-lookup"><span data-stu-id="bcac1-119">Add-AzureRmVirtualNetworkPeering</span></span>](/powershell/module/azurerm.network/add-azurermvirtualnetworkpeering) | <span data-ttu-id="bcac1-120">在兩個虛擬網路之間建立對等互連。</span><span class="sxs-lookup"><span data-stu-id="bcac1-120">Creates a peering between two virtual networks.</span></span>  |
| [<span data-ttu-id="bcac1-121">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="bcac1-121">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="bcac1-122">刪除資源群組，包括所有的巢狀資源。</span><span class="sxs-lookup"><span data-stu-id="bcac1-122">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="bcac1-123">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bcac1-123">Next steps</span></span>

<span data-ttu-id="bcac1-124">如需有關 hello Azure PowerShell 的詳細資訊，請參閱[Azure PowerShell 文件](https://docs.microsoft.com/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="bcac1-124">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="bcac1-125">其他網路的 PowerShell 指令碼範例可以在 hello [Azure 網路概觀文件](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="bcac1-125">Additional networking PowerShell script samples can be found in hello [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>
