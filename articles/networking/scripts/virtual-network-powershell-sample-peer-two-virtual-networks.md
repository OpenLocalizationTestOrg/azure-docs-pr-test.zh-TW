---
title: "Azure PowerShell 指令碼範例 - 讓兩個虛擬網路對等互連 | Microsoft Docs"
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
ms.openlocfilehash: 51c0b98727e148671cfd7ab2b31ffd1c705d8a4e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="peer-two-virtual-networks"></a><span data-ttu-id="75795-103">讓兩個虛擬網路對等互連</span><span class="sxs-lookup"><span data-stu-id="75795-103">Peer two virtual networks</span></span>

<span data-ttu-id="75795-104">此指令碼會在同一個區域中建立兩個虛擬網路，並透過 Azure 網路連接這兩個虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="75795-104">This script creates and connects two virtual networks in the same region trhough the Azure network.</span></span> <span data-ttu-id="75795-105">執行此指令碼之後，您將會在兩個虛擬網路之間建立對等互連。</span><span class="sxs-lookup"><span data-stu-id="75795-105">After running the script, you will create a peering between two virtual networks.</span></span>

<span data-ttu-id="75795-106">您可以視需要使用 [Azure PowerShell 指南 (英文)](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) 中的指示來安裝 Azure PowerShell，然後執行 `Login-AzureRmAccount` 來建立與 Azure 的連線。</span><span class="sxs-lookup"><span data-stu-id="75795-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="75795-107">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="75795-107">Sample script</span></span>

<span data-ttu-id="75795-108">[!code-azurepowershell[main](../../../powershell_scripts/virtual-network/peer-two-virtual-networks/peer-two-virtual-networks.ps1 "讓兩個網路對等互連")]</span><span class="sxs-lookup"><span data-stu-id="75795-108">[!code-azurepowershell[main](../../../powershell_scripts/virtual-network/peer-two-virtual-networks/peer-two-virtual-networks.ps1 "Peer two networks")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="75795-109">清除部署</span><span class="sxs-lookup"><span data-stu-id="75795-109">Clean up deployment</span></span> 

<span data-ttu-id="75795-110">執行下列命令來移除資源群組、VM 和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="75795-110">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="75795-111">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="75795-111">Script explanation</span></span>

<span data-ttu-id="75795-112">此指令碼使用下列命令來建立資源群組、虛擬機器和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="75795-112">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="75795-113">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="75795-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="75795-114">命令</span><span class="sxs-lookup"><span data-stu-id="75795-114">Command</span></span> | <span data-ttu-id="75795-115">注意事項</span><span class="sxs-lookup"><span data-stu-id="75795-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="75795-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="75795-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="75795-117">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="75795-117">Creates a resource group in which all resources are stored.</span></span> | 
| [<span data-ttu-id="75795-118">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="75795-118">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork)| <span data-ttu-id="75795-119">建立 Azure 虛擬網路和子網路。</span><span class="sxs-lookup"><span data-stu-id="75795-119">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="75795-120">Add-AzureRmVirtualNetworkPeering</span><span class="sxs-lookup"><span data-stu-id="75795-120">Add-AzureRmVirtualNetworkPeering</span></span>](/powershell/module/azurerm.network/add-azurermvirtualnetworkpeering) | <span data-ttu-id="75795-121">在兩個虛擬網路之間建立對等互連。</span><span class="sxs-lookup"><span data-stu-id="75795-121">Creates a peering between two virtual networks.</span></span>  |
| [<span data-ttu-id="75795-122">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="75795-122">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="75795-123">刪除資源群組，包括所有的巢狀資源。</span><span class="sxs-lookup"><span data-stu-id="75795-123">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="75795-124">後續步驟</span><span class="sxs-lookup"><span data-stu-id="75795-124">Next steps</span></span>

<span data-ttu-id="75795-125">如需有關 Azure PowerShell 的詳細資訊，請參閱 [Azure PowerShell 文件](https://docs.microsoft.com/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="75795-125">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="75795-126">您可以在 [Azure 網路概觀文件](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json)中找到其他網路 PowerShell 指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="75795-126">Additional networking PowerShell script samples can be found in the [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>