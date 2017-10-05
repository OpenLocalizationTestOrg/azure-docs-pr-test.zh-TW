---
title: "Azure CLI 指令碼範例 - 從快照集建立 VM | Microsoft Docs"
description: "Azure CLI 指令碼範例 - 從快照集建立 VM"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: ramankum
manager: kavithag
editor: ramankum
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/10/2017
ms.author: ramankum
ms.custom: mvc
ms.openlocfilehash: 6e47c3baebd5b68ec29d55c43dc00ae7665c81f2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-virtual-machine-from-a-snapshot-with-cli"></a><span data-ttu-id="c1bc4-103">使用 CLI 從快照集建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="c1bc4-103">Create a virtual machine from a snapshot with CLI</span></span>

<span data-ttu-id="c1bc4-104">此指令碼會從 OS 磁碟的快照集建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="c1bc4-104">This script creates a virtual machine from a snapshot of an OS disk.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="c1bc4-105">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="c1bc4-105">Sample script</span></span>

<span data-ttu-id="c1bc4-106">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-from-snapshot/create-vm-from-snapshot.sh "從快照集建立 VM")]</span><span class="sxs-lookup"><span data-stu-id="c1bc4-106">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-from-snapshot/create-vm-from-snapshot.sh "Create VM from snapshot")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="c1bc4-107">清除部署</span><span class="sxs-lookup"><span data-stu-id="c1bc4-107">Clean up deployment</span></span> 

<span data-ttu-id="c1bc4-108">執行下列命令來移除資源群組、VM 和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="c1bc4-108">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="c1bc4-109">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="c1bc4-109">Script explanation</span></span>

<span data-ttu-id="c1bc4-110">此指令碼使用下列命令來建立受控磁碟、虛擬機器和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="c1bc4-110">This script uses the following commands to create a managed disk, virtual machine, and all related resources.</span></span> <span data-ttu-id="c1bc4-111">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="c1bc4-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="c1bc4-112">命令</span><span class="sxs-lookup"><span data-stu-id="c1bc4-112">Command</span></span> | <span data-ttu-id="c1bc4-113">注意事項</span><span class="sxs-lookup"><span data-stu-id="c1bc4-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c1bc4-114">az snapshot show</span><span class="sxs-lookup"><span data-stu-id="c1bc4-114">az snapshot show</span></span>](https://docs.microsoft.com/cli/azure/snapshot#show) | <span data-ttu-id="c1bc4-115">使用快照集名稱和資源群組名稱取得快照集。</span><span class="sxs-lookup"><span data-stu-id="c1bc4-115">Gets snapshot using snapshot name and resource group name.</span></span> <span data-ttu-id="c1bc4-116">傳回物件的 Id 屬性用來建立受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="c1bc4-116">Id property of the returned object is used to create a managed disk.</span></span>  |
| [<span data-ttu-id="c1bc4-117">az disk create</span><span class="sxs-lookup"><span data-stu-id="c1bc4-117">az disk create</span></span>](https://docs.microsoft.com/cli/azure/disk#create) | <span data-ttu-id="c1bc4-118">使用快照集識別碼、磁碟名稱、儲存體類型和大小，從快照集建立受控磁碟</span><span class="sxs-lookup"><span data-stu-id="c1bc4-118">Creates managed disks from a snapshot using snapshot Id, disk name, storage type, and size</span></span>  |
| [<span data-ttu-id="c1bc4-119">az vm create</span><span class="sxs-lookup"><span data-stu-id="c1bc4-119">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="c1bc4-120">建立使用受控 OS 磁碟的 VM</span><span class="sxs-lookup"><span data-stu-id="c1bc4-120">Creates a VM using a managed OS disk</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c1bc4-121">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c1bc4-121">Next steps</span></span>

<span data-ttu-id="c1bc4-122">如需 Azure CLI 的詳細資訊，請參閱 [Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="c1bc4-122">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="c1bc4-123">您可以在 [Azure Linux VM 文件](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)中找到其他的虛擬機器 CLI 指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="c1bc4-123">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
