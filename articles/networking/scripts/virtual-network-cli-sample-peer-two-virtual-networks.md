---
title: "aaaAzure CLI 指令碼範例的對等的兩個虛擬網路 |Microsoft 文件"
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
ms.openlocfilehash: 54dabb2b9e05951d10f1b6b4f61ca592ce11d364
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="peer-two-virtual-networks"></a><span data-ttu-id="e3aea-103">讓兩個虛擬網路對等互連</span><span class="sxs-lookup"><span data-stu-id="e3aea-103">Peer two virtual networks</span></span>

<span data-ttu-id="e3aea-104">此指令碼會建立和連接 hello 中的兩個虛擬網路相同的區域 trhough hello Azure 網路。</span><span class="sxs-lookup"><span data-stu-id="e3aea-104">This script creates and connects two virtual networks in hello same region trhough hello Azure network.</span></span> <span data-ttu-id="e3aea-105">執行 hello 指令碼之後, 您將建立兩個虛擬網路之間對等互連。</span><span class="sxs-lookup"><span data-stu-id="e3aea-105">After running hello script, you will create a peering between two virtual networks.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


## <a name="sample-script"></a><span data-ttu-id="e3aea-106">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="e3aea-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/peer-two-virtual-networks/peer-two-virtual-networks.sh "Peer two networks")]

## <a name="clean-up-deployment"></a><span data-ttu-id="e3aea-107">清除部署</span><span class="sxs-lookup"><span data-stu-id="e3aea-107">Clean up deployment</span></span> 

<span data-ttu-id="e3aea-108">執行下列命令 tooremove hello 資源群組、 VM 和所有相關的資源的 hello。</span><span class="sxs-lookup"><span data-stu-id="e3aea-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="e3aea-109">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="e3aea-109">Script explanation</span></span>

<span data-ttu-id="e3aea-110">此指令碼會使用下列命令 toocreate 資源群組、 虛擬機器的 hello 和所有相關聯的資源。</span><span class="sxs-lookup"><span data-stu-id="e3aea-110">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="e3aea-111">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="e3aea-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="e3aea-112">命令</span><span class="sxs-lookup"><span data-stu-id="e3aea-112">Command</span></span> | <span data-ttu-id="e3aea-113">注意事項</span><span class="sxs-lookup"><span data-stu-id="e3aea-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="e3aea-114">az group create</span><span class="sxs-lookup"><span data-stu-id="e3aea-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="e3aea-115">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="e3aea-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="e3aea-116">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="e3aea-116">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="e3aea-117">建立 Azure 虛擬網路和子網路。</span><span class="sxs-lookup"><span data-stu-id="e3aea-117">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="e3aea-118">az network vnet peering create</span><span class="sxs-lookup"><span data-stu-id="e3aea-118">az network vnet peering create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet/peering#create) | <span data-ttu-id="e3aea-119">在兩個虛擬網路之間建立對等互連。</span><span class="sxs-lookup"><span data-stu-id="e3aea-119">Creates a peering between two virtual networks.</span></span>  |
| [<span data-ttu-id="e3aea-120">az group delete</span><span class="sxs-lookup"><span data-stu-id="e3aea-120">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="e3aea-121">刪除資源群組，包括所有的巢狀資源。</span><span class="sxs-lookup"><span data-stu-id="e3aea-121">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e3aea-122">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e3aea-122">Next steps</span></span>

<span data-ttu-id="e3aea-123">如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="e3aea-123">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="e3aea-124">其他網路功能的 CLI 指令碼範例可以在 hello [Azure 網路概觀文件](../cli-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="e3aea-124">Additional networking CLI script samples can be found in hello [Azure Networking Overview documentation](../cli-samples.md).</span></span>
