---
title: "CLI 指令碼範例-aaaAzure 從快照集建立的 VM |Microsoft 文件"
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
ms.openlocfilehash: ddc95289dcb8a0ca7c7854d969983f96b8f4613f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-from-a-snapshot-with-cli"></a><span data-ttu-id="c4006-103">使用 CLI 從快照集建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="c4006-103">Create a virtual machine from a snapshot with CLI</span></span>

<span data-ttu-id="c4006-104">此指令碼會從 OS 磁碟的快照集建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="c4006-104">This script creates a virtual machine from a snapshot of an OS disk.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="c4006-105">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="c4006-105">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-from-snapshot/create-vm-from-snapshot.sh "Create VM from snapshot")]

## <a name="clean-up-deployment"></a><span data-ttu-id="c4006-106">清除部署</span><span class="sxs-lookup"><span data-stu-id="c4006-106">Clean up deployment</span></span> 

<span data-ttu-id="c4006-107">執行下列命令 tooremove hello 資源群組、 VM 和所有相關的資源的 hello。</span><span class="sxs-lookup"><span data-stu-id="c4006-107">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="c4006-108">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="c4006-108">Script explanation</span></span>

<span data-ttu-id="c4006-109">此指令碼會使用下列命令 toocreate 受管理的磁碟，虛擬機器的 hello 和所有相關聯的資源。</span><span class="sxs-lookup"><span data-stu-id="c4006-109">This script uses hello following commands toocreate a managed disk, virtual machine, and all related resources.</span></span> <span data-ttu-id="c4006-110">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="c4006-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="c4006-111">命令</span><span class="sxs-lookup"><span data-stu-id="c4006-111">Command</span></span> | <span data-ttu-id="c4006-112">注意事項</span><span class="sxs-lookup"><span data-stu-id="c4006-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c4006-113">az snapshot show</span><span class="sxs-lookup"><span data-stu-id="c4006-113">az snapshot show</span></span>](https://docs.microsoft.com/cli/azure/snapshot#show) | <span data-ttu-id="c4006-114">使用快照集名稱和資源群組名稱取得快照集。</span><span class="sxs-lookup"><span data-stu-id="c4006-114">Gets snapshot using snapshot name and resource group name.</span></span> <span data-ttu-id="c4006-115">傳回物件 id 屬性是 hello 的使用的 toocreate 受管理的磁碟。</span><span class="sxs-lookup"><span data-stu-id="c4006-115">Id property of hello returned object is used toocreate a managed disk.</span></span>  |
| [<span data-ttu-id="c4006-116">az disk create</span><span class="sxs-lookup"><span data-stu-id="c4006-116">az disk create</span></span>](https://docs.microsoft.com/cli/azure/disk#create) | <span data-ttu-id="c4006-117">使用快照集識別碼、磁碟名稱、儲存體類型和大小，從快照集建立受控磁碟</span><span class="sxs-lookup"><span data-stu-id="c4006-117">Creates managed disks from a snapshot using snapshot Id, disk name, storage type, and size</span></span>  |
| [<span data-ttu-id="c4006-118">az vm create</span><span class="sxs-lookup"><span data-stu-id="c4006-118">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="c4006-119">建立使用受控 OS 磁碟的 VM</span><span class="sxs-lookup"><span data-stu-id="c4006-119">Creates a VM using a managed OS disk</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c4006-120">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c4006-120">Next steps</span></span>

<span data-ttu-id="c4006-121">如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="c4006-121">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="c4006-122">您可以找到額外的虛擬機器 CLI 指令碼範例在 hello [Azure Linux VM 文件](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="c4006-122">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
