---
title: "CLI 指令碼範例-aaaAzure 從快照集建立受管理的磁碟 |Microsoft 文件"
description: "Azure CLI 指令碼範例 - 從快照集建立受控磁碟"
services: virtual-machines-linux
documentationcenter: storage
author: ramankumarlive
manager: kavithag
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/19/2017
ms.author: ramankum
ms.openlocfilehash: 549692f5027b3f50b0dd89fe701ebbf0f51d6031
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-disk-from-a-snapshot-with-cli"></a><span data-ttu-id="a05af-103">使用 CLI 從快照集建立受控磁碟</span><span class="sxs-lookup"><span data-stu-id="a05af-103">Create a managed disk from a snapshot with CLI</span></span>

<span data-ttu-id="a05af-104">此指令碼會從快照集建立受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="a05af-104">This script creates a managed disk from a snapshot.</span></span> <span data-ttu-id="a05af-105">使用 toorestore OS 和資料磁碟的快照中的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a05af-105">Use it toorestore a virtual machine from snapshots of OS and data disks.</span></span> <span data-ttu-id="a05af-106">從個別的快照集建立 OS 和資料受控磁碟，再連結受控磁碟以建立新的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a05af-106">Create OS and data managed disks from respective snapshots and then create a new virtual machine by attaching managed disks.</span></span> <span data-ttu-id="a05af-107">您也可以連結從快照集建立的資料磁碟，以還原現有 VM 的資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="a05af-107">You can also restore data disks of an existing VM by attaching data disks created from snapshots.</span></span>


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="a05af-108">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="a05af-108">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-managed-disks-from-snapshot/create-managed-disks-from-snapshot.sh "Create managed disk from snapshot")]


## <a name="script-explanation"></a><span data-ttu-id="a05af-109">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="a05af-109">Script explanation</span></span>

<span data-ttu-id="a05af-110">此指令碼會使用下列命令 toocreate 受管理的磁碟，從快照集。</span><span class="sxs-lookup"><span data-stu-id="a05af-110">This script uses following commands toocreate a managed disk from a snapshot.</span></span> <span data-ttu-id="a05af-111">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="a05af-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="a05af-112">命令</span><span class="sxs-lookup"><span data-stu-id="a05af-112">Command</span></span> | <span data-ttu-id="a05af-113">注意事項</span><span class="sxs-lookup"><span data-stu-id="a05af-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="a05af-114">az snapshot show</span><span class="sxs-lookup"><span data-stu-id="a05af-114">az snapshot show</span></span>](https://docs.microsoft.com/cli/azure/snapshot#show) | <span data-ttu-id="a05af-115">取得所有快照集使用 hello 名稱 hello 內容和 hello 快照集的資源群組屬性。</span><span class="sxs-lookup"><span data-stu-id="a05af-115">Gets all hello properties of a snapshot using hello name and resource group properties of hello snapshot.</span></span> <span data-ttu-id="a05af-116">Id 屬性是使用的 toocreate 受管理的磁碟。</span><span class="sxs-lookup"><span data-stu-id="a05af-116">Id property is used toocreate managed disk.</span></span>  |
| [<span data-ttu-id="a05af-117">az disk create</span><span class="sxs-lookup"><span data-stu-id="a05af-117">az disk create</span></span>](https://docs.microsoft.com/cli/azure/disk#create) | <span data-ttu-id="a05af-118">使用受管理快照集的快照集識別碼建立受控磁碟</span><span class="sxs-lookup"><span data-stu-id="a05af-118">Creates a managed disk using snapshot Id of a managed snapshot</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a05af-119">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a05af-119">Next steps</span></span>

[<span data-ttu-id="a05af-120">將受控磁碟連結為 OS 磁碟以建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="a05af-120">Create a virtual machine by attaching a managed disk as OS disk</span></span>](./virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json)

<span data-ttu-id="a05af-121">如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="a05af-121">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="a05af-122">其他虛擬機器和受管理的磁碟 CLI 指令碼範例可以在 hello [Azure Linux VM 文件](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="a05af-122">Additional virtual machine and managed disks CLI script samples can be found in hello [Azure Linux VM documentation](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
