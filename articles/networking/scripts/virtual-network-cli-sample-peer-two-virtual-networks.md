---
title: "Azure CLI 指令碼範例 - 讓兩個虛擬網路對等互連 | Microsoft Docs"
description: "Azure CLI 指令碼範例 - 讓兩個虛擬網路對等互連"
services: virtual-network
documentationcenter: virtual-network
author: KumudD
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 07/07/2017
ms.author: kumud
ms.openlocfilehash: a2b8fda288072e2fb0087988bbd68d3e4d9031d8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="peer-two-virtual-networks"></a><span data-ttu-id="fd6d2-103">讓兩個虛擬網路對等互連</span><span class="sxs-lookup"><span data-stu-id="fd6d2-103">Peer two virtual networks</span></span>

<span data-ttu-id="fd6d2-104">此指令碼會在同一個區域中建立兩個虛擬網路，並透過 Azure 網路連接這兩個虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="fd6d2-104">This script creates and connects two virtual networks in the same region trhough the Azure network.</span></span> <span data-ttu-id="fd6d2-105">執行此指令碼之後，您將會在兩個虛擬網路之間建立對等互連。</span><span class="sxs-lookup"><span data-stu-id="fd6d2-105">After running the script, you will create a peering between two virtual networks.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


## <a name="sample-script"></a><span data-ttu-id="fd6d2-106">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="fd6d2-106">Sample script</span></span>

<span data-ttu-id="fd6d2-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/peer-two-virtual-networks/peer-two-virtual-networks.sh "讓兩個網路對等互連")]</span><span class="sxs-lookup"><span data-stu-id="fd6d2-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/peer-two-virtual-networks/peer-two-virtual-networks.sh "Peer two networks")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="fd6d2-108">清除部署</span><span class="sxs-lookup"><span data-stu-id="fd6d2-108">Clean up deployment</span></span> 

<span data-ttu-id="fd6d2-109">執行下列命令來移除資源群組、VM 和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="fd6d2-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="fd6d2-110">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="fd6d2-110">Script explanation</span></span>

<span data-ttu-id="fd6d2-111">此指令碼使用下列命令來建立資源群組、虛擬機器和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="fd6d2-111">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="fd6d2-112">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="fd6d2-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="fd6d2-113">命令</span><span class="sxs-lookup"><span data-stu-id="fd6d2-113">Command</span></span> | <span data-ttu-id="fd6d2-114">注意事項</span><span class="sxs-lookup"><span data-stu-id="fd6d2-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="fd6d2-115">az group create</span><span class="sxs-lookup"><span data-stu-id="fd6d2-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="fd6d2-116">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="fd6d2-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="fd6d2-117">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="fd6d2-117">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="fd6d2-118">建立 Azure 虛擬網路和子網路。</span><span class="sxs-lookup"><span data-stu-id="fd6d2-118">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="fd6d2-119">az network vnet peering create</span><span class="sxs-lookup"><span data-stu-id="fd6d2-119">az network vnet peering create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet/peering#create) | <span data-ttu-id="fd6d2-120">在兩個虛擬網路之間建立對等互連。</span><span class="sxs-lookup"><span data-stu-id="fd6d2-120">Creates a peering between two virtual networks.</span></span>  |
| [<span data-ttu-id="fd6d2-121">az group delete</span><span class="sxs-lookup"><span data-stu-id="fd6d2-121">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="fd6d2-122">刪除資源群組，包括所有的巢狀資源。</span><span class="sxs-lookup"><span data-stu-id="fd6d2-122">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="fd6d2-123">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fd6d2-123">Next steps</span></span>

<span data-ttu-id="fd6d2-124">如需 Azure CLI 的詳細資訊，請參閱 [Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="fd6d2-124">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="fd6d2-125">您可以在 [Azure 網路概觀文件](../cli-samples.md)中找到其他網路 CLI 指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="fd6d2-125">Additional networking CLI script samples can be found in the [Azure Networking Overview documentation](../cli-samples.md).</span></span>
